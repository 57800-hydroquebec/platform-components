# MongoDB Database Helm Chart

A Helm Chart for installing a MongoDB instance

## Prerequisites

The mongodb-operator-helm chart has to be up and running before any steps below

## Deploying a MongoDB Replica Set

The Operator will be watching for resources of type
`mongodbcommunity.mongodbcommunity.mongodb.com`; you can quickly install
a Mongo Database with:

``` shell
helm install mongodb ./mongodb-helm
```

- _Note: A new user will be created with a generic password. Make sure this is
  only used for testing purposes._

After a few minutes you will have a 3-member MongoDB Replica Set installed in
your cluster, that you can check with:

``` shell
$ kubectl get mdbc
NAME              PHASE     VERSION
example-mongodb   Running   4.2.6
```

## Connecting to MongoDB from a Client Application

The Operator will create a `Secret` object, _per user_, created as part of the
deployment of the MongoDB resource. Each `Secret` will contain a _Connection
String_ that can be mounted into a client application to connect to this MongoDB
instance.

The name of this `Secret` object follows the convention[^1]:

- `<mongodb-resource-name>-<database>-<username>`.

[^1]: Please note that the MongoDB `username` should comply with
    [DNS-1123](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-label-names)
    for the Operator to be able to create this Secret. This is a known issue
    with the Community Operator.

In our example, the above `helm install` command will create a MongoDB resource
with name `mongodb`, with a user `my-user` on the Database `admin`. The
resulting `Secret` will be named:

- `mongodb-admin-my-user`

This `Secret` object will contain the following attributes:

- `connectionString.standard`
- `connectionString.standardSrv`
- `username`
- `password`

A client application will be able to connect using the `connectionString`
attributes or the `username` and `password` ones.
