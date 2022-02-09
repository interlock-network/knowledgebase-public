Gitlab is a self-hosted cloud frontend for git version control system.

Historically, we used Gitlab because Github did not offer free private repos and had limited support for CI.
Since 2020, github has closed the gap on many of Gitlab's main feature advantages around CI, Project Management
and container registry.

Still, some gaps exist, which is why we still use Gitlab. Specifically, Github is lacking in [GitOps](../what/gitops.md).
For that, we use Gitlab to mirror our Github repositories, execute piplines, and orchestrate instances in
kubernetes. Gitlab's built in orchestration features include:

- Incident alerting and monitoring
- Instance scaling and management
- Automated management and rotation of SSL certs
- Automated scaffolding of kubernetes instances including routing and metrics (similar to Google https://skaffold.dev/)
- Uptime monitoring
- Response escalation
- Real-time package deployment tracking (which instance has what version package image running)
- Deployment rollout options (All at once, 10% at a time, manual, etc.)
- Package container registry (which is cheaper than Github's storage costs/limits)

By combining GitLab, Kubernetes, and GitOps, it results in a robust infrastructure:

- GitLab as the GitOps operator.
- Kubernetes as the automation and convergence system.
- GitLab CI/CD as the Continuous Deployment engine.
