# NFS Subdir External Provisioner

This component provides **dynamic RWX PersistentVolumes**
backed by the OMV NFS export `/export/k8s-appdata`.

## Why this exists
- Avoid manual PV creation for app configs
- Support RWX access for multiple pods
- Keep app config storage separate from media storage

## Namespace
infra

## StorageClass
- Name: nfs-client
- Default: false
- ReclaimPolicy: Retain
- archiveOnDelete: true

## Install / Upgrade

helm upgrade --install nfs-provisioner \
  nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
  --namespace infra \
  -f values.yaml

## Notes
- OMV requires NFSv3
- This chart is the source of truth — do not apply rendered YAML
