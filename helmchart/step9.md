Helmfile upgrade
Install helm diff plugin `helm plugin install https://github.com/databus23/helm-diff`{{execute}}
change directory `cd helmdemo`{{execute}}
check helm relases `helm ls -n helm-demo`{{execute}}

Change on  of the deployment file
```
cat << EOF >webpyapp/templates/sleep-before.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sleep-delay-before
  annotations:
    "helm.sh/hook": pre-install,pre-upgrade
    "helm.sh/hook-weight": "1"
    "helm.sh/hook-delete-policy": before-creation,hook-succeeded
spec:
  template:
    spec:
      containers:
      - name: update-app
        image: bash
        command: ["sh",  "-c", "sleep 30"]
      restartPolicy: Never
  backoffLimit: 4
EOF
```{{execute}}

check diff `helmfile diff`{{execute}}
apply the diff `helmfile apply`{{execute}}

helmfile list command `helmfile list`{{execute}}
check helm release `helm ls -n helm-demo`{{execute}}
check release history `helm history webpyapp -n helm-demo`{{execute}}
  