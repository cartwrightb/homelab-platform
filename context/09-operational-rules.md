# Operational Rules

## GitOps First

All persistent cluster changes should be made through GitOps wherever possible.

Avoid manual `kubectl apply` usage except for testing or emergency troubleshooting.

## Repository Structure

Follow existing repository structure and naming conventions.

Do not create duplicate patterns for the same problem.

## Simplicity

Prefer simple and understandable manifests over overly abstracted configurations.

Learning and operational clarity are more important than optimisation.

## Validation

Before major changes:

- inspect existing kustomizations
- inspect Flux reconciliation flow
- verify namespace usage
- verify ingress/TLS assumptions
- verify storage requirements

## Secrets

Do not commit:

- passwords
- API tokens
- private keys
- kubeconfig files

## Agent Behaviour

Agents should:

- explain proposed changes before applying them
- avoid inventing live cluster state
- avoid restructuring the repository unnecessarily
- prefer small reviewable changes
- preserve existing operational patterns

