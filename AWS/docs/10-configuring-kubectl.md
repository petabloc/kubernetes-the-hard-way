# Configuring kubectl for Remote Access

In this lab you will generate a kubeconfig file for the `kubectl` command line utility based on the `admin` user credentials.

> Run the commands in this lab from the same directory used to generate the admin client certificates.

## The Admin Kubernetes Configuration File

Each kubeconfig requires a Kubernetes API Server to connect to. To support high availability the IP address assigned to the external load balancer fronting the Kubernetes API Servers will be used.

Generate a kubeconfig file suitable for authenticating as the `admin` user:

```
{
LOADBALANCER=$(aws elbv2 describe-load-balancers --names kubernetes-the-hard-way --query 'LoadBalancers[].LoadBalancerArn' --output text)

PUBLICADDRESS=$(aws elbv2 describe-load-balancers \
--load-balancer-arns ${LOADBALANCER} \
--output text --query 'LoadBalancers[].DNSName')

kubectl config set-cluster kubernetes-the-hard-way \
  --certificate-authority=ca.pem \
  --embed-certs=true \
  --server=https://${PUBLICADDRESS}:443

kubectl config set-credentials kubernetes-the-hard-way-admin \
  --client-certificate=admin.pem \
  --client-key=admin-key.pem

kubectl config set-context kubernetes-the-hard-way \
  --cluster=kubernetes-the-hard-way \
  --user=kubernetes-the-hard-way-admin

kubectl config use-context kubernetes-the-hard-way
}
```

## Verification

Check the version of the remote Kubernetes cluster:

```
kubectl version
```

> output

```
Client Version: v1.28.4
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.28.3
```

List the nodes in the remote Kubernetes cluster:

```
kubectl get nodes
```

> output

```
NAME           STATUS   ROLES    AGE   VERSION
ip-10-0-1-20   Ready    <none>   17m   v1.21.0
ip-10-0-1-21   Ready    <none>   17m   v1.21.0
ip-10-0-1-22   Ready    <none>   17m   v1.21.0
```

Next: [Provisioning Pod Network Routes](11-pod-network-routes.md)
