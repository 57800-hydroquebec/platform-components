# MongoDB Community Kubernetes Operator Helm Chart

A Helm Chart for installing and upgrading the [MongoDB Community
Kubernetes Operator](https://github.com/mongodb/mongodb-kubernetes-operator).


## Installing the Operator

You can install the MongoDB Community Operator easily with:

``` shell
helm install mongodb-operator ./mongodb-operator-helm
```

This will install `CRD`s and Community Operator in the current namespace
(`default` by _default_). You can pass a different namespace with:

``` shell
helm install mongodb-operator ./mongodb-operator-helm --namespace mongodb [--create-namespace]
```

To install the Community Operator in a namespace called `mongodb` with the
optional `--create-namespace` in case `mongodb` didn't exist yet.


