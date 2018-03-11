
This repo provides a Helm chart to assemble a cluster of microservices. 

Uses the Sock Shop catalogue database microservice from https://microservices-demo.github.io/, and adds some microfrontend microservices.

This is part of a collection of demo repos:

### This repo. Master chart to install everything
https://github.com/willismorse/microservices-demo-master

### Hostapp µFrontend
https://github.com/willismorse/microservices-demo-microfrontend-hostapp

### Header µFrontend
https://github.com/willismorse/microservices-demo-microfrontend-header

### Products µFrontend
https://github.com/willismorse/microservices-demo-microfrontend-products

### Catalog DB µService
https://github.com/willismorse/microservices-demo-microservice-catalog



# Commands

```
# Initial install
helm repo add microservices-demo-microfrontend-hostapp  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-hostapp/master/
helm repo add microservices-demo-microfrontend-products  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-products/master/
helm repo add microservices-demo-microfrontend-header  https://raw.githubusercontent.com/willismorse/microservices-demo-microfrontend-header/master/
helm repo add microservices-demo-microservice-catalog  https://raw.githubusercontent.com/willismorse/microservices-demo-microservice-catalog/master/
cd microservices-demo-master-chart/
helm dep up
cd ..
helm install microservices-demo-master-chart/ --namespace microservices-demo
# Note the NAME field in the output. This is Helm's generated Release Name for this instance of the installed collection of parts.
# You will use this release name in subsequent calls to the `helm` command for various admin tasks

# View all releases that you have installed
helm list

# Upgrade a current release. Since all our docker images that are referenced in these charts pull from the ':latest' tag, this will magically pull any new images that are available since the last intall/upgrade of this chart
helm upgrade <release-name> microservices-demo-master-chart/

# Delete a release. This will shutdown and remove all parts that were installed previously
helm delete <release-name>
```
