# Enabling the IBM Operator Catalog 

The IBM Operator Catalog is an index of operators available to automate deployment and maintenance of IBM Software products into Red Hat&reg; OpenShift&reg; clusters.  Operators within this catalog have been built following Kubernetes best practices and IBM standards to provide a consistent integrated set of capabilities.

## Introduction
This chart deploys two operator catalogs for Cluster Administrators to discover and install IBM operators via the OperatorHub embedded in OpenShift. 

- IBM Operator Catalog : curated catalog of operators to deploy select [IBM Cloud Paks](https://www.ibm.com/support/knowledgecenter/en/cloudpaks) and standalone container software
- IBMCS Operators : curated catalog of operators to deploy [IBM Cloud Platform Common Services](https://www.ibm.com/support/knowledgecenter/SSHKN6/kc_welcome_cs.html)

For step by step operator installation instruction, including options, see ['Installing Operators from the OperatorHub'](https://docs.openshift.com/container-platform/4.4/operators/olm-adding-operators-to-cluster.html#olm-installing-operators-from-operatorhub_olm-adding-operators-to-a-cluster)

**Please note:** The operators are publically available, but products they install may require purchase and entitlement keys from IBM.      


## Chart Details
Deploys two custom catalogsources whose content will appear under "Custom" or "IBM Operator Catalog / IBMCS Operators" named catalog(s) depending on target cluster version.  Once created the catalogs will be updated on a regular polling frequency if connected to internet.

## Prerequisites
- HELM 3
- Kubernetes 1.17 or later
- Cluster Administrator access
- OpenShift Container Platform 4.4 or later

## SecurityContextConstraints Requirements
The Operator Lifecycle Manager (OLM), running by default, uses CatalogSources to query for available operators.  To ensure catalog functionatily, no custom SCC with priority > 0 should be installed as they may be selected incorrectly. 

## Resources Required
Minimum resources per operator catalog pod: 0.01 CPU and 0.05 GB Memory

## Pre-install Steps
* Create any user defined namespace
* (If using CLI Install) Retrieve chart from https://redhat-developer.github.io/redhat-helm-charts/

## Installing the Chart
Users installing this chart must have Cluster Administrator permissions.

To install the chart with the release name `my-release`:
```
$ helm install my-release stable/ibm-operator-catalog-enablement --namespace <your pre-created namespace> --set license=true
```
The command deploys ibm-operator-catalog-enablement on the Kubernetes cluster.

### Verifying the Chart
See the instructions (from NOTES.txt within chart) after the helm installation completes for chart verification. The instruction can also be viewed by running the command: helm status my-release --namespace <your pre-created namespace>.

### Uninstalling the Chart
To uninstall/delete the `my-release` deployment:
```
$ helm uninstall my-release --namespace <your pre-created namespace>
```  

## Configuration
The following table lists the configurable parameters of the `ibm-operator-catalog-enablement` chart and their default values.

| Parameter                       | Description                                                     | Default                                    |
| ------------------------------- | --------------------------------------------------------------- | ------------------------------------------ |
| `license`                       | Set to `true` to accept the terms of the license                | `false`                                  |

## Limitations
- This chart can only be installed once per cluster.
- The CatalogSource resources created will not show in Topology as they don't fall under workload catalog.  Future releases may show reference with regard to helm install.

## Documentation
- [Learn about IBM Cloud Paks](http://www.ibm.com/cloud/paks)
- [Learn about IBM CS Operators](https://www.ibm.com/support/knowledgecenter/SSHKN6/kc_welcome_cs.html)
