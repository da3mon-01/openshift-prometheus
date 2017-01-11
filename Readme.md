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
