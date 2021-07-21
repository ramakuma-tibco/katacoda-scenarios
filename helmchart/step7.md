Create a helmfile:

```
cat > helmfile.yaml <<EOF
releases:
- name: webpyapp
  chart: ./webpyapp
  wait: true
EOF
```{{execute}}

check template `helmfile template`{{execute}}