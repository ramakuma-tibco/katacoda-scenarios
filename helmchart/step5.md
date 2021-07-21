Adding storage class
```
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml
```{{execute}}


Get list of storage class
`kubectl get sc`{{execute}}

Set as default storage class
`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`{{execute}}

Get list of storage class
`kubectl get sc`{{execute}}

