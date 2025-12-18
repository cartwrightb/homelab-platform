- Why did I split media vs configs?
- What protocols are used (NFS vs SMB)?
- The configs are intentionally not user-browsable?

## Media share (content only)

This is your big, boring, dumb storage.
NFS export: media
SMB share: yes (for browsing / managing files)
Contents:
media/
  ├── incomplete-downloads
  ├── downloads
  ├── tv
  ├── movies
  └── books

This share:
Is safe to browse over SMB
Can be mounted by multiple systems
Contains no secrets
Can be blown away and rebuilt without breaking Kubernetes

## Configs share (Kubernetes-owned data)

This is private platform data.
NFS export: k8s-configs (or similar)
SMB share: ❌ no
Contents (initially):

k8s-configs/
  ├── appdata/
  ├── databases/    (later)
  └── backups/      (later)

This share:
Is mounted only by Kubernetes
Never exposed to SMB
Holds:
app configs
DB data
secrets-at-rest (as much as possible)
Can be backed up separately
Makes future security decisions much easier

## Why this is the right trade-off

You get:
Simplicity now (Option A)
Clean separation of concerns
No accidental leakage of configs over SMB
Easy future evolution (databases, backups, operators)
And importantly:
Nothing you do later will force you to redo this.
That’s the real win.
One tiny but important detail (don’t skip this)
On the configs NFS export:
Use restrictive permissions
Make sure only the K3s node(s) can mount it
Avoid mounting it on your desktop “just to look”
Treat it like internal storage.

Purpose:

## “How data is handled, and why”
Just make sure it answers:

where media lives
where configs live
why they’re separated
what protocols are used
what isn’t handled yet (e.g. backups “later”)