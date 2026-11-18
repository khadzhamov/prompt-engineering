# Prompt: Add a Kubernetes readiness probe

Act as a senior Kubernetes platform engineer.

Context:
The `go-demo-app` Go service listens on HTTP port 8080. It exposes `/ready` to
indicate whether it can receive traffic.

Task:
Create a Kubernetes Deployment with a readiness probe.

Requirements:
- Use `apps/v1` and 2 replicas.
- Use image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Name the container `go-demo-app`; expose port 8080 as `http`.
- Configure an HTTP GET readiness probe for path `/ready` on port `http`.
- Set `initialDelaySeconds: 5`, `periodSeconds: 5`,
  `timeoutSeconds: 2`, and `failureThreshold: 3`.
- Include matching labels and selectors.
- Do not configure a liveness probe.
- Do not add resources, volumes, or environment variables.

Output:
Return only the complete YAML Deployment. Check that the probe is under the
container specification and that its port matches the declared container port.
