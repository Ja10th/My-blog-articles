---
title: "GitOps: Managing Kubernetes Deployments with Git"
datePublished: Fri Oct 06 2023 15:21:35 GMT+0000 (Coordinated Universal Time)
cuid: clner84ob00030al4594hgp0m
slug: gitops-managing-kubernetes-deployments-with-git
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696765085789/816c3a10-6ad8-4e75-b830-d5d4c4804376.png
tags: continuous-deployment, kubernetes, devops, infrastructure-as-code, gitops

---

The way deployments are managed is critical in creating a durable and scalable infrastructure in the fast-paced world of Kubernetes orchestration. GitOps has evolved as a powerful paradigm for defining and controlling the state of Kubernetes clusters by leveraging Git repositories as the ultimate source of truth. This in-depth post will go into the fundamentals of GitOps, its process, and the tools that make it possible, as well as provide real examples with code.

## Understanding GitOps

GitOps is a set of practices that revolves around utilizing Git as the primary tool for infrastructure automation and application delivery. At its core, GitOps advocates for declaring the desired state of your system in a Git repository and relying on a continuous reconciliation process to bring the actual state in line with the desired state.

### Key Principles of GitOps:

1. **Declarative Configuration:** Infrastructure and application configurations are versioned and stored in Git repositories, following a declarative approach. This means specifying what the desired outcome should be rather than prescribing the steps to get there.
    
2. **Continuous Deployment:** Changes to the Git repository trigger automated deployment processes. This ensures continuous and reliable delivery, fostering agility in responding to changing requirements.
    
3. **Automated Synchronization:** Kubernetes clusters automatically reconcile their state with the Git repository. This automated synchronization keeps the infrastructure and applications in sync with the declared configurations.
    
4. **Observability:** GitOps emphasizes visibility and observability by leveraging Git's versioning capabilities. This makes it easy to track changes, understand the history of deployments, and perform rollbacks when necessary.
    

## GitOps Workflow

Let's walk through a detailed GitOps workflow for managing Kubernetes deployments, illustrating each step with practical examples.

### Step 1: Git Repository Structure

The foundation of GitOps lies in the organization of your Git repository. Create a structure that separates applications and environments, making it clear and maintainable. For instance:

```plaintext
├── k8s
│   ├── app
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   └── namespaces
│       └── staging.yaml
└── README.md
```

In this structure, the `k8s` directory holds Kubernetes manifests for different applications and environments. The `app` directory contains deployment and service manifests, while the `namespaces` directory contains namespace configurations.

### Step 2: Flux as the GitOps Operator

Flux is a popular GitOps operator that automates the deployment process based on changes in the Git repository. It continuously monitors the repository and ensures that the declared state aligns with the actual state in the Kubernetes cluster.

#### Installation of Flux:

Install Flux in your Kubernetes cluster. We'll use Helm to make the installation process smoother:

```bash
kubectl apply -f https://raw.githubusercontent.com/fluxcd/flux/main/install/flux-helm-release/crds.yaml
helm repo add fluxcd https://charts.fluxcd.io
helm upgrade -i flux fluxcd/flux -n flux-system --wait \
--set git.url=git@github.com:your-username/your-repo \
--set git.path=k8s \
--set sync.state=secret
```

This installation process establishes a Flux instance in your Kubernetes cluster, linking it to your Git repository.

### Step 3: Define a Deployment

Let's consider a simple Nginx deployment. Create or update the Kubernetes deployment manifests in the Git repository. For example, `deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
```

This manifest specifies a basic Nginx deployment with three replicas. It is part of the `app` category within the Git repository.

### Step 4: Git Commit and Push

Commit the changes to the Git repository and push them to the remote repository. This action triggers the deployment process.

```bash
git add .
git commit -m "Update Nginx deployment"
git push origin main
```

### Step 5: Flux Reconciliation

Flux continuously monitors the Git repository for changes. Upon detecting a new commit, it pulls the changes and applies them to the Kubernetes cluster. This is a continuous reconciliation process that keeps the cluster state aligned with the desired configurations.

```bash
kubectl get deployment
```

## Advanced GitOps Concepts

### Canary Deployments with GitOps

GitOps seamlessly integrates with progressive delivery strategies like Canary Deployments. A Canary Deployment involves gradually rolling out a new version of an application to a subset of users or servers. This minimizes the risk, allowing for real-time monitoring and rapid rollback if issues arise.

To implement Canary Deployments with Flux, you can use Flagger, a progressive delivery operator that works alongside Flux.

### GitOps Toolkit

The GitOps Toolkit is a set of libraries and best practices for creating a GitOps pipeline. It extends the capabilities of Flux, providing additional tools like Kustomize for configuration management, Helm Operator for Helm chart releases, and Helm Controller for GitOps-based Helm chart management.

## Conclusion

In conclusion, GitOps provides a robust and auditable approach to managing Kubernetes deployments. By treating Git as the source of truth, teams can achieve a declarative, version-controlled, and automated deployment workflow, fostering collaboration and reliability in the Kubernetes ecosystem. As you adopt GitOps, explore additional tools and practices that align with your specific needs, and enjoy the benefits of a streamlined and scalable Kubernetes deployment process. Whether you are a seasoned Kubernetes user or just getting started, GitOps brings efficiency, reliability, and collaboration to your deployment workflows.