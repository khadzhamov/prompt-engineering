# Prompt: Generate a Deployment with a mounted volume

Act as an experienced Kubernetes engineer.

Context:
A Go application named `go-demo-app` runs on port 8080 and needs a writable
directory at `/var/lib/go-demo-app/data` for temporary application data.

Task:
Create a Kubernetes Deployment that mounts an ephemeral `emptyDir` volume.

Requirements:
- Use `apps/v1`, 1 replica, and the image
  `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Name the container `go-demo-app` and expose TCP port 8080.
- Define an `emptyDir` volume named `app-data`.
- Mount it read-write at `/var/lib/go-demo-app/data`.
- Ensure `volumeMounts.name` exactly matches `volumes.name`.
- Use matching application labels and selectors.
- Do not create a PVC or claim that emptyDir data survives Pod replacement.
- Do not add unrelated resources.

Output:
Return only valid Kubernetes YAML for the Deployment. Verify volume and mount
references, API version, labels/selectors, and indentation.
