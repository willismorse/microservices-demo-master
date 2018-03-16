
This repo provides a Helm chart to assemble a cluster of microservices. It uses the existing Sock Shop catalogue database microservice from https://microservices-demo.github.io/, and adds some microfrontend microservices.

This is part of a collection of repos that create microservice artifacts:

### This repo. Umbrella chart to install everything
https://github.com/willismorse/microservices-demo-master

### Hostapp µFrontend
Provides the main index.html which implicitly loads the µFrontend as JS scripts
https://github.com/willismorse/microservices-demo-microfrontend-hostapp

### Header µFrontend
React component microfrontend script that will mount itself into the calling HTML document
https://github.com/willismorse/microservices-demo-microfrontend-header

### Products µFrontend
React component microfrontend script that will mount itself into the calling HTML document
https://github.com/willismorse/microservices-demo-microfrontend-products

### Catalog DB µService
Headless microservice that provides a REST API to query the product catalogue database. This repo just contains a Helm chart to pull and install the WeaveWorks SockShop Catalogue microservice

https://github.com/willismorse/microservices-demo-microservice-catalog





## Initial install

### Initial local helm setup
```
helm repo add microservices-demo-microfrontend-hostapp  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-hostapp/master/

helm repo add microservices-demo-microfrontend-products  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-products/master/

helm repo add microservices-demo-microfrontend-header  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-header/master/

helm repo add microservices-demo-microservice-catalog  https://raw.githubusercontent.com/willismorse/microservices-demo-microservice-catalog/master/
```

### Initial pull of child charts
```
cd <project-dir>/microservices-demo-master-chart/
helm dep up
cd ..
helm install microservices-demo-master-chart/ --namespace microservices-demo
```

Note the NAME field in the commandline output from `helm install`. This is Helm's generated Release Name for this instance of the installed collection of parts. You will use this release name in subsequent calls to the `helm` command for various admin tasks

## View all releases that you have installed
```
helm list
```


## Pulling changes to microfrontend/microservice images
When you make changes to one of your microservices or microfrontends, you must first delete the corresponding pod in Minikube. After you delete pod(s), the next time that you upgrade the umbrella chart Helm will implicitly recreate any missing child pods, which will in turn implicitly pull new copies of their underlying Docker images (since we are using the `:latest` tag on images) 

### Delete pod(s) prior to upgrading chart
```
kubectl delete pod <pod-name> --namespace=podnamespaceifany
```
This gets around an issue where upgrading a child chart will not (always?) force a new copy of the underlying image to be pulled, even if we specify the image as :latest and our pull policy as Always. This seems to be an active bug/problem in Kubernetes.

Reference:
* https://github.com/kubernetes/helm/issues/2735 
* https://github.com/kubernetes/kubernetes/issues/33664
 
### Upgrade main chart 

```
helm upgrade <release-name> microservices-demo-master-chart/
```


## Pulling changes to microfrontend/microservice charts 
```
cd microservices-demo-master-chart/
helm dep up
cd ..
```

## Delete a release. This will shutdown and remove all parts that were installed previously
```
helm delete <release-name>
```


