In a new terminal, inspect the Custom Resource manifest:

```
cd $HOME/projects/podset-operator
cat config/samples/app_v1alpha1_podset.yaml
```

Ensure your `kind: PodSet` Custom Resource (CR) is updated with `spec.replicas`

apiVersion: app.example.com/v1alpha1
kind: PodSet
metadata:
  name: podset-sample
spec:
  replicas: 3
You can easily update this file by running the following command:

`\cp /tmp/app_v1alpha1_podset.yaml config/samples/app_v1alpha1_podset.yaml`{{execute}}

Ensure you are currently scoped to the myproject Namespace:

`kubectl  project myproject`{{execute}}

Deploy your PodSet Custom Resource to the live OpenShift Cluster:

`kubectl  create -f config/samples/app_v1alpha1_podset.yaml`{{execute}}

Verify the Podset exists:

`kubectl  get podset`{{execute}}

Verify the PodSet operator has created 3 pods:

`kubectl  get pods`{{execute}}

Verify that status shows the name of the pods currently owned by the PodSet:

`kubectl  get podset podset-sample -o yaml`{{execute}}

Increase the number of replicas owned by the PodSet:

`kubectl  patch podset podset-sample --type='json' -p '[{"op": "replace", "path": "/spec/replicas", "value":5}]'`{{execute}}


Verify that we now have 5 running pods

`kubectl  get pods`{{execute}}