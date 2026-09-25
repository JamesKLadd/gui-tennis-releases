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
