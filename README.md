This Repository has examples copied from below:

[This code's documentation lives on the grpc.io site.](https://grpc.io/docs/quickstart/python.html)

# gRPC Load Balancing with Linkerd

Steps taken:

Create greeter-client and greeter-server (adapted from example https://grpc.io/docs/languages/python/quickstart/)

Create Docker files for both

Push images to Dockerhub

Create deployment and service manifests for both (`greeter.yaml`, `greeter-client.yaml`)

Apply manifests on Kubernetes: 

`kubectl apply -f greeter.yaml`
`kubectl apply -f greeter-client.yaml`

Open 3 terminal windows to see client pods logs. Observe that only one is outputting logs.

Install Linkerd (follow this https://linkerd.io/2/getting-started/)

Inject linkerd container to cliet pods:

```
kubectl get deploy greeter-client -o yaml \
  | linkerd inject - \
  | kubectl apply -f -
```

The client messages should be spread accross the 3 servers