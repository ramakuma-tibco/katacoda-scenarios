Helm Repository
helm search hub searches the Artifact Hub, which lists helm charts from dozens of different repositories.
`helm search hub wordpress`{{execute}}

Add a repo
`helm repo add brigade https://brigadecore.github.io/charts`{{execute}}
`helm repo add stable https://charts.helm.sh/stable`{{execute}}


helm search repo searches the repositories that you have added to your local helm client (with helm repo add). 
This search is done over local data, and no public network connection is needed.
`helm search repo wordpress`{{execute}}
