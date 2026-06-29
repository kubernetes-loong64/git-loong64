# Git for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/Git%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=git&logoColor=white" alt="Git LoongArch64 龙芯架构发行版"></p>

通过 CI/CD 为 **LoongArch64 (loong64)** 架构构建 [Git](https://github.com/git/git) Docker 镜像。
基于多种 Linux 发行版（Anolis OS、Debian、Debian Slim、OpenEuler）提供镜像。

## 工作原理

GitHub Actions 工作流克隆指定的 Git 版本，在 Debian 13 容器中以
`--platform linux/loong64` 交叉编译，并将产物打包为基于不同 Linux 发行版的
Docker 镜像。目标平台：`linux/loong64`。

## 分支命名

推送名为 `loong64-<git-version>` 的分支（例如 `loong64-v2.54.0`）以触发构建。
可附加 `+<build>`（例如 `loong64-v2.54.0+0`）来包含构建元数据。

## [发布](https://github.com/kubernetes-loong64/git-loong64/releases)

推送匹配 `release-loong64-<git-version>` 的标签（例如 `release-loong64-v2.54.0+0`）
即可发布 GitHub Release，包含构建好的 Docker 镜像。

`+<build>` 后缀提供构建元数据（例如 `+0`、`+1-alpha.1`）。

构建元数据中的后缀表示发布阶段：

| 后缀      | 阶段    |
|---------|-------|
| `alpha` | 内部测试版 |
| `beta`  | 公开测试版 |
| `rc`    | 预发布   |
| (无)     | 稳定版   |

## 发布产物

每个发布包含以下发行版的 Docker 镜像包：

| 文件                                      | 基础发行版         |
|-----------------------------------------|---------------|
| `git-loong64-<version>-anolis.tar`      | Anolis OS     |
| `git-loong64-<version>-debian.tar`      | Debian        |
| `git-loong64-<version>-debian-slim.tar` | Debian (slim) |
| `git-loong64-<version>-openeuler.tar`   | OpenEuler     |

每个文件都有对应的 `.asc` 分离 GPG 签名。

## Docker 镜像

- [![kubernetesloong64/git-loong64](https://img.shields.io/docker/v/kubernetesloong64/git-loong64/v2.54.0-anolis?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fgit-loong64)](https://hub.docker.com/r/kubernetesloong64/git-loong64/tags)
- [![kubernetesloong64/git-loong64](https://img.shields.io/docker/v/kubernetesloong64/git-loong64/v2.54.0-debian?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fgit-loong64)](https://hub.docker.com/r/kubernetesloong64/git-loong64/tags)
- [![kubernetesloong64/git-loong64](https://img.shields.io/docker/v/kubernetesloong64/git-loong64/v2.54.0-debian-slim?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fgit-loong64)](https://hub.docker.com/r/kubernetesloong64/git-loong64/tags)
- [![kubernetesloong64/git-loong64](https://img.shields.io/docker/v/kubernetesloong64/git-loong64/v2.54.0-openeuler?sort=semver&arch=loong64&logo=docker&label=kubernetesloong64%2Fgit-loong64)](https://hub.docker.com/r/kubernetesloong64/git-loong64/tags)

| 镜像仓库       | 镜像                                                                     |
|------------|------------------------------------------------------------------------|
| Docker Hub | `kubernetesloong64/git-loong64:<tag>`                                  |
| 阿里云（中国镜像）  | `registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:<tag>` |

Docker Hub：

```
kubernetesloong64/git-loong64:v2.54.0-anolis
kubernetesloong64/git-loong64:v2.54.0-debian
kubernetesloong64/git-loong64:v2.54.0-debian-slim
kubernetesloong64/git-loong64:v2.54.0-openeuler
```

阿里云（中国镜像）：

```
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-anolis
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-debian
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-debian-slim
registry.cn-qingdao.aliyuncs.com/kubernetesloong64/git-loong64:v2.54.0-openeuler
```

## 验证发布

- 发布文件使用 GPG 签名。
- 从 [keys.openpgp.org](https://keys.openpgp.org) 下载公钥。
- 指纹：[FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)
- [手动下载](https://keys.openpgp.org/vks/v1/by-fingerprint/FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

或者，手动下载公钥文件后导入：

```shell
gpg --import /tmp/xxx
```

## 许可证

[Apache License 2.0](LICENSE)
