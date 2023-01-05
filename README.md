# Observability

[![syntasso](https://circleci.com/gh/syntasso/promise-observability.svg?style=shield)](https://app.circleci.com/pipelines/github/syntasso/promise-observability?branch=main)

This Promise provides Observability-as-a-Service by deploying [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus). The Promise has 2 field `.spec.namespace`,
which is the namespace the [Grafana](https://github.com/grafana/grafana) and [Prometheus](https://github.com/prometheus/prometheus) installation and `.spec.env` which can be `dev` or `prod`.

To install, run the following command while targeting your Platform cluster:

```
kubectl create -f https://raw.githubusercontent.com/syntasso/promise-observability/main/promise.yaml
```

This will install the Prometheus Operator into the clusters. To verify it is installed,
run the following command while targeting a worker cluster:

```
kubectl get deployment prometheus-operator
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
prometheus-operator   1/1     1            1           4h30m
```

To get an instance of Grafana and Prometheus make a resource request (dev by default), run the
following command while targeting your Platform cluster:

```
kubectl apply -f https://raw.githubusercontent.com/syntasso/promise-observability/main/resource-request.yaml
```

This will create an instance of Promethues and Grafana on the targeted worker cluster. This may take a few minutes. 

## Accessing UI

Prometheus and Grafana dashboards can be accessed quickly using `kubectl port-forward`. The
following commands should be run while targeting your worker cluster.

### Prometheus

```shell
$ kubectl --namespace monitoring port-forward svc/prometheus-k8s 9090
```

Then access via [http://localhost:9090](http://localhost:9090)

### Grafana

```shell
$ kubectl --namespace monitoring port-forward svc/grafana 3000
```

Then access via [http://localhost:3000](http://localhost:3000) and use the default grafana user:password of `admin:admin`.

## Development

For development see [README.md](./internal/README.md)

## Questions? Feedback?

We are always looking for ways to improve Kratix and the Marketplace. If you run into issues or have ideas for us, please let us know. Feel free to [open an issue](https://github.com/syntasso/kratix-marketplace/issues/new/choose) or [put time on our calendar](https://www.syntasso.io/contact-us). We'd love to hear from you.
