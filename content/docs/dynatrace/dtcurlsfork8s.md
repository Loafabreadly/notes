# Dynatrace Shell Tool for Kubernetes

## Overview:
A tool to perform common Dynatrace Kubernetes troubleshooting steps via cURL Pods

 Usecases include:
- Validating the health of the Dynatrace Tenant/Environment from the Dynatrace namespace
  - This is done via API call to the Dynatrace Tenant/Environment at the `/rest/health` endpoint
- Validating the Dynatrace namespace's ability to communicate with the Kubernetes_Service_Host API Endpoint
  - This is done via cURL to the `KUBERNETES_SERVICE_HOST` IP addr from the Dynatrace namespace

## Usage

The script can be executed one of two ways:
1. Just exeucting it and following the prompts `./dtcurlsfork8s`
2. Executing it and supplying the dynakube-cr name `./dtcurlsfork8s <dynakube-cr>` (For example `./dtcurlsfork8s snurka-gke-k8s`)

![example-img](dtcurlsfork8s-example.png)
