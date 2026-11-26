# B站数据接口（Bilibili API）：视频搜索、详情、评论、UP 主、热门

**B站数据 API · B站视频搜索 · B站评论采集 · UP主主页和投稿 · B站热门**

这个仓库是 [DataXAPI](https://dataxapi.com/zh/?ref=gh-bilibili-api) 的B站接口说明和能直接跑的脚本：11 个接口，一把 Key，按次付费，$0.002 起，**出错不收费**。不用登录平台账号，不用 Cookie，不开浏览器。

[免费拿 Key：试用最多 333 次，不用绑卡](https://dataxapi.com/zh/signin/?button=gh-bilibili-api) · [全部接口文档](https://dataxapi.com/zh/apis/?ref=gh-bilibili-api) · [接进 AI（MCP）](#接进-aimcp) · [English](#english)

最低充 $10，余额不过期；支持支付宝、微信支付和银行卡。

## 全部 11 个接口

### 视频

| 接口 | 拿到什么 | 价格 | 编号 |
|---|---|---|---|
| [B站视频搜索](https://dataxapi.com/zh/apis/bilibili/videos/search/?ref=gh-bilibili-api) | 按搜索词取一页 B 站视频，可按相关度、最新或播放最多排：标题、UP 主、播放、点赞、收藏、评论数、时长。 | $0.002 一次 | `bilibili.videos.search` |
| [B站视频评论](https://dataxapi.com/zh/apis/bilibili/videos/comments/list/?ref=gh-bilibili-api) | 按 BV 号取一页 B 站视频评论，可按热门或最新排：正文、评论者和他的等级、点赞数、回复数、发布时间。 | $0.002 一次 | `bilibili.videos.comments.list` |
| [B站视频详情](https://dataxapi.com/zh/apis/bilibili/videos/get/?ref=gh-bilibili-api) | 按 BV 号或链接取一个 B 站视频：标题、简介、UP 主、播放、点赞、投币、收藏、弹幕数、时长、标签、分区、IP 属地，以及取字幕和弹幕要用的 cid。 | $0.002 一次 | `bilibili.videos.get` |
| [B站视频转文字（文案提取、逐字稿）](https://dataxapi.com/zh/apis/bilibili/videos/transcript/get/?ref=gh-bilibili-api) | 给一个 B 站视频的链接或 BV 号，返回视频里说的话：全文、每一句的起止时间和现成的 SRT 字幕，连同标题、UP 主和时长；可以区分说话人。多 P 视频转第一 P。每次收费，识别语音的另按视频分钟数收，没人说话不收。5 分钟以内的视频直接返回文字；超过 5 分钟、2 小时以内的先回一个凭证（job），过一会儿带着它再调这个接口取文字，按实际分钟数收，只在取到文字时收。 | $0.004 一次 | `bilibili.videos.transcript.get` |
| [B站综合热门](https://dataxapi.com/zh/apis/bilibili/videos/trending/?ref=gh-bilibili-api) | 取一页 B 站综合热门视频：标题、简介、UP 主、播放、点赞、投币、收藏、弹幕数、时长、分区、IP 属地、推荐理由。 | $0.002 一次 | `bilibili.videos.trending` |
| [B 站视频和音频下载地址](https://dataxapi.com/zh/apis/bilibili/videos/media/get/?ref=gh-bilibili-api) | 给一个 B 站视频的 BV 号或链接，返回视频的各档清晰度和音频的各档音质，分开给（带宽高、编码、码率、备用地址和过期时间）；每个地址都要带请求头 Referer: https://www.bilibili.com 去取，音视频用 ffmpeg 合成一个文件，过期了再调一次即可。 | $0.002 一次 | `bilibili.videos.media.get` |

### 评论

| 接口 | 拿到什么 | 价格 | 编号 |
|---|---|---|---|
| [B站评论回复](https://dataxapi.com/zh/apis/bilibili/comments/replies/list/?ref=gh-bilibili-api) | 按评论编号和它所在视频的 BV 号取一页回复：正文、回复者、点赞数、回复的是哪一条、发布时间。 | $0.002 一次 | `bilibili.comments.replies.list` |

### 热榜和趋势

| 接口 | 拿到什么 | 价格 | 编号 |
|---|---|---|---|
| [B站热搜榜](https://dataxapi.com/zh/apis/bilibili/trends/list/?ref=gh-bilibili-api) | 取 B 站当前的热搜词榜，最多 50 个词，带名次、热度和榜单上显示的那句话。 | $0.002 一次 | `bilibili.trends.list` |

### 账号

| 接口 | 拿到什么 | 价格 | 编号 |
|---|---|---|---|
| [B站用户资料](https://dataxapi.com/zh/apis/bilibili/users/get/?ref=gh-bilibili-api) | 按用户编号取 B 站用户资料：昵称、签名、头像、是否认证和认证说明、粉丝数、关注数、投稿视频数、累计获赞、账号等级、直播间链接。 | $0.002 一次 | `bilibili.users.get` |
| [B站用户投稿](https://dataxapi.com/zh/apis/bilibili/users/videos/list/?ref=gh-bilibili-api) | 按用户编号取一页 B 站用户投稿的视频，新的在前：标题、简介、播放数、评论数、弹幕数、时长、发布时间。 | $0.002 一次 | `bilibili.users.videos.list` |

### 备用版：原接口取不到时改调

| 接口 | 拿到什么 | 价格 | 编号 |
|---|---|---|---|
| [B站用户投稿（备用版）](https://dataxapi.com/zh/apis/bilibili/backup/users/videos/list/?ref=gh-bilibili-api) | B站用户投稿的备用版，原接口取不到时改调：参数和返回相同（不含简介和评论数），价格更高。 | $0.03 一次 | `bilibili.backup.users.videos.list` |

## 真实返回长什么样

**B站视频搜索**（`bilibili.videos.search`，参数 `{"query":"机械键盘"}`），录下的真实返回，个人信息换成了 …：

```json
{
  "data": {
    "items": [
      {
        "id": "…",
        "url": "https://example.com/…",
        "type": "video",
        "title": "…",
        "text": null,
        "published_at": "2026-09-30T08:55:00.000Z",
        "author": {
          "id": "…",
          "name": "…",
          "avatar_url": "https://example.com/…"
        },
        "metrics": {
          "likes": 237,
          "comments": 64,
          "favorites": 169,
          "views": 35706
        },
        "hashtags": [
          "…",
          "…"
        ]
      }
    ]
  },
  "page": {
    "next_cursor": "example-cursor-1",
    "cursor_expires_at": "2026-10-12T19:47:48.000Z",
    "has_more": true,
    "returned": 20
  }
}
```

每个接口都是同一种结构：列表在 `data.items`，单个在 `data.item`，下一页用 `page.next_cursor`，这次扣了多少在 `meta.billing.amount`，平台不给的字段为 `null` 并在 `meta.unavailable` 里写明。

## 快速开始

1. [拿一把 Key](https://dataxapi.com/zh/signin/?button=gh-bilibili-api)（`dx_` 开头），放进环境变量：`export DATAXAPI_API_KEY=dx_...`
2. 调一次接口：

```bash
curl -G "https://api.dataxapi.com/v1/bilibili/videos/search" \
  -H "Authorization: Bearer $DATAXAPI_API_KEY" \
  --data-urlencode 'query=机械键盘'
```

3. 或者跑 `examples/` 里的脚本。只用 Python 标准库（3.9 以上）；不加 `--yes` 只报价、不调用，加了才真跑，跑完告诉你实际花了多少：

| 脚本 | 做什么 | 先看要花多少 |
|---|---|---|
| [quickstart.py](examples/quickstart.py) | 取几页结果，存成 CSV | `cd examples && python3 quickstart.py 机械键盘` |

## 接进 AI（MCP）

Claude Code：

```bash
claude mcp add --transport http --scope user dataxapi https://api.dataxapi.com/mcp --header "Authorization: Bearer $DATAXAPI_API_KEY"
```

Cursor、Cherry Studio、WorkBuddy 等支持远程 MCP 的客户端：

```json
{
  "mcpServers": {
    "dataxapi": {
      "url": "https://api.dataxapi.com/mcp",
      "headers": {
        "Authorization": "Bearer dx_..."
      }
    }
  }
}
```

接上以后直接用中文问，比如“帮我看看这个关键词最近一个月在抖音上的热度”。AI 花钱前可以先免费查接口和价格。也可以装成技能：`npx skills add data-x-api/skills`。

## 常见问题

**要不要平台账号、Cookie 或扫码？**

不要。只要一把 DataXAPI Key，不碰你的账号，也就不存在账号被风控的问题。

**调用出错扣钱吗？**

不扣。每次返回里的 `meta.billing.amount` 写明这次扣了多少（美元）。

**数据有多新？**

默认在你调用时从平台实时读取，返回里的 `meta.fetched_at` 写明读取时间。

**怎么翻页？**

列表接口一次返回一页，把返回里的 `page.next_cursor` 作为 `cursor` 传回去取下一页，每一页单独计费。

## English

Bilibili API: video search, video details, comments, uploaders and trending, through one key, paid per call.

No platform account, cookie or QR login. Paid per call from $0.002; errors are not charged. Free trial: up to 333 calls, no card. [Get a key](https://dataxapi.com/signin/?button=gh-bilibili-api) · [All endpoints](https://dataxapi.com/apis/?ref=gh-bilibili-api) · MCP: `https://api.dataxapi.com/mcp`.

## License

MIT

<sub>接口和价格取自 DataXAPI 的目录 0051cce45e9530b9、价格版本 22；以 [dataxapi.com/zh/apis](https://dataxapi.com/zh/apis/?ref=gh-bilibili-api) 为准。</sub>
