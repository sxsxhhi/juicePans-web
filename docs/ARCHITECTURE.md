# juicePans-web 架构说明 · v1.7.5

## 定位

| 组件 | 作用 |
|------|------|
| **juicePans-web**（本仓库） | 浏览器本地 / Docker 站点，默认监听 **8765**，解压绿色版或 `web/server.py` 启动 |
| **PanSou**（可选自建） | 独立 TG/插件聚合 API，常见端口 **8888**；通过环境变量接入，不随绿色版捆绑 |
| **[juicePans](https://github.com/sxsxhhi/juicePans) Skill** | 对话 / CLI 形态，与本站点共享搜索核心思路，发布节奏可对齐版本号 |

Web 端**只检索、展示**公开分享链接，不转存、不托管文件。

## 请求路径

```text
浏览器 → server.py (8765)
           └─ search_core.run_search()
                 ├─ pansou（本地 PANSOU_URL 健康则优先，否则 so.252035.xyz）
                 ├─ haisou / yunso（默认并行）
                 ├─ 可选：panxiaozi、ataw(TA搜)、movie、local
                 └─ 主源 0 结果时自动补跑 ataw（未勾选时）
```

## 引擎策略（v1.7.5）

- **默认引擎**：`pansou,yunso,haisou`（与 Skill 默认三源一致；Web UI 另可勾选盘小子等）。
- **已移除**：`ghspider` / TG 库（GitHub netdisk-spider）；TG 类内容改由盘搜 `--src all` / 自建 PanSou 频道配置覆盖。
- **ataw（TA搜）**：对接 [so.ataw.top](https://so.ataw.top) SSR + 公开详情 API；UI **默认不勾选**；主源失败或无结果时**自动备份**一次。
- **`--engine all`**：仅 `pansou,haisou,yunso`，**不包含** ataw。

## 环境变量

| 变量 | 说明 |
|------|------|
| `JUICEPANS_HOST` | 监听地址；局域网访问设为 `0.0.0.0` |
| `JUICEPANS_PORT` | 端口，默认 `8765` |
| `PANSOU_URL` / `NETDISK_API_URL` | 可选自建 PanSou 根地址（需 `/api/health` 可用） |
| `QUARK_SKILL_DIR` / `NODE_BIN` | 可选，供 `check_links.py` 夸克 CLI 验链 |

不要在文档或示例中写入内网固定 IP、代理口令或账号密钥；部署时由运维自行配置。

## 可选自建 PanSou（概要）

若需要本地 PanSou 实例（例如 NAS / 玩客云侧已部署的兼容 API）：

1. 使用上游 **fish2018/pansou** 等镜像自行部署（本仓库**不 vendor** 上游源码）。
2. 设置 `PANSOU_URL=http://<你的主机>:8888`（示例端口，按实际为准）。
3. 盘搜引擎会先探测 health，再决定走本地或公开 fallback。

绿色版用户无 PanSou 时，仍可直接使用公开盘搜 endpoint，无需额外服务。

## 目录

```text
juicePans-web/
├── web/              # 站点源码（server、search_core、static）
├── docs/             # 部署与架构文档
└── README.md
```

## 合规

仅供学习研究；结果来自公开聚合源，链接有效性未核验 unless 用户开启「检验链接存活」。请支持正版。
