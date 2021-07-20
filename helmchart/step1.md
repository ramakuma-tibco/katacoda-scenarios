Check kubernetes cluster status `launch.sh`{{execute}}

You can get nodes with `kubectl get nodes`{{execute}}

Install helm
```
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```{{execute}}

check helm version `helm version`{{execute}}
