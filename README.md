# HAProxy Ingress controller

[Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) controller
implementation for [HAProxy](http://www.haproxy.org/) loadbalancer.

[![build](https://img.shields.io/github/workflow/status/jcmoraisjr/haproxy-ingress/build?logo=github)](https://github.com/jcmoraisjr/haproxy-ingress/actions/workflows/build.yaml) [![helm](https://img.shields.io/badge/helm%20chart-ready-blue?logo=helm)](https://artifacthub.io/packages/helm/haproxy-ingress/haproxy-ingress)

HAProxy Ingress is a Kubernetes ingress controller: it configures a HAProxy instance
to route incoming requests from an external network to the in-cluster applications.
The routing configurations are built reading specs from the Kubernetes cluster.
Updates made to the cluster are applied on the fly to the HAProxy instance.

## Use HAProxy Ingress

**Documentation:**

* Getting started guide: [/docs/getting-started/](https://haproxy-ingress.github.io/docs/getting-started/)
* Global and per ingress/service configuration keys: [/docs/configuration/keys/](https://haproxy-ingress.github.io/docs/configuration/keys/)
* Command-line options: [/docs/configuration/command-line/](https://haproxy-ingress.github.io/docs/configuration/command-line/)

**Supported versions:**

| HAProxy Ingress                                      | Embedded<br/>HAProxy | Supported<br/>Kubernetes | External<br/>HAProxy (*) |
|------------------------------------------------------|----------------------|--------------------------|--------------------------|
| [`v0.13`](CHANGELOG/CHANGELOG-v0.13.md) **(latest)** | `2.3`                | `1.19+`                  | `2.2+`                   |
| [`v0.12`](CHANGELOG/CHANGELOG-v0.12.md)              | `2.2`                | `1.18` - `1.21`          | `2.0+`                   |
| [`v0.10`](CHANGELOG/CHANGELOG-v0.10.md)              | `2.0`                | `1.8` - `1.21`           | -                        |

* Beta quality versions (`beta` / `canary` tags) has some new, but battle tested features, usually running on some of our production clusters
* Development versions (`alpha` / `snapshot` tags) has major changes with few tests, usually not recommended for production
* (*) Minimum supported HAProxy version if using an [external HAProxy](https://haproxy-ingress.github.io/docs/examples/external-haproxy/) instance

**Community:**

* [Slack](https://kubernetes.slack.com/channels/haproxy-ingress): We're in the [#haproxy-ingress](https://kubernetes.slack.com/channels/haproxy-ingress) channel on Kubernetes Slack. Take an invite [here](https://slack.k8s.io) if not subscribed yet
* [Users mailing list](https://groups.google.com/forum/#!forum/haproxy-ingress): Announcements and discussion on a mailing list
* [Stack Overflow](https://stackoverflow.com/questions/tagged/haproxy-ingress): Practical questions and curated answers

## Develop HAProxy Ingress

Building:

```
mkdir -p $GOPATH/src/github.com/jcmoraisjr
cd $GOPATH/src/github.com/jcmoraisjr
git clone https://github.com/jcmoraisjr/haproxy-ingress.git
cd haproxy-ingress
make
```

The following `make` targets are currently supported:

* `install`: run `go install` which saves some building time.
* `build` (default): compiles HAProxy Ingress and generates an ELF (Linux) executable at `rootfs/haproxy-ingress-controller` despite the source platform.
* `test`: run unit tests
* `image`: generates a Docker image tagged `localhost/haproxy-ingress:latest`
