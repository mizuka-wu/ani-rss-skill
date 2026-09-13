# ani-rss-skill

Codex skill for [ani-rss](https://github.com/wushuo894/ani-rss) — 通过 AI 管理自动追番订阅。

## 安装

### 方式一：Agent 一键安装

在 Codex 中直接告诉 agent：

> 帮我安装这个 skill：https://github.com/mizuka-wu/ani-rss-skill

或：

> Install the skill from github.com/mizuka-wu/ani-rss-skill

### 方式二：skill-installer

```
安装 ani-rss skill，来源：github.com/mizuka-wu/ani-rss-skill
```

### 方式三：手动安装

```bash
git clone https://github.com/mizuka-wu/ani-rss-skill.git ~/.codex/skills/ani-rss
```

或下载 `SKILL.md`、`scripts/ani-rss.sh`、`agents/openai.yaml` 到 `~/.codex/skills/ani-rss/` 目录。

## 配置

安装后需要配置服务器地址和认证：

```bash
# API Key 认证（推荐）
bash ~/.codex/skills/ani-rss/scripts/ani-rss.sh config set \
  --url http://your-nas-ip:7789 \
  --api-key your-api-key

# 或用户名密码认证
bash ~/.codex/skills/ani-rss/scripts/ani-rss.sh config set \
  --url http://your-nas-ip:7789
bash ~/.codex/skills/ani-rss/scripts/ani-rss.sh login \
  --username admin --password your-password
```

- 默认端口：**7789**（Docker 默认）
- 配置文件：`~/.config/ani-rss/config.json`
- 环境变量覆盖：`ANI_RSS_URL`、`ANI_RSS_API_KEY`

## 使用

在 Codex 中用自然语言即可：

- "帮我看看现在有哪些订阅"
- "搜索孤独摇滚，添加第一季的订阅"
- "刷新所有 RSS"
- "禁用这几个订阅"
- "看看最近的日志"
- "服务器版本是多少"

## 认证方式

| 方式 | 说明 | 推荐 |
|------|------|------|
| API Key | `x-api-key` 请求头，无过期 | ✅ |
| JWT | 用户名密码登录获取 token，有过期时间 | 需要时重新登录 |

API Key 在 ani-rss 管理后台 → 设置 → API Key 中获取。

## 命令一览

```bash
# 配置
config set --url <url> --api-key <key>
config show
login --username <u> --password <p>

# 订阅
list | add <json> | set <json> | delete <ids> [delFiles]
refresh [id] | enable <ids> | disable <ids>
preview <json> | download-path <json> | import <json>

# 搜索
search-bgm <name> | bgm-to-ani <id> | me-bgm
mikan <text> | mikan-group <url>
anime-garden [bgmUrl] | anime-garden-group <bgmId>

# 刮削
scrape <ids> [force] | scrape-one <json> [force]
update-episodes <ids> [force]

# 合集 & 评分
collection-preview <json> | collection-start <json>
rate <json> | set-rate <json>

# 服务器
ping | about | logs | clear-logs | clear-cache
config-get | config-set <json> | test-notification <json>

# 高级
raw <path> [method] [body] [params]
```

## 项目结构

```
ani-rss-skill/
├── SKILL.md              # Skill 定义（frontmatter + 指令）
├── agents/openai.yaml    # UI 元数据
├── scripts/ani-rss.sh    # API 调用脚本
└── README.md
```

## License

MIT
