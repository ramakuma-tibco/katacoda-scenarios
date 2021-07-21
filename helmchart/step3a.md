#Built-in objects
update the values file
```
cat << EOF >mychart/values.yaml
costCode: CC98112
projectCode: MyProject
EOF
```{{execute}}

Update config map 
Create a config map
```
cat << EOF >mychart/templates/configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mychart-configmap
data:
  myvalue: "Sample Config Map"
  costCode: {{ .Values.costCode }}
  contact: {{ .Values.contact | default "1-800-123-0000" | quote }}
  pipeline: {{ .Values.projectCode | upper | quote }}
EOF
```{{execute}}


Dry Run `helm install --debug --dry-run firstdryrun ./mychart`{{execute}}
 
 
 Install chart `helm install firstvalue ./mychart`{{execute}}
 
 
Check Helm Manifest `helm get manifest firstvalue`{{execute}}
 
`kubectl describe configmaps mychart-configmap`{{execute}}

Unisntall the helm chart `helm uninstall firstvalue`{{execute}}
