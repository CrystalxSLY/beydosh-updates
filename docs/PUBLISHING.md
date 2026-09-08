# Publishing: signed-plain-v2 owner-development updates

This repository is an append-only update channel, not an automatic deployment target. Editing documentation does not sign, publish or activate an update.

## Authorization and scope

The current baseline is 0.9.0; 0.9.1 is the next intended in-app update test. A locally authorized development installer and a specifically authorized GitHub update test are distinct actions. Building a UI fix does not by itself authorize uploading assets or changing stable Latest.

Before a remote update test, record explicit owner authorization for the exact source/payload version, signing role, repository/channel and activation step. A specifically authorized owner-development GitHub test does not constitute Customer, Legal, Live-business or final public-product approval.

Product/Customer/Legal publisher gates remain separate and closed unless their own requirements are met. The Draft EULA remains a draft. Owner-managed signing does not claim independent Product provenance, Authenticode certification or Windows publisher reputation.

Run relevant functional self-tests and record actual results. Do not automatically commission independent update QA or label functional self-tests “QA-PASS.” Installation/update/restart evidence must be reported honestly; an unperformed end-to-end test remains outstanding.

## Build and signing contract

1. Build the exact committed application payload with compatible installed-launcher contracts. For the intended 0.9.1 test, require launcher 0.9.0 or the actual verified minimum. Preserve signature, inventory, replay/downgrade, atomic activation, readiness/health and rollback checks.
2. Package only `beydosh-signed-plain-v2`. Reject encrypted v1, unknown formats and unsigned fallbacks. No AES/decryption key is part of this path.
3. Use only the approved persistent release-signing role and its pinned public identity. Keep private material outside repositories, payloads and logs. The private recovery key is never used for normal build/signing.
4. Sign canonical Latest and manifest payloads with NIST P-256. Latest binds the exact signed manifest bytes by SHA-256; the trusted KeyId must agree.
5. Keep signing and publication explicit. The existing generic `pack-remote` primitive is not by itself a fully authorized owner-release pipeline. The owner tool's `sign-base` operation signs an embedded local package, not a remote-v2 release. Establish the controlled, fixed-role remote invocation/adapter before using it; do not infer its existence from the installer build.
6. Build in isolated staging. A package builder may write a local Latest file; this must not accidentally modify an active release checkout.

No private keys, credentials, private key-storage paths, source archives or real customer data may be included in GitHub content or logs. Compiled plaintext payload bytes are expected in v2 and do not constitute a missing-encryption error.

## v2 transport and manifest

Each chunk begins with the exact ASCII header:

`BUPD|2|signed-plain|<version>|<index>|<total>|`

Index is zero-based; chunk filenames are one-based, beginning with `00001.bupd`. Plain archive bytes follow the header. Transport and plain chunks remain bounded to 50 MiB.

The manifest binds version, release ID, source commit, UTC time, trusted KeyId, MinimumLauncher, Windows/x64 compatibility and `Compatibility.PackageFormat = "beydosh-signed-plain-v2"`. It also binds ordered chunk URLs, `PlainBytes`/`TransportBytes`, `PlainSha256`/`TransportSha256`, `TotalPlainBytes`, `TotalTransportBytes`, `TotalTransportSha256`, exact payload inventory and rollback/security metadata. The total transport hash covers exact transport chunks concatenated in ascending index order.

Optional signed `PatchNotes` contain at most 100 plain-text lines of at most 1000 characters each. No dynamic HTML. Unknown fields and incompatible documents remain rejected by the actual client parser.

The repository's existing encrypted-v1 schemas/templates are legacy scaffolding, not authoritative v2 validators. Align and test them against the shipping parser before release use; never publish their placeholder signatures or example metadata.

## Immutable publication order

1. Record authorization; build, inspect, test and sign the exact version in isolated staging.
2. Refuse collisions with existing version folders, tags or assets. Prepare the immutable chunks and signed manifest.
3. Upload the version's assets to a release tagged `v<version>`. Make the authorized release assets accessible at their final HTTPS URLs before activating Latest. A private draft URL is not a successful public-client availability check.
4. Fetch the final assets through the intended client access path and verify their lengths and hashes. URLs must remain under `https://github.com/CrystalxSLY/beydosh-updates/releases/download/v<version>/`.
5. Commit the verified signed manifest at `updates/stable/<version>/manifest.beydosh.json`; retrieve and verify its exact final bytes.
6. Validate the signed index against that manifest, then create or update `updates/stable/latest.beydosh.json` **as the final channel-activation step**.
7. Observe the authorized real 0.9.0-to-0.9.1 in-app update, shutdown handoff, activation, restart/readiness and relevant failure behavior. Record what actually happened; this documentation does not claim the test passed.

A failure before activation leaves the previous Latest unchanged. An activation or runtime failure must not trigger ad-hoc index rollback, asset replacement, silent downgrade or removal of published versions; follow a separately authorized recovery procedure.

## Rollback and future public distribution

Local transactional rollback after failed activation/start is distinct from publishing a downgrade. Remote downgrade/recovery metadata must obey the launcher's highest-seen and previous-manifest rules and needs explicit authorization; it cannot bypass anti-replay state.

Final public-product/customer distribution retains its separate signing/release authority, legally approved EULA, supported clean-Windows validation and any required Authenticode process. A successful owner-development update test is evidence for that later work, not a substitute for those approvals.
