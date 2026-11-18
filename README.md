# Kubernetes Prompt Engineering Portfolio

A portfolio of English-language prompts and corresponding Kubernetes YAML examples.
The prompts are designed to generate and review common Kubernetes workload
configurations for a Go demo application.

> **Important:** These manifests are learning examples. The container image and
> application endpoints/commands are assumptions specified in the prompts.
> Confirm that the image exists and supports the stated ports, health endpoints,
> filesystem paths, and commands before deploying. No Docker image build or
> Kubernetes cluster deployment is required for this assignment.

## Repository structure

```text
.
├── README.md
├── prompts/   # English prompts used to generate each manifest
└── yaml/      # Resulting Kubernetes YAML manifests
```

## Prompt portfolio

| NAME | PROMPT | DESCRIPTION | EXAMPLE |
|---|---|---|---|
| [`app`](prompts/app.md) | [Prompt](prompts/app.md) | Creates a basic Deployment and internal ClusterIP Service for the Go demo application. | [ `yaml/app.yaml` ](yaml/app.yaml) |
| [`app-livenessProbe`](prompts/app-livenessProbe.md) | [Prompt](prompts/app-livenessProbe.md) | Adds an HTTP liveness probe so Kubernetes can restart an unhealthy container. | [ `yaml/app-livenessProbe.yaml` ](yaml/app-livenessProbe.yaml) |
| [`app-readinessProbe`](prompts/app-readinessProbe.md) | [Prompt](prompts/app-readinessProbe.md) | Adds an HTTP readiness probe so traffic is sent only to ready Pods. | [ `yaml/app-readinessProbe.yaml` ](yaml/app-readinessProbe.yaml) |
| [`app-volumeMounts`](prompts/app-volumeMounts.md) | [Prompt](prompts/app-volumeMounts.md) | Mounts an ephemeral emptyDir volume into the application container. | [ `yaml/app-volumeMounts.yaml` ](yaml/app-volumeMounts.yaml) |
| [`app-cronjob`](prompts/app-cronjob.md) | [Prompt](prompts/app-cronjob.md) | Schedules a recurring cleanup task every day at 02:30. | [ `yaml/app-cronjob.yaml` ](yaml/app-cronjob.yaml) |
| [`app-job`](prompts/app-job.md) | [Prompt](prompts/app-job.md) | Runs a one-time cleanup task with retry and TTL settings. | [ `yaml/app-job.yaml` ](yaml/app-job.yaml) |
| [`app-multicontainer`](prompts/app-multicontainer.md) | [Prompt](prompts/app-multicontainer.md) | Demonstrates a Pod with an application container and a log-reader sidecar sharing a volume. | [ `yaml/app-multicontainer.yaml` ](yaml/app-multicontainer.yaml) |
| [`app-resources`](prompts/app-resources.md) | [Prompt](prompts/app-resources.md) | Defines CPU and memory requests and limits for predictable resource scheduling. | [ `yaml/app-resources.yaml` ](yaml/app-resources.yaml) |
| [`app-secret-env`](prompts/app-secret-env.md) | [Prompt](prompts/app-secret-env.md) | Creates a Kubernetes Secret and injects its keys into a Deployment as environment variables. | [ `yaml/app-secret-env.yaml` ](yaml/app-secret-env.yaml) |

## Prompt engineering approach

Each prompt uses a structured instruction pattern:

1. **Role** — assigns the model a relevant role, such as a Kubernetes platform engineer.
2. **Context** — describes the application and the operational scenario.
3. **Task** — states exactly which Kubernetes resource must be generated.
4. **Constraints** — specifies API versions, names, ports, replicas, probes,
   resource values, and restrictions to avoid invented configuration.
5. **Output format** — requires complete YAML and, where relevant, separates
   multiple resources with `---`.
6. **Self-check** — asks the model to verify API versions, field placement,
   selectors, references, and YAML structure before responding.

This structure applies core prompt-engineering practices: clear instructions,
relevant context, explicit constraints, task decomposition, and a defined
output format.

## Reviewing the manifests

The YAML files can be checked locally without deploying them:

```bash
# If yq is installed:
for file in yaml/*.yaml; do
  echo "Checking $file"
  yq eval '.' "$file" >/dev/null || exit 1
done
```

For Kubernetes schema validation, use a validator such as kubeconform:

```bash
kubeconform -strict -summary yaml/
```

Schema validation does not prove that the referenced image, HTTP endpoints,
or application commands actually exist; those are application-specific
assumptions and must be confirmed separately.

## kubectl-ai / model-assisted workflow

The prompts in `prompts/` are intended to be used with an AI assistant such as
Google Cloud's `kubectl-ai` or another compatible LLM tool. The YAML files in
`yaml/` are the reviewed example outputs included in this portfolio.

Do not expose API keys in Git, README files, shell history, screenshots, or
prompt examples. Use environment variables or a secret manager for credentials.

## Optional: Ingress and Gateway API

The optional Gateway API exercise is separate from the nine required examples.
Ingress combines host/path routing rules in one resource, while Gateway API
separates infrastructure entry points (`Gateway`) from application routing
(`HTTPRoute`). This allows a platform team to manage shared Gateway resources
while application teams own routes, subject to the Gateway's attachment policy.

Useful references:
- [Kubernetes Gateway API](https://gateway-api.sigs.k8s.io/)
- [Gateway API: migrating from Ingress NGINX](https://gateway-api.sigs.k8s.io/guides/getting-started/migrating-from-ingress-nginx/)
- [Google Cloud kubectl-ai](https://github.com/GoogleCloudPlatform/kubectl-ai)
- [Google Prompt Engineering whitepaper](https://www.kaggle.com/whitepaper-prompt-engineering)

## Assignment scope

This repository contains the nine requested prompts and YAML examples. It does
not include a Docker image, and it does not require applying resources to a
Kubernetes cluster.
