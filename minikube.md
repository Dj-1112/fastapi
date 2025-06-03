#### Hands-On with Basic Kubernetes Commands

-   **Starting Minikube**
    -   Ensure Minikube is running:
        ```bash
        minikube start
        ```
-   **kubectl Commands**
    -   Get cluster information:
        ```bash
        kubectl cluster-info
        ```
    -   List nodes:
        ```bash
        kubectl get nodes
        ```
    -   List namespaces:
        ```bash
        kubectl get namespaces
        ```
    -   Access the Kubernetes dashboard
        ```bash
        minikube dashboard
        ```

#### Push your Image to Docker Hub

-   Tag `my-fast-api:1.0` image to `<docker-hub-username>/my-fast-api:1.0`

    ```bash
    docker tag my-fastapi-app:1.0 jayanth00003/my-fastapi-app:1.0
    ```

-   Log in to Docker Hub
    ```bash
    docker login
    ```

-   Push `my-fast-api:1.0` image to your Docker Hub account
    ```bash
    docker push jayanth00003/my-fastapi-app:1.0
    ```

#### Deploying Applications in Kubernetes

-   **Creating a Deployment**
    -   Create a simple fastapi deployment:
        ```bash
        kubectl create deployment fastapi --image=jayanth00003/my-fastapi-app:1.0
        ```
    -   View the deployment and pods:
        ```bash
        kubectl get deployments
        kubectl get pods
        ```
-   **Exposing the Deployment**

    -   Expose fastapi deployment as a service:
        ```bash
        kubectl expose deployment fastapi --type=NodePort --port=8000
        ```
    -   Get the service details:
        ```bash
        kubectl get services
        ```
    -   Access the fastapi service using Minikube:

        ```bash
        minikube service fastapi
        ```
    -   Forward the port:
        ```bash
        kubectl port-forward service/fastapi 7080:8000
        ```

#### Scaling and Updating Applications

-   **Scaling the Deployment**
    -   Scale fastapi deployment to 3 replicas:
        ```bash
        kubectl scale deployment fastapi --replicas=3
        ```
    -   Verify the scaling:
        ```bash
        kubectl get pods
        ```
- **Updating the Deployment**
  - Update the fastapi image version:
    ```bash
    kubectl set image deployment/fastapi my-fastapi-app=jayanth00003/my-fastapi-app:2.0
    ```
  - Verify the update:
    ```bash
    kubectl rollout status deployment/fastapi
    ```
  - Check the pod versions:
    ```bash
    kubectl get pods -o wide
    ```
  - Check logs from any one pod:
    ```bash
    kubectl logs deployment/fastapi
    ```
  - Check logs from all the pods:
    ```bash
    kubectl logs deployment/fastapi --all-pods=true
    ```
- **Manage your cluster**
  - Pause Kubernetes:
    ```bash
    minikube pause
    ```
  - Unpause a paused instance:
    ```bash
    minikube unpause
    ```
  - Halt the cluster:
    ```bash
    minikube stop
    ```
  - Start the cluster:
    ```bash
    minikube start
    ```
  - Delete all of the minikube clusters:
    ```bash
    minikube delete --all
    ```
