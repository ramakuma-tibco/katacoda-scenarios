Begin by running a proxy to the Kubernetes API server:

`kubectl proxy --port=8001`{{execute}}

Open up another terminal by clicking the + button and select `Open New Terminal`.


Let's create a new Custom Resource Definition (CRD) object manifest for Postgres:

```
cat >> postgres-crd.yaml <<EOF
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: postgreses.rd.example.com
spec:
  group: rd.example.com
  names:
    kind: Postgres
    listKind: PostgresList
    plural: postgreses
    singular: postgres
    shortNames:
    - pg
  scope: Namespaced
  versions:
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        type: object
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: true
EOF
```

Create the CRD resource object:

`kubectl create -f postgres-crd.yaml`{{execute}}

You should now see the Kubernetes API reflect a brand new api group called rd.example.com:

`curl http://localhost:8001/apis | jq .groups[].name`{{execute}}

This will also be reflected in the `kubectl api-versions` command:

`kubectl api-versions`{{execute}}

Within the rd.example.com group there will be an api version v1alpha1 (per our CRD resource object). The database resource resides here.

`curl http://localhost:8001/apis/rd.example.com/v1alpha1 | jq`{{execute}}

Notice how kubectl now recognize postgres as a present resource (although there will be no current resource objects at this time).

`kubectl get postgres`{{execute}}

Let's create a new Custom Resource (CR) object manifest for the database:
```
cat >> wordpress-database.yaml <<EOF
apiVersion: "rd.example.com/v1alpha1"
kind: Postgres
metadata:
  name: wordpressdb
spec:
  user: postgres
  password: postgres
  database: primarydb
  nodes: 3
EOF
```
Create the new object:

`kubectl create -f wordpress-database.yaml`{{execute}}

Verify the resource was created:

`kubectl get postgres`{{execute}}

View the details about the wordpressdb object:

`kubectl get postgres wordpressdb -o yaml`{{execute}}