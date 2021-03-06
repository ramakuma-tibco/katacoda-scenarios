## Why an Operator? 
Operators make it easy to manage complex stateful applications on top of Kubernetes. However writing an Operator today can be difficult because of challenges such as using low level APIs, writing boilerplate, and a lack of modularity which leads to duplication.

## What is the Operator SDK?
The Operator SDK is a framework that uses the controller-runtime library to make writing Operators easier by providing:

High level APIs and abstractions to write the operational logic more intuitively.
Tools for scaffolding and code generation to bootstrap a new project fast.
Extensions to cover common Operator use cases.

## How do I use it?
The following is the workflow for a new Go-based Operator with the Operator SDK:

Create a new Operator project using the SDK CLI.
Create a new Custom Resource Definition API Type using the SDK CLI.
Add your Custom Resource Definition (CRD) to your live Kubernetes cluster.
Define your Custom Resource Spec and Status.
Create a new Controller for your Custom Resource Definition API.
Write the reconciling logic for your Controller.
Run the Operator locally to test your code against your live Kubernetes cluster.
Add your Custom Resource (CR) to your live Kubernetes cluster and watch your Operator in action!
After you are satisifed with your work, run some Makefile commands to build and generate the Operator Deployment manifests.
Optionally add additional APIs and Controllers using the SDK CLI.
## PodSet Operator
In this tutorial, we will create an Operator called a PodSet. A PodSet is a simple Controller/Operator that manages pods.

A user provides a number of pods specified in spec.replicas. The PodSet also conveniently outputs the name of all Pods currently controlled by the PodSet in the status.PodNames field.

Let's begin!