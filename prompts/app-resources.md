# Prompt: Configure Kubernetes CPU and memory resources

Act as a Kubernetes performance and reliability engineer.

Context:
A Go web application runs in a Kubernetes Deployment and listens on port 8080.

Task:
Create a Deployment manifest with explicit resource requests and limits.

Requirements:
- Use `apps/v1`, 2 replicas, and image
  `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Container name: `go-demo-app`; container port: 8080.
- Set CPU request to `100m` and memory request to `128Mi`.
- Set CPU limit to `500m` and memory limit to `256Mi`.
- Use matching labels and selectors.
- Use valid Kubernetes quantity syntax.
- Do not add HPA or make claims about measured application consumption.
- Do not add unrelated probes, volumes, or environment variables.

Output:
Return only valid Deployment YAML. Check that resources.requests and
resources.limits are nested under the container and that requests do not exceed
the corresponding limits.
