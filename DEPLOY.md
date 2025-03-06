# Getting Started with the Turbonomic Secure Connect Operator

## Installing the Turbonomic Secure Connect Operator without Operator Lifecycle Manager (OLM)

```
export namespace=turbonomic
kubectl create ns $namespace
curl -L https://raw.githubusercontent.com/IBM/t8c-client-operator/refs/heads/main/deploy/operator_bundle.yaml -o operator_bundle.yaml
sed "s/__NAMESPACE__/${namespace}/g"  operator_bundle.yaml | kubectl apply -n $namespace -f -
```

## Creating Turbonomic Secure Connect Deployment
Create or modify the Turbonomic Secure Connect custom resource, to deploy an instance of Turbonomic Secure Connect within the namespace.

```
export version=8.15.3
curl -L https://raw.githubusercontent.com/IBM/t8c-client-operator/refs/heads/main/deploy/turbonomicclient.yaml -o turbonomicclient.yaml
sed "s/__VERSION__/${version}/g"  turbonomicclient.yaml  | kubectl apply -n $namespace -f -
```


## auto-upgrade of the probes
By deploying the version-manager yaml file probes/components on client side will upgrade once server upgrades.

```
kubectl apply -f https://raw.githubusercontent.com/IBM/t8c-client-operator/refs/heads/main/deploy/versionmanager.yaml -n $namespace
```
