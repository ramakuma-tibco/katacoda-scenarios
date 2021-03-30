Let's create a new directory for our project:

`mkdir -p $HOME/projects/podset-operator`{{execute}}

Navigate to the directory:

`cd $HOME/projects/podset-operator`{{execute}}

Initialize a new Go-based Operator SDK project for the PodSet Operator:

`operator-sdk init --domain=example.com --repo=github.com/redhat/podset-operator`{{execute}}