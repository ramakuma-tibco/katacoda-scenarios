This environment has a `launch.sh`{{execute}}

You can get with `kubectl get nodes`{{execute}}

Create a new pod manifest that specifies two containers:
```
cat > pod-multi-container.yaml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: my-two-container-pod
  namespace: myproject
  labels:
    environment: dev
spec:
  containers:
    - name: server
      image: nginx:1.13-alpine
      ports:
        - containerPort: 80
          protocol: TCP
    - name: side-car
      image: alpine:latest
      command: ["/usr/bin/tail", "-f", "/dev/null"]
  restartPolicy: Never 
  EOF
  ```

  Create the pod by specifying the manifest:
  `kubectl create -f pod-multi-container.yaml`{{execute}}

  View the detail for the pod and look at the events:
  `kubectl describe pod my-two-container-pod`{{execute}}

  Let's first execute a shell session inside the server container by using the -c flag:
  `kubectl` exec -it my-two-container-pod -c server -- /bin/sh`{{execute}}

 Run some commands inside the server container:
 ```
ip address
netstat -ntlp
hostname
ps
exit
```
Let's now execute a shell session inside the side-car container:
`kubectl exec -it my-two-container-pod -c side-car -- /bin/sh`
Run the same commands in side-car container. Each container within a pod runs it's own cgroup, but shares IPC, Network, and UTC (hostname) namespaces:
```
ip address
netstat -ntlp
hostname
exit
```{{execute}}
