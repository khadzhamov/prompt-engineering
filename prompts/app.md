# Prompt: Generate a basic Kubernetes application

Act as a senior Kubernetes platform engineer.

Context:
We are preparing Kubernetes manifests for a small Go web application used in a
learning/demo environment. The application listens on TCP port 8080 and exposes
HTTP traffic.

Task:
Create a Kubernetes Deployment and a ClusterIP Service in one multi-document
YAML file.

Requirements:
- Use `apps/v1` for the Deployment and `v1` for the Service.
- Name the application `go-demo-app` and use the namespace `default`.
- Configure 2 replicas.
- Use the container image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Set the container port to 8080 and name it `http`.
- Use matching, recommended labels and selectors.
- Set `imagePullPolicy: IfNotPresent`.
- Do not add an Ingress, Secret, PVC, or external dependency.
- Do not invent environment variables.

Output:
Return only complete Kubernetes YAML, with `---` separating resources.
Before returning it, check API versions, selector/label consistency, indentation,
and required fields. Do not include explanatory prose or Markdown fences.
