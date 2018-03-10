
Assembles a cluster of microservices. 

Uses the Sock Shop catalogue database microservice from https://microservices-demo.github.io/, and adds some microfrontend microservices.


# Commands

```
# Initial install
helm install microservices-demo-master-chart/ --namespace microservices-demo

# Upgrade a current release. Since all our docker images are tagged with latest, this will magically pull any new images that are available since the last intall/upgrade of this chart
helm upgrade <release-name> microservices-demo-master-chart/
```