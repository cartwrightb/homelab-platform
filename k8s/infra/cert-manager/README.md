# cert-manager

Installed via Helm into the `cert-manager` namespace.

## Why
Provides certificate issuance + renewal via CRDs (Issuer/ClusterIssuer/Certificate).

## Install / Upgrade

helm repo add jetstack https://charts.jetstack.io
helm repo update

helm upgrade --install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.14.5 \
  -f values.yaml

## Notes
- CRDs are installed by Helm (`installCRDs=true`).
- Do not apply `rendered-manifest.yaml` directly; it is for reference only.
