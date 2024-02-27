---
title: "Curl Tests"
date: 2024-02-27T10:23:57-07:00
draft: true
---
# Dynatrace cURL Image Tests Commands

Testing between Dynatrace Operator Namespace the K8s API Server.
We should expect to see a 403 error at the end of the curl pod deployment as we did not specify authentication credentials with which to ping the K8s API, so we received a 403 unauthenticated.

```bash
K8SHOST=$(kubectl exec -n dynatrace deploy/dynatrace-operator -it -- sh -c 'env | grep KUBERNETES_SERVICE_HOST' | awk -F "=" '/KUBERNETES_SERVICE_HOST/{print $2}')
echo $K8SHOST
echo $K8SHOST/api/v1/nodes
echo "\n\nRunning cURL test against $K8SHOST/api/v1/nodes \n\n"
kubectl -n dynatrace run curl --image=curlimages/curl --restart=Never -it --rm -- $K8SHOST/api/v1/nodes --connect-timeout 10 -kv
```

Testing between the DT-Operator and the DT API URL

```bash
read -p "What is the name of your Dynakube custom resource? By default, its' dynakube': " answer
echo "\nSearching for Dynakube CR's matching: $answer"
APIURL=$(kubectl get dynakube $answer -n dynatrace -o=jsonpath='{.spec.apiUrl}')
echo "\n\nGrabbed the API URL! We are connected to: $APIURL\n\n"
kubectl -n dynatrace run curl --image=curlimages/curl --restart=Never -it --rm -- $APIURL/rest/health --connect-timeout 10 -k
```

```bash
kubectl get dynakube [Dybakube-Resource-name] -n dynatrace -o=jsonpath='{.spec.apiUrl}'
kubectl -n dynatrace run curl --image=curlimages/curl --restart=Never -it --rm -- $APIURL/rest/health --connect-timeout 10 -k
```
 

 Successful examples

 ```bash
 kubectl -n dynatrace run curl --image=curlimages/curl --restart=Never -it --rm -- https://10.0.0.1:443/api/v1/nodes --connect-timeout 10 -k
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "Unauthorized",
  "reason": "Unauthorized",
  "code": 401
}pod "curl" deleted
 ```

 ```bash
kubectl -n dynatrace run curl --image=curlimages/curl --restart=Never -it --rm -- https://myx35151.dev.dynatracelabs.com/rest/health --connect-timeout 10 -k
If you don't see a command prompt, try pressing enter.
warning: couldn't attach to pod/curl, falling back to streaming logs: unable to upgrade connection: container curl not found in pod curl_dynatrace
RUNNING
pod "curl" deleted
 ```
