# Prompt: Generate a multi-container Pod

Act as a senior Kubernetes engineer.

Context:
Create a demonstration Pod with two containers: a Go application and a
sidecar that periodically reads the application's shared log file.

Task:
Generate a Kubernetes Pod manifest.

Requirements:
- Use `v1` and name the Pod `go-demo-multicontainer`.
- Container 1: name `app`, image
  `ghcr.io/den-vasyliev/go-demo-app:latest`, container port 8080.
- Container 2: name `log-reader`, image `busybox:1.36`.
- The sidecar should run `sh -c 'while true; do cat /var/log/app/app.log 2>/dev/null; sleep 30; done'`.
- Define one `emptyDir` volume named `shared-logs`.
- Mount it in both containers at `/var/log/app`.
- Set `restartPolicy: Always`.
- Add a clear label.
- Do not claim that the application writes to this path unless configured to do so.
- Do not add Service, Deployment, or other resources.

Output:
Return only valid Pod YAML. Validate container list structure and ensure both
volumeMounts reference the declared volume.
