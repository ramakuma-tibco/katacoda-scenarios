Get a list of all pods in the `myproject` Namespace:
`kubectl get pods -n myproject`{{execute}}

Create a ReplicaSet object manifest file:

```
cat > replica-set.yaml <<EOF
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myfirstreplicaset
  namespace: myproject
spec:
  selector:
    matchLabels:
     app: myfirstapp
  replicas: 3
  template:
    metadata:
      labels:
        app: myfirstapp
    spec:
      containers:
        - name: nodejs
          image: openshiftkatacoda/blog-django-py
EOF
```{{execute}}

Create the ReplicaSet:

`kubectl apply -f replica-set.yaml`{{execute}}

In a new terminal window, select all pods that match `app=myfirstapp`:
`kubectl get pods -l app=myfirstapp --show-labels -w`{{execute}}

Delete the pods and watch new ones spawn:
`kubectl delete pod -l app=myfirstapp`{{execute}}

Imperatively scale the ReplicaSet to 6 replicas:
`kubectl scale replicaset myfirstreplicaset --replicas=6`{{execute}}

Imperatively scale down the ReplicaSet to 3 replicas:
`kubectl scale replicaset myfirstreplicaset --replicas=3`{{execute}}

The `oc scale` command interacts with the `/scale` endpoint:
`curl -X GET http://localhost:8001/apis/apps/v1/namespaces/myproject/replicasets/myfirstreplicaset/scale`{{execute}}

Use the `PUT` method against the `/scale` endpoint to change the number of replicas to 5:
`curl  -X PUT localhost:8001/apis/apps/v1/namespaces/myproject/replicasets/myfirstreplicaset/scale -H "Content-type: application/json" -d '{"kind":"Scale","apiVersion":"autoscaling/v1","metadata":{"name":"myfirstreplicaset","namespace":"myproject"},"spec":{"replicas":5}}'`{{execute}}

You can also get information regarding the pod by using the `GET` method against the `/status` endpoint
`curl -X GET http://localhost:8001/apis/apps/v1/namespaces/myproject/replicasets/myfirstreplicaset/status`{{execute}}

The status endpoint's primary purpose is to allow a controller (with proper RBAC permissions) to send a `PUT` method along with the desired status.