Create a Helm chart `helm create mychart`{{execute}}
check generated files `tree mychart`{{execute}}

Delete auto generated templates `rm -rf mychart/templates/*`{{execute}}

Create a config map
```
cat << EOF >mychart/templates/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mychart-configmap
data:
  myvalue: "Sample Config Map"
EOF
```{{execute}}

install the chart `helm install helm-demo-configmap ./mychart`{{execute}}

List helm charts `helm ls`{{execute}}

check resource in the cluster `kubectl get all`{{execute}}

Check Helm Manifest `helm get manifest helm-demo-configmap`{{execute}}

Check config map content `kubectl describe configmaps mychart-configmap`{{execute}}

Unisntall the helm chart `helm uninstall helm-demo-configmap`{{execute}}






