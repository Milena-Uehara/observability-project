# Running a web server in Golang with Kubernetes

- [Web server repository](https://github.com/Milena-Uehara/golang-app)

## Running locally with minikube
### Create local cluster
```
minikube start --driver=docker
```
### Running local stack
1. Apply the manifests in order or run the command `make`.
    1. Create the namespaces:
        ```
        kubectl apply -f 1-namespace.yaml
        ```
    2. Create the secrets:
        ```
        kubectl apply -f 2-secrets.yaml
        ```
    3. Create the database configMap:
        ```
        kubectl apply -f 3-db-configmap.yaml
        ```
    4. Create the database deployment:
        ```
        kubectl apply -f 3.1-db-deployment.yaml
        ```
    5. Create the database service:
        ```
        kubectl apply -f 3.2-db-service.yaml
        ```
    6. Create web server deployment:
        ```
        kubectl apply -f 4-app-deployment.yaml
        ```
    7. Create web server service:
        ```
        kubectl apply -f 4.1-app-service.yaml
        ```
2. Installing Datadog with Helm.
    1. Add the datadog repo:
        ```
        helm repo add datadog https://helm.datadoghq.com
        ```
    2. Update existing helm repos:
        ```
        helm repo update
        ```
    3. Add the Datadog ApiKey value as a secret:
        ```
        kubectl create secret generic datadog-secret --from-literal api-key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX -n datadog
        ```
    4. Install datadog:
        ```
        helm install datadog-agent -f 5-datadog-values.yaml datadog/datadog -n datadog
        ```
    [Original values](https://github.com/DataDog/helm-charts/blob/main/charts/datadog/values.yaml)

### Deleting local stack
1. To delete resources created with kubectl, run:
    ```
    make delete-all
    ```
2. To delete Datadog:
    ```
    helm uninstall datadog-agent -n datadog
    ```
    To delete Datadog secret, run:
    ```
    kubectl delete secrets datadog-secret -n datadog
    ```
