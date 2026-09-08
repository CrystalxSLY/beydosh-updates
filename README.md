# Beydosh Update Channel

This public repository provides signed metadata and GitHub Release assets for Beydosh desktop updates.

## Current update path

The installed development baseline is **0.9.0**. The next intended update-test version is **0.9.1**, using the installed 0.9.0 launcher. These are owner-authorized development builds, not a public final 1.0.0 or Customer/Legal release.

The supported format is **`beydosh-signed-plain-v2`**: signed, unencrypted update packages. No AES key, decryption-key provisioning, or encrypted-v1 fallback is required or accepted.

The application requests metadata through its installed, receipt-verified launcher. The launcher verifies the channel and performs download, integrity checking, staging, activation and restart/health handling. The application does not obtain private signing keys. Update functionality belongs to the application workstream; installer work packages the compatible application, launcher and maintenance components.

## Channel state is not a success claim

At this documentation revision, no `updates/stable/latest.beydosh.json` is present. Publication must be determined from the signed live index, not from this README.

- An exact index HTTP 404 means **channel not published**. It does not prove that the installed app is current.
- Network unavailability is an availability error, not “up to date.”
- Invalid, unsigned, stale, malformed or untrusted metadata is rejected; it must not be shown as verified current.
- Only a valid signed index and its exact referenced signed manifest can establish current/update-available status.

## Stable layout

- `updates/stable/latest.beydosh.json`: signed stable-channel index; changed **last**.
- `updates/stable/<version>/manifest.beydosh.json`: immutable signed version manifest.
- GitHub Release assets: immutable signed-plain-v2 `*.bupd` transport chunks, at most 52,428,800 bytes (50 MiB) each.

Version folders, tags and published asset identities must not be reused for different bytes. There is no second `current` or version-list source of truth.

**Legacy scaffolding warning:** the current files under `schemas/` and `templates/UNPUBLISHED-NOT-A-RELEASE/` were created for the former encrypted-v1 contract. They are not v2 validators or publishable metadata. Regenerate and validate them against the actual v2 parser before using them in a release workflow. This documentation update does not change schemas, examples or live release files.

## Trust and release scope

NIST P-256 signatures, pinned public trust, SHA-256, strict inventories and URL/version/replay checks establish authenticity and integrity. The installed trust document's `Production` purpose selects the regular cryptographic verifier; it does not confer Customer, Legal or public-release approval.

The local installer is classified **LOCAL OWNER DEVELOPMENT CANDIDATE**. Persistent owner-managed keys authorize that development workflow; they do not establish Product provenance independent of the local build caller, Authenticode trust or SmartScreen reputation. The installer retains transparent Draft-EULA acknowledgment.

Only the approved release-signing role signs normal updates. The recovery role is pretrusted publicly but its private key is not used in normal publishing. Private keys, credentials, key-storage paths, customer data and source archives must never enter this repository, release assets or logs. Unencrypted compiled update payloads are intentional in v2.

See [Publishing](docs/PUBLISHING.md) for the controlled owner-development release procedure and the separate public-distribution boundary.
