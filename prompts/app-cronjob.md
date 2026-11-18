# Prompt: Generate a Kubernetes CronJob

Act as a senior Kubernetes batch-workload engineer.

Context:
A container image for the demo application can run a maintenance command:
`/app/go-demo-app cleanup`. The task should run once every day at 02:30.

Task:
Create a Kubernetes CronJob manifest.

Requirements:
- Use `batch/v1`.
- Name it `go-demo-cleanup` in namespace `default`.
- Use schedule `30 2 * * *`.
- Set `concurrencyPolicy: Forbid`.
- Set `startingDeadlineSeconds: 300`.
- Set `successfulJobsHistoryLimit: 3` and `failedJobsHistoryLimit: 1`.
- Use image `ghcr.io/den-vasyliev/go-demo-app:latest`.
- Set `restartPolicy: OnFailure`.
- Configure the container command as `["/app/go-demo-app", "cleanup"]`.
- Set `backoffLimit: 2` in the job template.
- Do not add credentials, volumes, or invented environment variables.

Output:
Return only a complete `batch/v1` CronJob YAML. Check nesting under
spec.jobTemplate.spec.template.spec, schedule syntax, and restart policy.
Mention no prose outside the YAML.
