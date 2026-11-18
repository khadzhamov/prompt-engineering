# Prompt: Add a Kubernetes liveness probe

Act as a senior Kubernetes reliability engineer.

Context:
A Go web application named `go-demo-app` runs in a container and listens on
HTTP port 8080. Its health endpoint is `/healthz`.

Task:
Generate a Kubernetes Deployment manifest with a liveness probe.

Requirements:
- Use `apps/v1`.
- Configure 2 replicas and a container named `go-demo-app`.
- Use image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Expose container port 8080, named `http`.
- Configure an HTTP GET liveness probe against `/healthz` on port `http`.
- Set `initialDelaySeconds: 10`, `periodSeconds: 10`,
  `timeoutSeconds: 2`, `failureThreshold: 3`.
- Add consistent labels and selectors.
- Do not add a readiness or startup probe.
- Do not invent unrelated configuration.

Output:
Return only a valid Kubernetes YAML Deployment. Validate the probe structure,
port reference, API version, labels/selectors, and YAML indentation.
