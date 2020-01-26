---
title: "Using Kourier With Knative"
date: 2020-01-25T18:51:15-08:00
description: "Using Kourier with KNative"
slug: ""

tags: 
  - GCP
  - knative
  - kourier
  - k8s
  - kubernetes

categories: 
  - Knative

keywords: []

hidden: false

draft: true

---
# Using Kourier with KNative
The [3Scale](https://www.3scale.net/) [Kourier](https://github.com/3scale/kourier) is an Ingress 
for [Knative](https://knative.dev). A deployment of Kourier consists of an Envoy proxy and a control
plane for it. Kourier is meant to be a lightweight replacement for the [Istio](https://istio.io/) 
ingress.  They say in the future it will provide API managemetn capabilities.

## Motivation
I was reading the release notes for [Knative 0.11.1](https://github.com/knative/serving/releases/tag/v0.11.1)
and saw this mentioned as a native knative ingress controller and knew I'd have to change all my [terraform](https://terraform.io) code for
installing Istio anyway. (Istio has moved from using [Helm](https://helm.sh/) which just did a major
change to 3.0 - to using the istioctl cli for instalation.)  This seemed a bit cleaner and easier and
likely to be more maintainable.  (For the record - I do actually like using stable tools, if I could
find them.)

## Installing & Configuring
The Kourier instructions in thier [README](https://github.com/3scale/kourier/blob/master/README.md) are
great, I just thend to do things a bit differently.  When in doubt, use thiers.

### 305-config-network ConfigMap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: config-network
  namespace: knative-serving
data:
  domainTemplate: "{{.Name}}.{{.Domain}}"
  clusteringress.class: "kourier.ingress.networking.knative.dev"
  ingress.class: "kourier.ingress.networking.knative.dev"
```
You'll note that I change my `domainTemplate` in a way that works for my application of just using the
appName and not the namespace. (I run almost every app in a unique namespace that is the same as the
app.)

Next you'll find the kourier changes.

```shell script
kubectl apply -f 305-config-network.yaml
```
### Install
```shell script
kubectl apply -f https://raw.githubusercontent.com/3scale/kourier/${kourier_version}/deploy/kourier-knative.yaml
```

### Setup a custom domain
This is just patching the knative `config-domain` ConfigMap in the [standard way](https://knative.dev/docs/serving/using-a-custom-domain/).
```shell script
kubectl patch configmap/config-domain -n knative-serving --type merge -p '{"data":{"${domain}":""}}'
```

### Setup the TLS certificate
I found the description in the docs to be a bit of a handwave, so I'm a bit more explicit here.
```shell script
kubectl create secret tls ingressgateway-certs --key ${KEY_FILE} --cert ${CERT_FILE} -n kourier-system
kubectl patch deployment 3scale-kourier-control -n kourier-system  --type json \
  -p '[{"op": "replace", "path":"/spec/template/spec/containers/0/env/0/value", "value":"kourier-system"}, {"op":"replace","path":"/spec/template/spec/containers/0/env/1/value","value":"ingressgateway-certs"}]'
```

## Conclusions
It was fairly easy, I found the folks at 3Scale to be very responsive to questions and comments.  I
really like the simplicity of it all - compared to installing Istio.  I did notice that http appeared
to remain open (I need to test this again)

I did run into some trouble installing Knative monitoring w/o Istio, I had to create the istio-system
namespace to get that to work.

## Next Steps
First off, I want to do a bit more testing, I should be ready for that tomorrow. Then I'll take a look
at [Contour](https://projectcontour.io/) another gateway. Lasty, I need to quickly decide if I want to
pick Istio with all it's complexity or risk using one of these lightweight ingress controlers.