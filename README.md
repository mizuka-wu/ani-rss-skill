# ani-rss-skill

[Codex](https://github.com/openai/codex) skill for [ani-rss](https://github.com/wushuo894/ani-rss) — 通过 AI 管理你的自动追番订阅。

## 这是什么

这是一个 Codex skill，让你可以通过自然语言与 ani-rss 交互：

- 搜索 Bangumi、Mikan、AnimeGarden
- 添加 / 删除 / 启用 / 禁用订阅
- 刷新 RSS、刮削元数据
- 查看日志、服务器状态

AI 通过 `scripts/ani-rss.sh` 脚本与 ani-rss API 通信。

## 安装

```bash
git clone https://github.com/YOUR_USERNAME/ani-rss-skill.git ~/.agents/skills/ani-rss
```

## 配置

```bash
# API Key 认证（推荐）
bash scripts/ani-rss.sh config set --url http://your-host:7789 --api-key your-api-key

# 或者用户名密码认证
bash scripts/ani-rss.sh config set --url http://your-host:7789
bash scripts/ani-rss.sh login --username admin --password your-password
```

环境变量：`ANI_RSS_URL`、`ANI_RSS_API_KEY`。

## 使用

在 Codex 中直接用自然语言：

- "帮我看看现在有哪些订阅"
- "搜索孤独摇滚，添加订阅"
- "刷新所有 RSS"
- "看看最近的日志"

## 认证

| 方式 | 说明 |
|------|------|
| API Key | `x-api-key` 请求头，推荐，无过期 |
| JWT | 用户名密码登录，有过期时间 |

## 命令一览

```bash
config set/show    配置管理
login              登录获取 token
list               订阅列表
add <json>         添加订阅
set <json>         修改订阅
delete <ids>       删除订阅
refresh [id]       刷新 RSS
enable/disable     启用/禁用
search-bgm <name>  搜索 Bangumi
bgm-to-ani <id>    BGM → 订阅对象
mikan <text>       搜索 Mikan
scrape <ids>       刮削元数据
ping / about / logs / config-get
raw <path> [method] [body] [params]  原始 API 调用
```

## License

MIT
