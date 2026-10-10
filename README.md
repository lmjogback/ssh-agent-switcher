# ssh-agent-switcher release builds

This branch exists only to build prebuilt binaries of
[ssh-agent-switcher](https://github.com/jmmv/ssh-agent-switcher) by
Julio Merino. It contains no source code and no changes to the program.

**For the project itself — documentation, issues and pull requests — go to
[jmmv/ssh-agent-switcher](https://github.com/jmmv/ssh-agent-switcher).**
Please do not report bugs here.

## What this is

Upstream does not publish prebuilt binaries. The workflow in
[`.github/workflows/release.yml`](.github/workflows/release.yml) checks out an
unmodified upstream release tag (`ssh-agent-switcher-<version>`), builds it, and
publishes the results as a release in this fork (`v<version>`).

Targets:

| Target                           | Platform                                  |
| -------------------------------- | ----------------------------------------- |
| `x86_64-unknown-linux-musl`      | Linux x86-64                              |
| `aarch64-unknown-linux-musl`     | Linux arm64 (incl. 64-bit Raspberry Pi OS) |
| `armv7-unknown-linux-musleabihf` | Linux ARMv7 (32-bit Raspberry Pi OS, Pi 2+) |
| `arm-unknown-linux-musleabihf`   | Linux ARMv6 (Pi Zero / Pi 1)              |
| `aarch64-apple-darwin`           | macOS on Apple Silicon                    |
| `x86_64-apple-darwin`            | macOS on Intel                            |

The Linux binaries are statically linked against musl and do not depend on the
host's glibc version. Each archive contains the binary, the manual page and the
upstream `COPYING` file. A `SHA256SUMS` file is attached to every release.

## Building a new version

Run the workflow manually with the upstream version number:

```sh
gh workflow run release.yml -R lmjogback/ssh-agent-switcher -f version=1.0.2
gh run watch -R lmjogback/ssh-agent-switcher
```

## Branches

- `release-builds` (default): this README and the build workflow only.
- main: upstream main as of when the fork was created. It is not used by the 
  build, which always checks out upstream directly, and may be out of date.

## License

ssh-agent-switcher is distributed under the BSD 3-Clause license; see
[`COPYING`](https://github.com/jmmv/ssh-agent-switcher/blob/main/COPYING)
upstream. The released archives include that file.
