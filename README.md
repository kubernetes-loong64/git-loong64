# Git for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/Git%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=git&logoColor=white" alt="Git LoongArch64 龙芯架构发行版"></p>

Build [Git](https://github.com/git/git) Docker images for the **LoongArch64 (loong64)** architecture via CI/CD.
Images are provided on multiple base distributions (Anolis OS, Debian, Debian Slim, OpenEuler).

## How it works

A GitHub Actions workflow clones the specified Git version, cross-compiles with
`--platform linux/loong64` in a Debian 13 container, and packages the result into
Docker images based on different Linux distributions. Target platform: `linux/loong64`.

## Branch naming

Push a branch named `loong64-<git-version>` (e.g. `loong64-v2.54.0`) to trigger a build.
Append `+<build>` (e.g. `loong64-v2.54.0+0`) to include build metadata.

## [Release](https://github.com/kubernetes-loong64/git-loong64/releases)

Push a tag matching `release-loong64-<git-version>` (e.g. `release-loong64-v2.54.0+0`)
to publish a GitHub Release with the built Docker images.

The `+<build>` suffix provides build metadata (e.g. `+0`, `+1-alpha.1`).

The suffix in the build metadata indicates the release stage:

| Suffix  | Stage         |
|---------|---------------|
| `alpha` | Internal beta |
| `beta`  | Public beta   |
| `rc`    | Pre-release   |
| (none)  | Stable        |

## Release artifacts

Each release includes Docker image tarballs for the following distributions:

| File                                      | Base distribution |
|-------------------------------------------|-------------------|
| `git-loong64-<version>-anolis.tar`        | Anolis OS         |
| `git-loong64-<version>-debian.tar`        | Debian            |
| `git-loong64-<version>-debian-slim.tar`   | Debian (slim)     |
| `git-loong64-<version>-openeuler.tar`     | OpenEuler         |

Each file has a corresponding `.asc` detached GPG signature.

## Docker images

[![kubernetesloong64/git-loong64](https://img.shields.io/docker/v/kubernetesloong64/git-loong64?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fgit-loong64)](https://hub.docker.com/r/kubernetesloong64/git-loong64/tags)

| Registry               | Image                                                                  |
|------------------------|------------------------------------------------------------------------|
| Docker Hub             | `kubernetesloong64/git-loong64:<tag>`                                  |
| Aliyun (China mirror)  | `registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:<tag>` |

Docker Hub:

```
kubernetesloong64/git-loong64:v2.54.0-loong64-anolis
kubernetesloong64/git-loong64:v2.54.0-loong64-debian
kubernetesloong64/git-loong64:v2.54.0-loong64-debian-slim
kubernetesloong64/git-loong64:v2.54.0-loong64-openeuler
```

Aliyun (China mirror):

```
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-loong64-anolis
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-loong64-debian
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-loong64-debian-slim
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-loong64-openeuler
```

## Verifying releases

- Releases are signed with GPG.
- Download the public key from [keys.openpgp.org](https://keys.openpgp.org).
- Fingerprint: [FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)
- [Manual download](https://keys.openpgp.org/vks/v1/by-fingerprint/FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

Or download the key file manually and import it:

```shell
gpg --import /tmp/xxx
```

## License

[Apache License 2.0](LICENSE)
