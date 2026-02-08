TLS (Internal CA) with cert-manager
==================================

This cluster uses cert-manager to issue internal TLS certificates for services
exposed via Traefik Ingress on the `.home.lan` domain.

GOAL
----

- Provide HTTPS for internal services (Jellyfin, *arr apps, etc.)
- Use an internal Certificate Authority (CA) first (no Let's Encrypt yet)
- Use a wildcard certificate for `*.home.lan`
- Keep everything declarative and GitOps-ready

--------------------------------------------------

RESPONSIBILITIES (MENTAL MODEL)
-------------------------------

- cert-manager
  Issues certificates and stores them as Kubernetes Secrets.

- Internal CA
  Signs certificates. Clients must trust this CA.

- Traefik
  Terminates TLS using the Secret referenced by each Ingress.

- Ingress
  Declares host routing and which TLS Secret to use.

--------------------------------------------------

WHAT EXISTS IN THE CLUSTER
-------------------------

ClusterIssuers
~~~~~~~~~~~~~~

- homelan-selfsigned
  * Bootstrap issuer only
  * Used once to mint the root CA certificate

- homelan-ca
  * CA-backed issuer
  * Signs all leaf certificates using the root CA keypair

Check:
  kubectl get clusterissuer

--------------------------------------------------

Root CA (cert-manager namespace)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Certificate: cert-manager/homelan-root-ca
- Secret:      cert-manager/homelan-root-ca
- Type:        kubernetes.io/tls

This Secret contains:
- Root CA private key
- Root CA certificate

This is the trust anchor for the entire cluster.

Check:
  kubectl -n cert-manager get certificate,secret | grep homelan

--------------------------------------------------

Wildcard leaf certificate (media namespace)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Certificate: media/wildcard-home-lan
- Secret:      media/wildcard-home-lan-tls
- Type:        kubernetes.io/tls

SANs:
- *.home.lan
- home.lan

Check:
  kubectl -n media get certificate,secret | grep wildcard

--------------------------------------------------

INGRESS TLS WIRING
------------------

Ingress YAML files live in Git under:

  k8s/infra/ingress/

However, the Kubernetes namespace is defined in the YAML itself
(typically: metadata.namespace: media).

Each Ingress enables TLS like this:

  spec:
    tls:
    - hosts:
      - <app>.home.lan
      secretName: wildcard-home-lan-tls

Traefik reads the Secret and serves HTTPS for that host.

--------------------------------------------------

CLIENT TRUST (REQUIRED)
----------------------

Clients must trust the internal root CA to avoid browser warnings.

Export the CA certificate from Kubernetes:

  kubectl -n cert-manager get secret homelan-root-ca \
    -o jsonpath='{.data.ca\.crt}' | base64 -d > homelan-root-ca.crt

Install into Linux system trust store (Arch/CachyOS):

  sudo install -Dm644 homelan-root-ca.crt \
    /etc/ca-certificates/trust-source/anchors/homelan-root-ca.crt
  sudo update-ca-trust

Verify:

  curl -v https://sonarr.home.lan | head

--------------------------------------------------

RENEWAL
-------

cert-manager automatically renews certificates before expiry.

Check:

  kubectl -n media describe certificate wildcard-home-lan

--------------------------------------------------

NOTES / FUTURE WORK
-------------------

- Enforce HTTPS-only later (HTTP -> HTTPS redirect) once client compatibility
  (e.g. TVs / Jellyfin apps) is confirmed.
- If other namespaces require TLS:
  - issue another wildcard certificate per namespace, or
  - implement controlled Secret syncing after GitOps is in place.
