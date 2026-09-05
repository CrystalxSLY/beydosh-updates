# Beydosh Update Channel

This public repository is the metadata channel for verified Beydosh desktop updates.

## Current state

**No update is published.** The stable index `updates/stable/latest.beydosh.json` intentionally does not exist. A missing, unreachable, stale, malformed, unsigned, or untrusted index must be treated as “no update available” (fail closed).

The repository contains only schemas, publishing guidance, and clearly marked unpublished templates. It contains no application binaries, customer data, private source code, credentials, encryption keys, or signing keys.

## Stable layout

- `updates/stable/latest.beydosh.json`: signed stable-channel index; created only for an approved release.
- `updates/stable/<version>/manifest.beydosh.json`: immutable signed manifest for one version.
- GitHub Release assets: immutable encrypted chunks, each at most 52,428,800 bytes (50 MiB).
- `schemas/`: strict JSON schemas for the signed index and manifest.
- `templates/UNPUBLISHED-NOT-A-RELEASE/`: examples that are deliberately invalid as live release documents.

Published version folders and Release assets are append-only. They are never deleted, replaced, or reused for another build.

## Trust model

Authenticity comes from a trusted NIST P-256 public key, signatures over the canonical payload bytes, SHA-256 hashes, strict URL validation, ordered chunk metadata, and anti-downgrade state in the launcher. Private signing keys and decryption keys must never be stored here or embedded as repository secrets.

Encryption does not prevent analysis of client code: a client that can run an update must eventually decrypt it. Encryption can protect transport artifacts, but signatures and hashes establish authenticity and integrity.

See [Publishing](docs/PUBLISHING.md) for the gated release procedure. Until that procedure is approved and completed, the channel remains intentionally empty.
