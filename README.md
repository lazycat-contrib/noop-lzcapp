# noop-lzcapp

Noop（huacnlee/noop，MIT）的懒猫微服打包仓库。镜像模式：引用 dockers-x 从上游源码构建的镜像 `ghcr.io/dockers-x/noop`（上游无官方 Docker 发布）。

## 打包形态

上游 noop 的"服务端"是 bun 运行的 daemon（`src/cli.ts daemon`）：任务编排、agent 调度、本地聊天 API 与 Web 聊天页（8787 端口）。Cloudflare Worker 是可选协调面，本地模式不需要——本打包即本地模式：

- 聊天 API、数据、记忆全部在本机（`/lzcapp/var/noop`），重启不丢失
- Web 聊天页用机器 token 登录（noop.toml 的 `[server] token`，或终端 `bun /noop/src/cli.ts status` 查看）
- 需要多机协调/邮箱登录时，用户可在容器内自行 `noop init --primary` 部署自己的 Worker
- AI agent 运行时（claude/codex CLI）需用户在容器内自行登录，额度走用户自己的账号

## 版本跟踪

跟踪 dockers-x/noop 镜像的 `latest` tag（镜像仓库每 6 小时跟随上游 main 构建一次），lazy 用 mutable latest + bump:patch 模式。

上游：[huacnlee/noop](https://github.com/huacnlee/noop)（MIT）
