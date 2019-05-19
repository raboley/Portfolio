# Minikube Setup

The easiest way to get started with kubernetes is using [minikube](https://kubernetes.io/docs/setup/minikube/).

Follow the install instructions from the link and then using

``` bash
minikube start
```

will start up a new cluster!

This can be resource intensive on a laptop, and if the computer goes to sleep or loses network connectivity some things may stop working, so the easiest way to fix it is to delete everything in your cluster and start over.

``` bash
minikube delete
minikube start
```

This will delete the cluster and any pods or services that were on it.