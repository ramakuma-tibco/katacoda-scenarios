`cd helmdemo`{{execute}}
check genereated Template:
`helmfile --state-values-set storage.storageClass=local-path template`{{execute}}

Check cluster status in new tab:
open a new tab and run following command:
`watch kubectl get all -n helm-demo`{{execute}}

deploy application using helmfile
`helmfile --state-values-set storage.storageClass=local-path sync`{{execute}}

Check PVC `kubectl get pvc -n helm-demo`{{execute}}

Check PV `kubectl get pv`{{execute}}

Check kubernetres resources:
`kubectl get all -n helm-demo`{{execute}}

List Helm release
`helm ls -A`{{execute}}



