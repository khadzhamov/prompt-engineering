# Prompt: Generate a Kubernetes Job

Act as a senior Kubernetes engineer specializing in batch workloads.

Context:
We need to run a one-time database-independent maintenance task using the
Go demo application's cleanup command.

Task:
Create a Kubernetes Job manifest.

Requirements:
- Use `batch/v1`.
- Name the Job `go-demo-cleanup-once` in namespace `default`.
- Use image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Set container name to `cleanup`.
- Set command to `["/app/go-demo-app", "cleanup"]`.
- Set `restartPolicy: Never`.
- Set `backoffLimit: 2`.
- Set `ttlSecondsAfterFinished: 3600`.
- Use appropriate labels.
- Do not create a CronJob or Deployment.
- Do not invent environment variables or secrets.

Output:
Return only a valid Kubernetes YAML Job. Verify the batch API version, pod
template structure, restart policy, and field placement.
