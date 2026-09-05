# Publishing policy

This repository is a public, append-only update metadata channel. It is not an automatic deployment target.

## Release gate

A release may be published only after all of the following exist:

1. documented business and technical approval;
2. a reproducible build tied to the exact 40-character source commit;
3. passing automated tests, including offline, HTTP 404, malformed document, bad signature, version ordering, URL allowlisting, and the 50 MiB chunk boundary;
4. sandbox or staging evidence for installation, cancellation rollback, update rollback, and recovery;
5. an offline NIST P-256 signing operation with an approved key ID.

No real customer data, production credentials, private signing key, decryption key, or unencrypted application payload may enter this repository or GitHub logs.

## Immutable publication order

1. Build and inspect the release outside this repository.
2. Split the encrypted package into ordered chunks no larger than 52,428,800 bytes.
3. Calculate SHA-256 for every encrypted chunk, every plain chunk, every payload file, and the total encrypted package. The total encrypted hash is calculated over the exact byte concatenation of chunks in ascending `Index` order.
4. Create a draft GitHub Release tagged `v<version>` and upload the chunks. Asset URLs must be HTTPS URLs under `github.com/CrystalxSLY/beydosh-updates/releases/download/v<version>/`.
5. Generate and validate the signed manifest. `MinimumLauncher`, compatibility, rollback policy, sizes, order, URLs, hashes, key ID, UTC timestamp, and source commit must all be explicit.
6. Commit the manifest once at `updates/stable/<version>/manifest.beydosh.json`. Refuse publication if the tag, asset name, or version folder already exists.
7. Independently download and hash-check all assets from their final URLs.
8. Generate, sign, and validate the stable index against the final manifest bytes.
9. Create `updates/stable/latest.beydosh.json` last, or replace it only with a strictly newer, approved, correctly signed version.
10. Publish the GitHub Release only after the index and remote verification agree.

A failed step leaves the current stable index unchanged. Previously published versions and assets are never overwritten or deleted.

## Rollback

Automatic downgrade is forbidden. Rollback metadata identifies whether an independently approved manual rollback is possible and binds the previous version and manifest hash. A rollback requires a new documented approval and cannot bypass the launcher's highest-seen anti-downgrade record.

## Cryptographic boundary

The repository stores signatures and identifiers, not secrets. NIST P-256 signatures and SHA-256 hashes provide authenticity and integrity when verified against a public key already trusted by the launcher. Encryption is not a substitute for signing and cannot prevent code analysis because a functioning client must obtain the ability to decrypt its own update.
