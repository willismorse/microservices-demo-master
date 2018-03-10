
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
helm install microservices-demo-master-chart/ --namespace microservices-demo

# Upgrade a current release. Since all our docker images are tagged with latest, this will magically pull any new images that are available since the last intall/upgrade of this chart
helm upgrade <release-name> microservices-demo-master-chart/
```
