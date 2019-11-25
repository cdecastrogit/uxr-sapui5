# Proof of Concept for UXr Recruiting

## Get Started

### Prerequisities

Install [Docker](https://docs.docker.com/).

### Build the project

From within the local repository directory, run:

```sh
docker build -t uxr-sapui5 .
```

### Project Structure

### Start the project

```sh
docker run -P -d -p 9080:80 uxr-sapui5
```

Or 

```sh
docker-compose up -d
```



Once started, the project should be available locally at http://localhost:9080, or if running on a server at http://server_name:9080
	


To push the image to the Azure Container Registry

```sh
docker tag uxr-sapui5 uxrpocreg.azurecr.io/uxr-sapui5:v1
docker push  uxrpocreg.azurecr.io/uxr-sapui5:v1
```

To deploy to AKS

```sh
az aks get-credentials --resource-group recruiting-uxr --name recruiting-uxr-aks-eastus2
kubectl apply -f uxr-sapui5.yaml
```


To get the public ip

```sh
kubectl get service uxr-sapui5 --watch
```

Once the public ip goes from pending to actual ip, press CTRL-C.  For example

```sh
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   	PORT(S)        AGE
uxr-sapui5   LoadBalancer   10.0.247.115   <pending>     	80:32384/TCP   44s
uxr-sapui5   LoadBalancer   10.0.247.115   104.208.153.139	80:32384/TCP   2m25s
```

