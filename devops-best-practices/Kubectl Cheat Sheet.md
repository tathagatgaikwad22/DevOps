# Kubectl Cheat Sheet

Basic Commands
kubectl version
kubectl cluster-info
kubectl config view
kubectl get nodes
kubectl get namespaces

# Context & Namespace Management

kubectl config get-contexts
kubectl config use-context <context-name>
kubectl config set-context --current --namespace=<namespace>
kubectl get ns

# Get Resources

kubectl get pods
kubectl get pods -o wide
kubectl get svc
kubectl get deploy
kubectl get all
kubectl get pods -n <namespace>

kubectl get pods -l app=nginx

# Describe Resources

kubectl describe pod <pod-name>
kubectl describe svc <service-name>
kubectl describe node <node-name>

# Create, Apply & Delete Resources

kubectl apply -f file.yaml
kubectl create -f file.yaml
kubectl delete -f file.yaml

kubectl apply -f file.yaml --dry-run=client -o yaml

# Pods & Containers

kubectl get pods
kubectl delete pod <pod-name>
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -c <container-name> -- sh

Logs

kubectl logs <pod-name>
kubectl logs <pod-name> -f
kubectl logs <pod-name> -c <container-name>
kubectl logs --previous <pod-name>

# Deployments & Rollouts

kubectl get deploy
kubectl scale deploy <deploy-name> --replicas=3
kubectl rollout status deploy <deploy-name>
kubectl rollout history deploy <deploy-name>
kubectl rollout undo deploy <deploy-name>

# Services & Networking

kubectl get svc
kubectl describe svc <service-name>
kubectl port-forward pod/<pod-name> 8080:80
kubectl port-forward svc/<service-name> 8080:80

# ConfigMaps & Secrets

kubectl get cm
kubectl get secrets
kubectl describe cm <name>
kubectl describe secret <name>

kubectl create cm app-config --from-literal=env=prod
kubectl create secret generic db-secret --from-literal=password=1234

# Node Management

kubectl get nodes
kubectl cordon <node-name>
kubectl drain <node-name>
kubectl uncordon <node-name>

# Resource Usage & Events

kubectl top nodes
kubectl top pods
kubectl get events --sort-by=.metadata.creationTimestamp

#Dangerous Commands

kubectl delete pod --all
kubectl delete all --all -n <namespace>

# Aliases & Shortcuts

alias k=kubectl
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'

# Common Flags

-n <namespace>
-o yaml
-o wide
--dry-run=client
--force
--grace-period=0

# Final Note
Kubectl mastery is about awareness, not memorization.
rization.
Always know your cluster, namespace, and roll
