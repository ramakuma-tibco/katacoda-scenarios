Verify the currently available Kubernetes API versions:
`kubectl api-versions`{{execute}}

Use the --v flag to set a verbosity level. This will allow you to see the request/responses against the Kubernetes API:

`kubectl get pods -n myproject --v=8`{{execute}}

Use the oc proxy command to proxy local requests on port 8001 to the Kubernetes API:

`kubectl proxy --port=8001`{{execute}}

Open up another terminal by clicking the + button and select `Open New Terminal`.

Send a `GET` request to the Kubernetes API using `curl`:
`curl -X GET http://localhost:8001`{{execute}}

We can explore the OpenAPI definition file to see complete API details.
`curl localhost:8001/openapi/v2`{{execute}}

Send a `GET` request to list all pods in the environment:
`curl -X GET http://localhost:8001/api/v1/pods`{{execute}}

Use jq to parse the json response:
`curl -X GET http://localhost:8001/api/v1/pods | jq .items[].metadata.name`{{execute}}

We can scope the response by only viewing all pods in a particular `namespace`:
`curl -X GET http://localhost:8001/api/v1/namespaces/myproject/pods`{{execute}}

Export the manifest associated with `my-two-container-pod` in `json` format:
`kubectl get pods my-two-container-pod -n myproject --export -o json > podmanifest.json`{{execute}}

Within the manifest, replace the 1.13 version of alpine with 1.14:
`sed -i 's|nginx:1.13-alpine|nginx:1.14-alpine|g' podmanifest.json`{{execute}}

Update/Replace the current pod manifest with the newly updated manifest:
`curl -X PUT http://localhost:8001/api/v1/namespaces/myproject/pods/my-two-container-pod -H "Content-type: application/json" -d @podmanifest.json`{{execute}}

Patch the current pod with a newer container image (1.15):
`curl -X PATCH http://localhost:8001/api/v1/namespaces/myproject/pods/my-two-container-pod -H "Content-type: application/strategic-merge-patch+json" -d '{"spec":{"containers":[{"name": "server","image":"nginx:1.15-alpine"}]}}`{{execute}}

Delete the current pod by sending the `DELETE` request method:
`curl -X DELETE http://localhost:8001/api/v1/namespaces/myproject/pods/my-two-container-pod`{{execute}}

Verify the pod is in `Terminating` status:

`kubectl get pods -n myproject`{{execute}}

Verify the pod no longer exists:
`curl -X GET http://localhost:8001/api/v1/namespaces/myproject/pods/my-two-container-pod`{{execute}}