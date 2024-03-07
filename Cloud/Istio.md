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
