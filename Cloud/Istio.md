# Istio
> Oferece de forma facil recursos de service mash com dois componenetes: Data Plane (intercepta trafego) && Control Plane (controle de trafego)
> Oque é um service mash? Permuite incluir nos microserviços mais observabilidade, gerenciamento de trafego e segurança com TLS sem adicionar nada no código.

## Instalando

### Criando ambiente
``` shell script
### Usuario root
curl -sfL https://get.k3s.io | sh -

### checa se o cluster ta no ar
kubectl get nodes
```

### Install Istio

- <https://istio.io/latest/docs/setup/getting-started//>
- [profiles](https://istio.io/latest/docs/setup/additional-setup/config-profiles/)

``` shell script
### Usuario root
### default || demo

curl -L https://istio.io/downloadIstio | sh -
cd istio-1.20.3
export PATH=$PWD/bin:$PATH
istioctl install --set profile=default -y
sudo cp /etc/rancher/k3s/k3s.yaml .
sudo sed -i 's:localhost:hoseplak3s:;s:default:TheNameOfYourHost:g' k3s.yaml
sudo KUBECONFIG=~/.kube/config:k3s.yaml kubectl config view --raw > config.tmp
sudo mv config.tmp /root/.kube/config
sudo istioctl manifest apply --set profile=default

### check istio
kubectl get ns
kubectl get all -n istio-system

### habilita por namespace, só trocaro default pelo nome
kubectl label namespace default istio-injection=enabled
```

### Deploy exemplo BookInfo

``` shell SCRIPT
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

### verificando o Ingress
kubectl get svc -n istio-system

### Procura o serviço istio-ingressgateway e ve qual porta representa a 80 (,80:XXXXX/TCP)
### Pega o IP da maquina e acessa, em ec2 só pegar o nome completo da maquina (ec2-XX-XX-XXX-XXX.compute....)
### IP:XXXXX/productpage
```

### Dashboard

``` shell script
kubectl apply -f samples/addons
kubectl rollout status deployment/kiali -n istio-system

### verificando
kubectl get svc -n istio-system

### alterando grafana e kiali, troca o tipo de ClusterIp para NodePort

kubectl edit svc -n istio-system grafana
kubectl edit svc -n istio-system kiali

### Lembrando que salva no :wq
```

## Traffic Management

### Editando o gateway
``` shell script
kubectl get getway bookinfo-gateway -o yaml
```

### Virtual service
> Define o roteamento, ou seja como chegar no destino
Podemos:
1. Definir o destino da requisição
2. Criar regras por usuario
3. Definir um load balance para redirecionar parte das requisições para outro destino

``` shell script
kubectl get gateway
kubectl get virtualservice bookinfo -o yaml
```

### Destination rules
> Oque acontece com o trafego no destino
```shell script
kubectl get destinationrules reviews -o yaml
```

## Security
### Globally TLS in STRICT mode
> Com isso habilitar requisição de origem apenas para pods que tem um side car com a policita de TLS habilitado

``` shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: "default"
  namespace: "istio-system"
spec:
  mtls:
    mode: STRICT
EOF

## Get All
kubectl get peerauthentication -all-namespaces

## Delete
kubectl delete peerauthentication -n istio-system default

```

### Enable mutual TLS per namespace or workload
``` shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: "default"
  namespace: "foo"
spec:
  mtls:
    mode: STRICT
EOF

```

### HTTP Trafic
#### Não permite nada
``` shell script
$ kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: allow-nothing
  namespace: default
spec:
  {}
EOF
```

#### Habilitando 1 pod e 1 metodo
``` shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: "productpage-viewer"
  namespace: default
spec:
  selector:
    matchLabels:
      app: productpage
  action: ALLOW
  rules:
  - to:
    - operation:
        methods: ["GET"]
EOF
```

#### Habilitando 1 pod e 1 metodo e uma origem (conta de serviço)
``` shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: "reviews-viewer"
  namespace: default
spec:
  selector:
    matchLabels:
      app: reviews
  action: ALLOW
  rules:
  - from:
    - source:
        principals: ["cluster.local/ns/default/sa/bookinfo-productpage"]
    to:
    - operation:
        methods: ["GET"]
EOF

## Clean all
kubectl delete authorizationpolicy.security.istio.io/allow-nothing

```

### TCP Traffic
#### Habilita 9000 && 9000
```shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: tcp-policy
  namespace: foo
spec:
  selector:
    matchLabels:
      app: tcp-echo
  action: ALLOW
  rules:
  - to:
    - operation:
        ports: ["9000", "9001"]
EOF
```

#### Só habilita GET na 9000
```shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: tcp-policy
  namespace: foo
spec:
  selector:
    matchLabels:
      app: tcp-echo
  action: ALLOW
  rules:
  - to:
    - operation:
        methods: ["GET"]
        ports: ["9000"]
EOF
```

#### Só bloqueia o GET
```shell script
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: tcp-policy
  namespace: foo
spec:
  selector:
    matchLabels:
      app: tcp-echo
  action: DENY
  rules:
  - to:
    - operation:
        methods: ["GET"]
EOF
```

### Egress
#### Controlled access to external services
> Somente oque for configurado vai estar habilitado
``` shellscript
## vamos alterar de "ALLOW_ANY" para "REGISTRY_ONLY"
$ istioctl install --set meshConfig.outboundTrafficPolicy.mode=REGISTRY_ONLY
```

#### Liberando acesso ao google
```shell script
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1alpha3
kind: ServiceEntry
metadata:
  name: google
spec:
  hosts:
  - www.google.com
  ports:
  - number: 443
    name: https
    protocol: HTTPS
  resolution: DNS
  location: MESH_EXTERNAL
EOF
```

#### Definindo timeout
```shell script
$ kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin-ext
spec:
  hosts:
    - www.google.com
  http:
  - timeout: 3s
    route:
      - destination:
          host: httpbin.org
        weight: 100
EOF
```

---

### Kubernets commands
```shell script
### Get Pods
kubectl get pods

### Get Services
kubectl get services
```

### Habilitando o Istio em qualquer lugar
``` shell script
### Tem que ir primeiro ate o home
cp istio-1.14.2/bin/istioctl /usr/local/bin/
```

### Notas: Com o virtual service podemos gerencia e redirecionar todas as requisições ao mesmo endpoint trocando apenas o path para redirecionar as APIs sem a necessidade das url customizadas
