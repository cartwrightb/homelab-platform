# Storage Design

## Overview

Storage is intentionally separated into two distinct concerns:

1.  Media storage (content)
2.  Kubernetes configuration and stateful data

This separation reduces risk, simplifies future security decisions, and
allows independent lifecycle management.

------------------------------------------------------------------------

## Media Share (Content Only)

Purpose: Large, user-browsable content storage.

Protocol: - NFS export for Kubernetes - SMB share for desktop browsing

Structure:

media/ 
├── incomplete-downloads 
├── downloads 
├── tv 
├── movies 
└──

Characteristics:

-   Safe to browse over SMB
-   No sensitive configuration data
-   Mounted by multiple systems
-   Can be rebuilt without affecting Kubernetes platform integrity

This share is intentionally "dumb storage".

------------------------------------------------------------------------

## Kubernetes Configs Share (Platform Data)

Purpose: Private stateful platform storage.

Protocol: - NFS export only - Not exposed via SMB

Structure (evolving):

k8s-configs/ ├── appdata/ ├── databases/ └── backups/

Characteristics:

-   Mounted exclusively by Kubernetes nodes
-   Not user-browsable
-   Contains application configuration and state
-   Designed for future backup strategy separation
-   Restrictive permissions applied at export level

This share represents internal platform state.

------------------------------------------------------------------------

## Why Separate Media and Configs?

Separation provides:

-   Reduced risk of accidental data exposure
-   Clear boundary between user content and platform state
-   Simpler future migration toward database operators or object storage
-   Easier backup policy evolution
-   Reduced blast radius during storage changes

This design avoids future refactoring as the platform grows.

------------------------------------------------------------------------

## Security Considerations

-   Config share is not mounted on desktop systems
-   NFS export is restricted to k3s node(s)
-   SMB is disabled for configuration storage
-   Permissions are intentionally restrictive

------------------------------------------------------------------------

## Future Improvements

-   Automated backup strategy
-   Snapshot-based recovery validation
-   Potential migration toward CSI-backed storage
-   Separate database persistence strategy
