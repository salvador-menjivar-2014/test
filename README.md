# Prueba Técnica DevOps - Demo API por Salvador Menjivar

Este repositorio contiene la solución completa para la prueba técnica de DevOps. La solución incluye la aplicación Django, su contenedorización con Docker, un pipeline de CI/CD seguro con GitHub Actions y manifiestos para su despliegue en un entorno de Kubernetes.

## Arquitectura de la Solución

El siguiente diagrama ilustra el flujo de trabajo de DevSecOps implementado, desde el desarrollo hasta el despliegue.

```mermaid
graph TD
    A[👨‍💻 Desarrollador] -- git push --> B[🐱 GitHub];
    B --> C{🤖 GitHub Actions};
    C -- Dispara Workflow --> D[🧪 Job: Test];
    D -- Pasa --> E[🏗️ Job: Build & Push];
    E -- Imagen OK --> F[🛡️ Job: Scan];
    E -- Publica Imagen --> G[🐳 Docker Hub];
    F -- Pasa --> H{✅ Pipeline Exitoso};

    subgraph Kubernetes Cluster (Minikube)
        I[🌐 Service (LoadBalancer)] --> J[📱 Pod 1];
        I --> K[📱 Pod 2];
        J -- Conecta a --> L[🗄️ Pod BD];
        K -- Conecta a --> L;
    end

    G -- k8s pull image --> J;
    G -- k8s pull image --> K;
