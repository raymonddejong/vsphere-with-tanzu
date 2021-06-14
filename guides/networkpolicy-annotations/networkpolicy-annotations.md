# NetworkPolicy Annotations

by Raymond de Jong [@dejongraymond](https://twitter.com/dejongraymond) / [LinkedIn](https://linkedin.com/in/dejongraymond) / [Blog](https://www.cloudxtreme.com)

_**This disclaimer informs readers that the views, thoughts, and opinions expressed in this series of posts belong solely to the author, and not necessarily to the author’s employer, organization, committee or other group or individual.**_

## Introduction
This guide is to demonstrate the usage of Kubernetes annotations on Network Policy objects. 

Network Policy annotations will trigger NSX Container Plugin (NCP) whether to log the traffic matching the DFW rules created for this policy. This allows users to enable DFW logging at the NetworkPolicy level. 

It is possible to enable logging for all DFW rules, only the deny rules or off.  Note that if a network policy does not have an annotation logging on the DFW rules will be off.

User can add an annotation for traffic logging option in the network policy's metadata, as shown in the below examples.

### Enable logging for all DFW rules (both DENY and ALLOW):
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: nginx-network-policy
  annotations:
    ncp/log_traffic: "ALL"
......
```
### Enable logging only for DENY rules
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy
  annotations:
    ncp/log_traffic: "DENY"
......
```
### Do not enable logging for any rule
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy
  annotations:
    ncp/log_traffic: "OFF"
......
```

## Usage in vSphere with Tanzu on NSX-T
In a vSphere with Tanzu on NSX-T environment there is a namespaces configured call 'Marketing'. Two NGINX vSphere-Pods are deployed using a deployment. This example is to show 

Apply the Network Policy

```
kubectl apply -f network-policy-logging-all.yaml
```
Describe the Network Policy
kubectl describe network-policy



