check genereated Template:
`helmfile --state-values-set storage.storageClass=local-path template` {{execute}}

Check cluster status in new tab:
open a new tab and run following command:
`watch kubectl get all -n helm-demo`{{execute}}

deploy application using helmfile
```
cd helmdemo
helmfile sync
```{{execute}}

List Helm release
`helm ls -A`{{execute}}

