# goal
Alert on container restart, replicas unavailable and the like, based on kube-state-metrics. A reference implementation.

# method
Use metricbeat to forward kube-state-metrics to es for storage and then alerting to opsgenie.

```bash
# run cluster
$ minikube start
# run es and kibana on host for simplicity
$ docker-compose up -d
# deploy kube-state-metrics and metricbeat
$ kubectl apply -R -f manifests
```

# kube-state metrics in es

container ready and restart count
- kubernetes.container.status.ready - bool
- kubernetes.container.name - string
- kubernetes.container.status.phase - string i.e running
- kubernetes.container.status.restarts - num

replicas unavailable
- kubernetes.deployment.name - string
- kubernetes.deployment.replicas.unavailable - num
- kubernetes.namespace - string

# todos
- [x] run kube-state-metrics in cluster
- [x] run es and kibana on host
- [x] run metricbeat w k8s module in cluster
- [x] profit
- [ ] kube state limits
- [ ] opsgenie integration
