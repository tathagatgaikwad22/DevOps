# Rolling Update Explained

## What is Rolling Update?  
Rolling Update is a deployment strategy where newer application versions are released gradually by replacing existing running instances (pods/servers) in small batches instead of updating everything at once. This ensures the application remains available throughout the deployment process.

## Why Rolling Update is Important?
- Prevents full application downtime  
- Reduces deployment risk  
- Allows real-time verification of new release  
- Issues impact only a subset of traffic, not entire production  
- Very easy to rollback if needed  
- Works seamlessly in Kubernetes and cloud-native environments

## How Rolling Update Works (Example)
If you have 10 pods running version `v1`, a rolling update will replace 1 or 2 pods at a time with version `v2`.

- Old pods get terminated gradually  
- New pods start serving traffic  
- Once verified healthy, the next batch replaces the next set of pods  
- Continues until 100% rollout completes

## Where It's Used?
- Kubernetes Rolling Deployments (maxSurge / maxUnavailable)  
- ECS Rolling Updates  
- Blue/Green hybrid variations  
- Modern CI/CD Continuous Delivery systems

## Key Benefits

| Benefit | Description |
|---------|-------------|
| Zero/Minimal Downtime | Users do not face outage during deployment |
| Safer Releases | Small batch updates reduce blast radius |
| Faster Rollback | Easy to revert to older stable version |
| Progressive Delivery Ready | Base strategy for advanced controlled rollout |

## Conclusion
Rolling Update is one of the core deployment patterns in modern DevOps. It provides safe, gradual, and controlled production release with no major downtime impact to end users. It is widely used in Kubernetes, cloud-native CI/CD, SRE, and production-grade systems.

---

### Tags  
`#DevOps` `#Kubernetes` `#RollingUpdate` `#DeploymentStrategies` `#SRE` `#CloudNative` `#CICD` `#DevOpsLearning` `#90DaysOfDevOps`
