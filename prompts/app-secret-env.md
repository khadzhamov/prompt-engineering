# Prompt: Inject Secret values as environment variables

Act as a Kubernetes security-focused platform engineer.

Context:
A Go web application needs a database username and password at runtime. Values
must be supplied by a Kubernetes Secret rather than embedded in the Pod spec.

Task:
Create a Secret and a Deployment in one multi-document YAML file.

Requirements:
- Use `v1` for the Secret and `apps/v1` for the Deployment.
- Secret name: `go-demo-db-credentials`, namespace: `default`.
- Use `stringData` keys `DB_USERNAME` and `DB_PASSWORD` with clearly marked
  non-production placeholders (for example, `CHANGE_ME_USERNAME` and
  `CHANGE_ME_PASSWORD`). Do not use real credentials.
- Deployment name: `go-demo-app`, 2 replicas.
- Use image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Container name: `go-demo-app`; port 8080.
- Populate environment variables `DB_USERNAME` and `DB_PASSWORD` using
  `secretKeyRef` references to the matching Secret keys.
- Use consistent labels and selectors.
- Do not expose Secret values in plain environment `value` fields.
- Add a YAML comment warning that placeholders must be replaced and Secrets
  should be protected with RBAC and encryption at rest.

Output:
Return only valid multi-document Kubernetes YAML. Validate Secret key names,
secretKeyRef names, resource nesting, and YAML syntax.
