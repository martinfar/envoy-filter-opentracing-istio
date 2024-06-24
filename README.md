# Istio Filter for Opentracing

> About this project
>
> This project consist on a Lua filter for the envoy proxy in order to enable payload logs on the opentracing monitoring included in the Istio platform, this enable a powerful debug and reproducibility tool for transaction that need to be tested in case of error.
>

<a href="https://istio.io/">
    <img src="https://github.com/istio/istio/raw/master/logo/istio-bluelogo-whitebackground-unframed.svg"
         alt="Istio logo" title="Istio" height="100" width="100" />
</a>

---

## Change Log Level Istio Proxy

```
kubectl exec $(kubectl get pod --selector app=istio-ingressgateway --output jsonpath='{.items[0].metadata.name}' --namespace istio-system) --namespace istio-system -c istio-proxy -- curl -X POST http://localhost:15000/logging?level=warning
```

## Introduction

[Istio](https://istio.io/latest/docs/concepts/what-is-istio/) is an open platform for providing a uniform way to [integrate
microservices](https://istio.io/latest/docs/examples/microservices-istio/), manage [traffic flow](https://istio.io/latest/docs/concepts/traffic-management/) across microservices, enforce policies
and aggregate telemetry data. Istio's control plane provides an abstraction
layer over the underlying cluster management platform, such as Kubernetes.

Istio is composed of these components:

- **Envoy** - Sidecar proxies per microservice to handle ingress/egress traffic
  between services in the cluster and from a service to external
  services. The proxies form a _secure microservice mesh_ providing a rich
  set of functions like discovery, rich layer-7 routing, circuit breakers,
  policy enforcement and telemetry recording/reporting
  functions.

  > Note: The service mesh is not an overlay network. It
  > simplifies and enhances how microservices in an application talk to each
  > other over the network provided by the underlying platform.
  >
- **Istiod** - The Istio control plane. It provides service discovery, configuration and certificate management. It consists of the following sub-components:

  - **Pilot** - Responsible for configuring the proxies at runtime.
  - **Citadel** - Responsible for certificate issuance and rotation.
  - **Galley** - Responsible for validating, ingesting, aggregating, transforming and distributing config within Istio.
- **Operator** - The component provides user friendly options to operate the Istio service mesh.

## Repositories

The Istio project is divided across a few GitHub repositories:

- [istio/api](https://github.com/istio/api). This repository defines
  component-level APIs and common configuration formats for the Istio platform.
- [istio/community](https://github.com/istio/community). This repository contains
  information on the Istio community, including the various documents that govern
  the Istio open source project.
- [istio/istio](README.md). This is the main code repository. It hosts Istio's
  core components, install artifacts, and sample programs. It includes:

  - [istioctl](istioctl/). This directory contains code for the
    [_istioctl_](https://istio.io/latest/docs/reference/commands/istioctl/) command line utility.
  - [operator](operator/). This directory contains code for the
    [Istio Operator](https://istio.io/latest/docs/setup/install/operator/).
  - [pilot](pilot/). This directory
    contains platform-specific code to populate the
    [abstract service model](https://istio.io/docs/concepts/traffic-management/#pilot), dynamically reconfigure the proxies
    when the application topology changes, as well as translate
    [routing rules](https://istio.io/latest/docs/reference/config/networking/) into proxy specific configuration.
  - [security](security/). This directory contains [security](https://istio.io/latest/docs/concepts/security/) related code,
    including Citadel (acting as Certificate Authority), citadel agent, etc.
- [istio/proxy](https://github.com/istio/proxy). The Istio proxy contains
  extensions to the [Envoy proxy](https://github.com/envoyproxy/envoy) (in the form of
  Envoy filters) that support authentication, authorization, and telemetry collection.
