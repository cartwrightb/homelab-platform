# Networking & DNS Design

## Goals

The networking and DNS design aims to:

- Provide stable internal service naming
- Enable internal TLS using FQDNs
- Support remote access via Tailscale
- Reduce dependency on hypervisor-hosted services
- Centralise IP management

The emphasis is simplicity first, segmentation later.

---

## Current State

### DNS

- Pi-hole runs inside an LXC container on PVE1.
- Internal domain: `home.lan`
- DNS records support internal service access.

### DHCP

- DHCP is currently provided by the ISP router.
- No reservations in place yet.
- Devices receive DNS configuration via router settings.

### Remote Access

- Tailscale subnet routing is operational.
- Split DNS is not yet configured.
- Internal services can be accessed via IP remotely.

---

## Current Limitations

- DNS is dependent on PVE1 being online.
- DHCP is not centrally managed.
- No DHCP reservations.
- Split DNS not yet implemented.
- No VLAN segmentation.

These constraints are accepted at this stage of platform evolution.

---

## Target State

### Dedicated DNS Host

- Move Pi-hole to a Raspberry Pi.
- Decouple DNS from Proxmox dependency.
- Improve platform resilience during hypervisor maintenance.

### DHCP Migration

- Disable DHCP on ISP router.
- Enable DHCP in Pi-hole.
- Implement reservations for:
  - Kubernetes node(s)
  - Core VMs
  - Client devices

### Internal Naming

- All services accessed via FQDN:
  - `service.home.lan`
- TLS termination handled via Traefik + cert-manager.

### Split DNS

- Configure Tailscale to forward `home.lan` queries to Pi-hole.
- Enable consistent naming on LAN and remotely.
- Remove need for IP-based access.

---

## IP Strategy

Static:
- Router
- Proxmox hosts
- Pi-hole

DHCP Reservations:
- Kubernetes nodes
- Virtual machines
- Client devices
- Smart TVs and IoT

This approach centralises IP control while maintaining stability of core infrastructure.

---

## Future Considerations

- Secondary DNS/DHCP
- Managed switch and VLAN segmentation
- OPNSense firewall
- Inter-VLAN routing policies

These are intentionally deferred to prioritise Kubernetes and platform development.

---

## Design Philosophy

The networking layer is designed to support the platform — not dominate it.

Complexity is introduced only when it provides operational or learning value.
