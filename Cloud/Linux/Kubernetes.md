# Kubernetes
> gerencia os containers

### **Instalando kubectl**  
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl && mv kubectl /usr/local/bin/
```

**Instalando o minikube**  
```
curl -Lo minikube https://github.com/kubernetes/minikube/releases/download/v0.28.0/minikube-linux-amd64
chmod +x minikube && mv minikube /usr/local/bin/
 OBS: apt-get install kubelet kubectl kubeadm
minikube start
kubectl get nodes - visualiza todos os minikube
```

### **Instalando Kubernets**  
```
https://www.linuxtips.com.br/blog/descomplicando-o-kubernetes-02
curl -fsSL https://get.docker.com | bash
apt-get update && apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
apt-get update
apt-get install -y kubelet kubeadm kubectl
```

- **NO MASTER**  
```
kubeadm init --apiserver-advertise-address IpDoMaster - ip do master pode ser o host com a porta certa
 OBS: esse comando devolve oque deve ser executado nas outras maquinas
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```

- **OUTRAS MAQUINA**  
*executa o comando q o "kubeadm init.." do master devolveu*

- **NO MASTER**  
```
kubectl get nodes - tras maquinas no cluster
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')" - configura o cluster
kubectl run NOME --image IMAGEM --replicas NUMERO - vai criar um numero de pods dividindo nos servidores
```

### **Monit**
> Monitoramento nao nativo do Kubernets
-  sysdig

