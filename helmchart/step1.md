This environment has a `launch.sh`{{execute}}

You can get with `kubectl get nodes`{{execute}}

Install helm
```
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```{{execute}}

check helm version `helm version`{{execute}}

install Helmfile
Download Helmfile 
```wget https://github.com/roboll/helmfile/releases/download/v0.139.9/helmfile_linux_amd64
mv helmfile_linux_amd64 /usr/bin/helmfile
chmod +x /usr/bin/helmfile
```{{execute}}

check Helmfile version `helmfile version`{{execute}}

