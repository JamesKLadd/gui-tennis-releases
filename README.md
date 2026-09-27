# gui-tennis-releases

Installers for ATP Tennis Simulator. Download the latest from
[Releases](https://github.com/JamesKLadd/gui-tennis-releases/releases/latest); installed copies of the
app check here for updates and install them from inside the app.

## Publishing a release

**Actions → Build and publish a release → Run workflow**, then enter:

- **Version:** the new version, such as `1.2.1` (no `v`). It must not be older than the latest release.
- **gui-tennis branch, tag or commit:** normally `main`.
- **Release notes:** optional; left empty, they list the commits since the previous release.

The workflow checks out the private source with the `SOURCE_TOKEN` secret (a fine-grained token with
**Contents: Read-only** on `JamesKLadd/gui-tennis`), runs every test suite on Windows, macOS and
Linux, builds the installers and publishes `v<version>` here. Running the same version again
replaces its installers.

## Optional: signing the Windows installer

Unsigned installers work, but Windows SmartScreen may show "Windows protected your PC" until the
installer has a reputation. Signing needs a code-signing certificate from a certificate authority (a
paid, yearly purchase; an organization-validated or EV certificate builds reputation fastest). The
workflow signs the `.msi` only when these repository secrets exist, and skips signing otherwise:

- `WINDOWS_CERTIFICATE`: the certificate and private key as a `.pfx` file, base64-encoded
  (PowerShell: `[Convert]::ToBase64String([IO.File]::ReadAllBytes("cert.pfx")) | Set-Clipboard`).
- `WINDOWS_CERTIFICATE_PASSWORD`: the `.pfx` password.
- Optional repository variable `TIMESTAMP_URL`: your certificate authority's timestamp server
  (defaults to DigiCert's). Timestamping keeps signatures valid after the certificate expires.

Certificates issued on a hardware token or kept in a cloud signing service (such as Azure Trusted
Signing) cannot be exported as a `.pfx`; they need that service's own signing step instead. The
macOS disk image would need an Apple Developer ID and notarization, which this workflow does not do.
