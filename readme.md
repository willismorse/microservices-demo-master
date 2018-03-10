helm install  chart --namespace microservices-demo


# Commands

```
# Upgrade a current release. Since all our docker images are tagged with latest, this will magically pull any new images that are available since the last intall/upgrade of this chart
helm upgrade <release-name> microservices-demo-master-chart/