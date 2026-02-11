# channel

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/alphafactor/channel/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/alphafactor/channel/SKILL.md)
> Category: AI & LLMs

---

## Description

WeChat Official Account Draft Box management tool. Create and manage graphic draft articles via WeChat API, supporting text and images. Automatically extracts the first paragraph as summary. Supports draft creation, listing, publishing, and deletion.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
WeChat Official Account Draft Box management tool. Create and manage graphic draft articles via WeChat API, supporting text and images. Automatically extracts the first paragraph as summary. Supports draft creation, listing, publishing, and deletion.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run channel`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the channel workflow. Use the following context:

Description: WeChat Official Account Draft Box management tool. Create and manage graphic draft articles via WeChat API, supporting text and images. Automatically extracts the first paragraph as summary. Supports draft creation, listing, publishing, and deletion.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: channel
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 微信公众号草稿箱管理

通过微信公众号 API 管理草稿箱内容，支持创建图文消息、上传图片、发布文章。

## 功能特性

- 📝 **图文草稿** - 创建带格式的图文消息
- 🖼️ **图片支持** - 自动上传正文和封面图片
- 📋 **自动摘要** - 正文第一段自动提取为文章摘要
- 📊 **草稿管理** - 查看、发布、删除草稿
- 🔗 **发布接口** - 支持通过 API 发布（需权限）

## 前提条件

### 1. 微信公众号认证

- 拥有一个微信公众号（订阅号或服务号）
- 完成微信认证（部分接口需要）

### 2. 获取开发者凭证

1. 登录 [微信公众平台](https://mp.weixin.qq.com)
2. 开发 → 基本配置 → 开发者ID
3. 获取 **AppID** 和 **AppSecret**
4. 添加服务器 IP 到白名单

### 3. 配置环境变量

```bash
# 添加到 ~/.zshrc
export WECHAT_APPID="your-app-id"
export WECHAT_APPSECRET="your-app-secret"
```

然后执行：
```bash
source ~/.zshrc
```

## 使用方法

### 创建草稿

**基础用法：**
```bash
python3 scripts/channel.py create "文章标题" "这里是正文内容..."
```

**从文件读取正文：**
```bash
python3 scripts/channel.py create "文章标题" --file article.txt
```

**带封面图：**
```bash
python3 scripts/channel.py create "文章标题" "正文内容..." --cover cover.jpg
```

**设置作者：**
```bash
python3 scripts/channel.py create "文章标题" "正文..." --author "张三"
```

### 正文格式

**纯文本：**
```bash
python3 scripts/channel.py create "标题" "这是正文内容，支持换行。\n\n第二段内容..."
```

**带图片（Markdown 格式）：**
```bash
python3 scripts/channel.py create "标题" "正文\n\n!<span class=\"image\"><span>描述</span></span>(/path/to/image.jpg)\n\n更多内容..."
```

**HTML 格式：**
```bash
python3 scripts/channel.py create "标题" "<p>正文</p><img src='url' />"
```

### 查看草稿列表

```bash
# 列出最近 20 篇
python3 scripts/channel.py list

# 列出最近 50 篇
python3 scripts/channel.py list --limit 50
```

输出示例：
```
📝 草稿列表 (3 篇):

序号   Media ID                       标题                                     更新时间
----------------------------------------------------------------------------------------------------
1      MEDIA_ID_1234567890abcdef    欢迎使用微信公众号                         2024-02-03 15:30
2      MEDIA_ID_abcdef1234567890    文章标题示例                               2024-02-03 14:20
3      MEDIA_ID_xxxxxxxxxxxxxxxx    测试草稿                                   2024-02-03 13:10
```

### 发布草稿

```bash
python3 scripts/channel.py publish MEDIA_ID_1234567890abcdef
```

⚠️ **注意**：发布接口需要开通发布权限，部分账号可能需要手动在后台发布。

### 删除草稿

```bash
python3 scripts/channel.py delete MEDIA_ID_1234567890abcdef
```

## 命令参考

| 命令 | 功能 | 示例 |
|------|------|------|
| `create` | 创建草稿 | `create "标题" "正文" --cover img.jpg` |
| `list` | 列岀草稿 | `list --limit 20` |
| `publish` | 发布草稿 | `publish media_id` |
| `delete` | 删除草稿 | `delete media_id` |

### create 命令参数

| 参数 | 简写 | 说明 | 必填 |
|------|------|------|------|
| `title` | - | 文章标题 | 是 |
| `content` | - | 正文内容 | 否（可用 --file） |
| `--file` | `-f` | 从文件读取正文 | 否 |
| `--author` | `-a` | 作者名称 | 否 |
| `--cover` | `-c` | 封面图片路径 | 否 |
| `--no-comment` | - | 关闭评论 | 否 |
| `--fans-only` | - | 仅粉丝可评论 | 否 |

## 正文内容格式

### Markdown 支持

- `**粗体**` → 粗体
- `*斜体*` → 斜体
- `<span class="image"><span>描述</span></span>(路径)` → 图片（自动上传）

### 图片处理

**本地图片（自动上传）：**
```markdown
!<span class="image"><span>图片描述</span></span>(/path/to/local/image.jpg)
```

**网络图片（直接使用）：**
```markdown
!<span class="image"><span>图片描述</span></span>(https://example.com/image.jpg)
```

### 摘要提取规则

- 自动提取正文第一段作为摘要
- 移除 HTML 标签
- 超过 120 字符自动截断并添加 "..."
- 用于文章列表展示和分享预览

## 输出结果

创建成功示例：
```
============================================================
✅ 草稿创建成功!
============================================================
📄 Media ID: MEDIA_ID_1234567890abcdef
📝 标题: 欢迎使用微信公众号
📋 摘要: 这是文章的摘要内容，来自正文第一段...
⏰ 创建时间: 2024-02-03T15:30:45.123456

💡 提示:
   - 草稿已保存到微信公众号后台
   - 请登录 mp.weixin.qq.com 查看并发布
   - 或使用 'publish' 命令直接发布（需开通权限）
============================================================
```

## 使用场景

### 场景1：快速发布文章

```bash
# 创建并准备发布
python3 scripts/channel.py create "今日新闻" "今天的重要新闻是..." --author "编辑部"

# 然后手动或自动发布
python3 scripts/channel.py list
python3 scripts/channel.py publish MEDIA_ID_xxxx
```

### 场景2：批量导入文章

```bash
# 准备多个文章文件
for file in articles/*.md; do
    title=$(head -1 "$file")
    python3 scripts/channel.py create "$title" --file "$file"
done
```

### 场景3：自动化发布流程

```bash
#!/bin/bash
# publish_daily.sh

TITLE="$(date +%Y年%m月%d日) 日报"
CONTENT=$(cat template.txt)

# 创建草稿
RESULT=$(python3 scripts/channel.py create "$TITLE" "$CONTENT" --cover daily_cover.jpg)

# 提取 Media ID 并发布（可选）
# MEDIA_ID=$(echo "$RESULT" | grep "Media ID:" | awk '{print $3}')
# python3 scripts/channel.py publish "$MEDIA_ID"
```

## 常见问题

**错误：请设置环境变量 WECHAT_APPID 和 WECHAT_APPSECRET**
→ 检查环境变量是否正确设置并生效

**错误：access_token missing**
→ 检查 AppID 和 AppSecret 是否正确
→ 确认服务器 IP 已添加到公众号白名单

**错误：api unauthorized**
→ 公众号未认证，部分接口需要微信认证
→ 订阅号和服务号权限不同

**图片上传失败**
→ 检查图片路径是否正确
→ 图片大小不能超过 10MB
→ 支持格式：jpg, png, gif

**发布失败**
→ 确认已开通发布权限
→ 部分账号需要手动在后台发布

## API 限制

| 接口 | 每日限制 | 说明 |
|------|----------|------|
| 获取 Access Token | 2000 次 | 有效期 7200 秒 |
| 创建草稿 | 100 篇 | 草稿总数上限 100 |
| 上传图片 | 无明确限制 | 单张最大 10MB |
| 发布 | 无明确限制 | 需要发布权限 |

## 注意事项

1. **草稿数量** - 草稿箱最多保存 100 篇，超出需要删除旧草稿
2. **图片存储** - 上传的图片存储在微信服务器，有有效期限制
3. **内容审核** - 发布的内容需要符合微信内容规范
4. **原创声明** - 可通过 API 声明原创（需额外参数）

## 参考

- 微信公众号文档: https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html
- 草稿箱接口: [references/wechat_api.md](references/wechat_api.md)
- 微信公众平台: https://mp.weixin.qq.com

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
