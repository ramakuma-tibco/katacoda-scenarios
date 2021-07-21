deploy application using helmfile

```
cd helmdemo
helmfile sync
```{{execute}}

Check cluster status in new tab:
open a new tab and run following command:
watch kubectl get all -n helm-demo