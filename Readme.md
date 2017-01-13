This is a deployment configuration that will install Prometheus on Openshift.

Before installing you need to create a service account with the cluster-reader role
to enable Prometheus read-only access rights to the Kubernetes API underneath Openshift.

My recommendation is a separate project named prometheus. If you want to use something else,
modify the oadm policy command accordingly:

```
oc new-project prometheus
oc create serviceaccount prometheus
oadm policy add-cluster-role-to-user cluster-reader system:serviceaccount:prometheus:prometheus
```

If you want to use a different serviceaccount, modify the deploymentConfig accordingly.

If you want to enable a pod/service for scraping, check out the comments in the jobs. An example deploymentConfig
that houses a Java application with the Prometheus Spring Boot exporter can be used with the following annotations in the DC
```
  annotations:
    prometheus.io/path: prometheus
    prometheus.io/port: '8080'
    prometheus.io/scrape: 'true'
```

Grafana Dashboard is based on https://github.com/instrumentisto/grafana-dashboard-kubernetes-prometheus, modified to use Openshift labels, instead of Kubernetes ones, where needed.
