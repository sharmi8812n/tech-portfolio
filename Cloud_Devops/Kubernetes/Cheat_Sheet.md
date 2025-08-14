# kubectl Commands Cheat Sheet

## Cluster Information
- `kubectl cluster-info`  
  Display cluster info and master/node endpoints.

- `kubectl config view`  
  Show current kubeconfig settings.

- `kubectl get nodes`  
  List all nodes in the cluster.

---

## Working with Pods
- `kubectl get pods`  
  List all pods in the current namespace.

- `kubectl get pods -A` or `--all-namespaces`  
  List pods in all namespaces.

- `kubectl describe pod <pod-name>`  
  Show detailed info about a specific pod.

- `kubectl logs <pod-name>`  
  View logs of a pod’s main container.

- `kubectl logs <pod-name> -c <container-name>`  
  View logs of a specific container in a pod.

- `kubectl exec -it <pod-name> -- /bin/bash`  
  Open an interactive shell inside a running pod.

---

## Managing Deployments
- `kubectl get deployments`  
  List deployments in current namespace.

- `kubectl describe deployment <deployment-name>`  
  Show details of a deployment.

- `kubectl apply -f <file.yaml>`  
  Create or update resources from a YAML file.

- `kubectl delete -f <file.yaml>`  
  Delete resources defined in a YAML file.

- `kubectl rollout status deployment/<deployment-name>`  
  Check rollout status of a deployment.

- `kubectl rollout undo deployment/<deployment-name>`  
  Rollback deployment to previous version.

---

## Services and Networking
- `kubectl get services`  
  List services in the current namespace.

- `kubectl describe service <service-name>`  
  Show details about a service.

- `kubectl expose deployment <deployment-name> --type=LoadBalancer --port=80`  
  Expose a deployment as a LoadBalancer service.

---

## Namespaces
- `kubectl get namespaces`  
  List all namespaces.

- `kubectl create namespace <name>`  
  Create a new namespace.

- `kubectl config set-context --current --namespace=<namespace>`  
  Set default namespace for kubectl commands.

---

## ConfigMaps and Secrets
- `kubectl get configmaps`  
  List ConfigMaps.

- `kubectl get secrets`  
  List Secrets.

- `kubectl create configmap <name> --from-file=<file>`  
  Create a ConfigMap from a file.

---

## Scaling and Autoscaling
- `kubectl scale deployment <deployment-name> --replicas=3`  
  Scale deployment to 3 replicas.

- `kubectl autoscale deployment <deployment-name> --min=2 --max=5 --cpu-percent=80`  
  Enable autoscaling based on CPU usage.

---

## Miscellaneous
- `kubectl version`  
  Show client and server versions.

- `kubectl explain <resource>`  
  Get documentation for a Kubernetes resource.

- `kubectl get all`  
  List all resources (pods, services, deployments, etc.) in current namespace.

- `kubectl apply -k <directory>`  
  Apply resources from a Kustomize directory.

---

## Tips
- Add `-o yaml` or `-o json` to output resource details in YAML or JSON format.  
- Use `--watch` to continuously watch resource changes, e.g., `kubectl get pods --watch`.  
- Use `-n <namespace>` to specify namespace for any command.

---

# Summary

`kubectl` is the command-line tool for interacting with Kubernetes clusters. These commands cover most daily operations from inspecting resources to managing deployments and services.

