# skupper-demo

Tested versions:


Red Hat OpenShift 4.10, 4.11, 4.12 and 4.13
Advanced Cluster Management for Kubernetes 2.7.1
Gitops Operator 1.8.3
Red Hat Interconnect 1.1

## 1st Step Install

git clone https://github.com/ignaciolago/skupper-demo.git

cd skupper-demo/

oc apply -k /skupper-demo/bootstrap/base 00-argocd

oc apply -k /skupper-demo/bootstrap/base/01-applicationset-acm/

oc apply -k bootstrap/base/02-applicationset-acm-integration/

oc apply -k bootstrap/base/03-skupper/

## 2nd Step Install Skupper and Expose DeploymentConfig

### Cluster 1:
 oc login --token=sha256~6bD7qga3s8n1V3vloycwgEMrfUzVjXfBuWaiK5sPrdc --server=https://api.cluster-szcpr.szcpr.sandbox338.opentlc.com:6443\n


skupper init --enable-console --enable-flow-collector


skupper token create $HOME/secret.yaml


### Cluster 2:
oc login --token=sha256~xQeRHQ7pWcU0qd22ExO-gPLTEbSboPShvOOnGOpuIao --server=https://api.cluster-tdqgj.tdqgj.sandbox313.opentlc.com:6443\n


skupper init --enable-console --enable-flow-collector


skupper link create $HOME/secret.yaml


skupper token create $HOME/secret.yaml


### Cluster 1:
 oc login --token=sha256~6bD7qga3s8n1V3vloycwgEMrfUzVjXfBuWaiK5sPrdc --server=https://api.cluster-szcpr.szcpr.sandbox338.opentlc.com:6443\n


skupper link create $HOME/secret.yaml


skupper expose deploymentconfig boards


