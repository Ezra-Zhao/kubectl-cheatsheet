# kubectl 命令速查表 · kubectl Cheatsheet

[![Stars](https://img.shields.io/github/stars/Ezra-Zhao/kubectl-cheatsheet?style=social)](https://github.com/Ezra-Zhao/kubectl-cheatsheet/stargazers) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE) ![Languages](https://img.shields.io/badge/languages-3-blue)

Support & more: [GitHub Sponsors](https://github.com/sponsors/Ezra-Zhao) · [Gumroad — templates & workbooks I use](https://ezraflow28.gumroad.com) · [Ko-fi](https://ko-fi.com/ezra777zhao)


> 🌍 [Español](README.es.md) · [Português](README.pt.md)

一份**一页纸**的 kubectl 速查表：30 个高频条目，覆盖查状态、排障、部署发布、看日志、进容器、上下文切换这些每天都在敲的活。每条只讲三件事——**它是干什么的、一条能直接复制粘贴的命令、适用场景标签**。不编造参数，不拼凑语法。

## 面向谁

SRE、运维工程师、后端开发者，以及任何把应用跑在 Kubernetes 上的人。如果你每次 Pod 崩了都要现搜 `logs` 怎么看上一个容器的，这张表就是给你准备的。

## 怎么用

1. 直接看 **[CHEATSHEET.md](CHEATSHEET.md)** ——速查表正文，英文命令全球开发者都无压力。
2. 先有个集群能练：本地用 minikube / kind 起一个，或者用云厂商的托管 K8s；`kubectl cluster-info` 能出地址就是连上了。
3. 按"查状态排障 → 部署与发布 → 日志与进容器 → 资源管理 → 上下文与命名空间 → 调试神器"的顺序，每个条目亲手敲一遍。注意：多数命令默认作用于当前命名空间，换命名空间加 `-n <ns>`。

## 先跑起来（30 秒验证环境）

```bash
kubectl create deployment hello --image=nginx:1.27   # 起一个 nginx 部署
kubectl get pods                                     # 看到 Running 就是成了
kubectl delete deployment hello                      # 用完删掉
```

## 收录了什么

| 分类 | 内容 |
|---|---|
| 🔍 查状态与排障 | cluster-info / get nodes / get pods -A / describe / events / top（6 条） |
| 🚀 部署与发布 | apply -f / create deployment / scale / set image / rollout restart·status·history·undo / expose（7 条） |
| 📜 日志与进容器 | logs / logs -f / logs -p / exec -it / cp（5 条） |
| 🧰 资源管理 | get 组合查询 / edit / delete / label / port-forward（5 条） |
| 🧭 上下文与命名空间 | config get-contexts / use-context / get·create ns / set-context 固定命名空间（4 条） |
| 🩺 调试神器 | debug 临时容器 / explain 查字段 / diff 预览变更（3 条） |

官方文档只链 https://kubernetes.io/docs/reference/kubectl/，所有命令均对照官方 kubectl 参考核对过子命令与参数。

## 为什么是这 30 条

- **排障闭环**：Pod 出事照着顺序走——`get pods -A` 看状态 → `describe` 看 Events → `logs -p` 看崩溃前的日志，多数问题在这三步里就能定位。
- **发布可回滚**：`set image` 发版、`rollout status` 盯进度、出事 `rollout undo` 一条命令退回去，不用半夜翻 YAML。
- **防手滑**：`diff` 在 `apply` 之前先看会改什么；切到生产集群前先 `config get-contexts` 确认当前上下文。

## 欢迎 PR

发现命令写错了、参数过时了、翻译不到位——欢迎提 Pull Request。新增条目请保持统一格式（一句话说明 / bash 代码块 / 标签），**只收真实可用的命令，不确定的宁可不收**。

## 📚 更多速查表

同一作者的其他速查表，同样有中/西/葡三语版本：

- [FFmpeg 命令速查表](https://github.com/Ezra-Zhao/ffmpeg-cheatsheet) — 28 条音视频处理命令
- [Docker 命令速查表](https://github.com/Ezra-Zhao/docker-cheatsheet) — 28 条 docker / compose 命令
- [Git 实战速查表](https://github.com/Ezra-Zhao/git-cheatsheet) — 30 条日常+救命命令
- [curl 命令速查表](https://github.com/Ezra-Zhao/curl-cheatsheet) — 29 条 API 调试命令
- [正则表达式速查表](https://github.com/Ezra-Zhao/regex-cheatsheet) — 30 条实战正则模式
- [jq 命令速查表](https://github.com/Ezra-Zhao/jq-cheatsheet) — 30 条 JSON 处理 filter
- [终端神器速查表](https://github.com/Ezra-Zhao/terminal-superpowers-cheatsheet) — 14 个终端效率工具
- [Adobe 免费替代速查表](https://github.com/Ezra-Zhao/adobe-free-alternatives-cheatsheet) — 16 个 Adobe 免费替代品
- [退订省钱速查表](https://github.com/Ezra-Zhao/desubscribe-cheatsheet) — 10 组退订替代，年省约 $1,260
- [SQL 速查表](https://github.com/Ezra-Zhao/sql-cheatsheet) — 查询、联表、聚合与实战写法
- [SSH 速查表](https://github.com/Ezra-Zhao/ssh-cheatsheet) — 连接、隧道与跳板机实战

## License

MIT © 2026 Guangyi Zhao，详见 [LICENSE](LICENSE)。
