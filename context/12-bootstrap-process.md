# Bootstrap Process

## Current Bootstrap Sequence

1. Create Ubuntu VM in Proxmox
2. Install k3s
3. Install Flux bootstrap
4. Install cert-manager manually
5. Install NFS provisioner manually
6. Flux reconciles infra/media/ops
7. Configure Pi-hole DNS entries
8. Import internal CA into client devices

## Current Manual Dependencies

The following are currently not GitOps-managed:

- cert-manager installation
- NFS provisioner installation
- Pi-hole DNS records
- Client CA trust import

## Future Goal

Eventually move as much bootstrap as practical into GitOps.