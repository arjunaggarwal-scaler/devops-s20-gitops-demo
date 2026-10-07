# devops-s20-gitops-demo

GitOps demo for **Session 20 – Monitoring, Observability & GitOps** (Arjun Aggarwal, 24BCS10109).

Argo CD watches the `app/` folder of this repository and keeps the `session20` namespace of my local
kind cluster identical to it (auto-sync, prune and self-heal enabled).

```text
Developer --git push--> GitHub (this repo, desired state) <--polls-- Argo CD --applies--> Kubernetes (actual state)
```

| Path | What | Applied by |
|---|---|---|
| `app/namespace.yaml` | `session20` namespace | Argo CD (from Git) |
| `app/deployment.yaml` | `session20-mini` nginx Deployment | Argo CD (from Git) |
| `app/service.yaml` | ClusterIP Service | Argo CD (from Git) |
| `argocd/application.yaml` | Argo CD `Application` pointing at `app/` | me, once, with `kubectl apply` |

Every change to the running application is made by committing here – see the commit history for the
scale-up, image bump, prune and `git revert` rollback used in the demo.
