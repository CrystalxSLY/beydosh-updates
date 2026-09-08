# Stable channel

The supported update format is `beydosh-signed-plain-v2`: signed, unencrypted packages with no AES-key requirement.

At this documentation revision, `latest.beydosh.json` is absent. An exact HTTP 404 for that index means **channel not published**, not “installed version verified current.” Network failures and invalid metadata are separate states. This README never substitutes for signed channel metadata.

The installed development baseline is 0.9.0; 0.9.1 is the next intended authorized in-app update test. Follow [Publishing](../../docs/PUBLISHING.md): immutable assets must be accessible and verified, then publish the exact signed version manifest, and activate Latest **last**.

Published version directories use normalized `<major>.<minor>.<patch>` names and remain immutable. Do not replace or remove them, reuse asset identities, introduce unsigned placeholders or enable encrypted-v1 fallback.

Updating this documentation does not activate the channel, publish an application update or grant Customer/Legal/public-product approval.
