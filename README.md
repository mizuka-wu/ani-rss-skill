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
# 克隆到 skills 目录
git clone https://github.com/YOUR_USERNAME/ani-rss-skill.git ~/.agents/skills/ani-rss
```

或者手动复制：
```bash
cp -r /path/to/ani-rss-skill ~/.agents/skills/ani-rss
```

## 配置

首次使用前需要配置服务器地址和认证信息：

```bash
# API Key 认证（推荐）
~/.agents/skills/ani-rss/scripts/ani-rss.sh config set \
  --url http://your-host:12444 \
  --api-key your-api-key

# 或者用户名密码认证
~/.agents/skills/ani-rss/scripts/ani-rss.sh config set \
  --url http://your-host:12444
~/.agents/skills/ani-rss/scripts/ani-rss.sh login \
  --username admin --password your-password
```

也可以通过环境变量配置：
```bash
export ANI_RSS_URL=http://your-host:12444
export ANI_RSS_API_KEY=your-api-key
```

## 使用

在 Codex 中直接用自然语言即可：

- "帮我看看现在有哪些订阅"
- "搜索孤独摇滚，添加订阅"
- "刷新所有 RSS"
- "禁用这几个订阅：xxx, yyy"
- "看看最近的日志"

## 认证方式

ani-rss 支持多种认证，本 skill 使用以下两种：

| 方式 | 说明 | 推荐 |
|------|------|------|
| API Key | 通过 `x-api-key` 请求头发送，设置一次即可 | ✅ |
| JWT Token | 用户名密码登录获取，有过期时间 | 需要时重新登录 |

## 脚本命令一览

```bash
ani-rss.sh <command> [args...]

# 配置
config set --url <url> --api-key <key>
config show
login --username <u> --password <p>

# 订阅
list / add <json> / set <json> / delete <ids-json>
refresh [id] / enable <ids-json> / disable <ids-json>
preview <json> / download-path <json> / import <json>

# 搜索
search-bgm <name> / bgm-to-ani <id>
mikan <text> / mikan-group <url>
anime-garden [bgm-url] / anime-garden-group <bgmId>

# 刮削 & 更新
scrape <ids-json> [force] / scrape-one <json> [force]
update-episodes <ids-json> [force]

# 合集
collection-preview <json> / collection-start <json>

# 评分
rate <json> / set-rate <json>

# 服务器
ping / about / logs / clear-logs / clear-cache
config-get / config-set <json> / test-notification <json>

# 高级
raw <path> [method] [body] [params]
```

## License

MIT
