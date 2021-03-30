Create a manifest for a Deployment with a Finalizer:
```
cat >> finalizer-test.yaml<<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: finalizer-test
  namespace: myproject
  labels:
    app: finalizer-test
  finalizers:
    - finalizer.extensions/v1beta1  
spec:
  selector:
    matchLabels:
      app: finalizer-test
  replicas: 3
  template:
    metadata:
      labels:
        app: finalizer-test
    spec:
      containers:
        - name: hieveryone
          image: openshiftkatacoda/blog-django-py
          imagePullPolicy: Always
          ports:
            - name: helloworldport
              containerPort: 8080
EOF
```{{execute}}

Create the Deployment.

`kubectl create -f finalizer-test.yaml`{{execute}}

Verify the Deployment has been created.

`kubectl get deploy -n myproject`{{execute}}

Verify the ReplicaSet has been created:

`kubectl get replicaset -n myproject`{{execute}}

Verify the pods are running:

`kubectl get pods -n myproject`{{execute}}

Attempt to delete the Deployment.

`kubectl delete deployment finalizer-test -n myproject`{{execute}}

Open up another terminal by clicking the + button and select `Open New Terminal`.

Observe the Deployment still exits and has been updated with the `deletionGracePeriodSeconds` and `deletionTimestamp` fields.

`kubectl get deployment finalizer-test -n myproject -o yaml | grep 'deletionGracePeriodSeconds\|deletionTimestamp'`{{execute}}

Attempt to scale the Deployment up and down. Although status is updated, pods will not be created/deleted:

```
kubectl scale deploy finalizer-test --replicas=5 -n myproject
kubectl scale deploy finalizer-test --replicas=1 -n myproject
```{{execute}}

```
kubectl get deploy -n myproject
kubectl get pods -n myproject
```{{execute}}


Update the Deployment with the Finalizer value unset.

```
cat >> finalizer-test-remove.yaml<<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: finalizer-test
  namespace: myproject
  labels:
    app: finalizer-test
  finalizers:
spec:
  selector:
    matchLabels:
      app: finalizer-test
  replicas: 3
  template:
    metadata:
      labels:
        app: finalizer-test
    spec:
      containers:
        - name: hieveryone
          image: openshiftkatacoda/blog-django-py
          imagePullPolicy: Always
          ports:
            - name: helloworldport
              containerPort: 8080
EOF
```{{execute}}

Replace the Deployment.

`kubectl replace -f finalizer-test-remove.yaml`{{execute}}

The Deployment will now be deleted.
```
kubectl get deploy -n myproject
kubectl get pods -n myproject
```{{execute}}