# helloword_with_mysql_helm

## Pre-Requisites

```bash
1. Install GIT
2. Install Java
3. Install Maven
4. Minikube Setup
5. Helm Install
```

## Install JAVA-8, GIT and Maven

```bash
yum install java-1.8.0-openjdk -y
yum install git -y
yum install maven -y
```
## kubernetes cluster - minikube
[minikube setup](https://github.com/Naresh240/kubernetes/blob/main/minikube-setup/README.md)

## Install helm

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
export PATH=$PATH:/usr/local/bin
./get_helm.sh
```

## Update Secret Values and Run

```bash
kubectl apply -f helm/mysql-secrets.yaml
```

# Deploy Helm Chart 

```bash
helm repo add helm-repo https://charts.bitnami.com/bitnami
helm install mysql-release helm-repo/mysql --dry-run --debug -f mysql-values.yaml
helm install mysql-release helm-repo/mysql -f helm/mysql/mysql-values.yaml
```

## Build and Deploy Springboot Applcation with helm

1. Build Springboot Applocation

```bash
mvn clean install
```

2. Build and Push docker image

```bash
docker build -t naresh240/springboothello:v1 .
docker login
docker push naresh240/springboothello:v1
```

3. Deploy Springboot Application

```bash
helm install springboothello helm/springboot-example
```

## Check application in UI
![image](https://user-images.githubusercontent.com/58024415/209840332-e3edb88f-6ed7-48bc-923d-9e02ff257b53.png)
