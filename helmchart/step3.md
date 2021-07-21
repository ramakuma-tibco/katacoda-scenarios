#Built-in objects
update the config map template
```
cat << EOF >configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Sample Config Map"
EOF
```{{execute}}

Install the chart `helm install releasename-test ./mychart`{{execute}}

  
Check manifest `helm get manifest releasename-test`{{execute}}

Dry Run without installing the chart `helm install --debug --dry-run dryrun-test ./mychart`{{execute}}

Check config map `kubectl describe configmaps releasename-test-configmap`{{execute}}

Uninstall `helm uninstall releasename-test`{{execute}}
