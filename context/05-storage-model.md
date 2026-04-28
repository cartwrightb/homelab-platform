# Storage Model

## Storage Classes

The cluster currently uses two primary storage approaches:

### local-path

- Default k3s storage class
- Node-local storage
- Suitable for single-node persistent workloads

### nfs-client

- Backed by OMV NFS exports
- Provides shared RWX-style storage
- Used for shared media/application storage

## Current Storage Areas

Infrastructure storage configuration exists under:

`k8s/infra/storage/`

This includes:

- NFS provisioner configuration
- Static media PV/PVC definitions

## Design Intent

The current storage design balances:

- simplicity
- low operational overhead
- learning Kubernetes storage concepts
- practical media hosting requirements

## Notes

The platform is currently single-node.

Storage decisions may change later if the cluster becomes multi-node.