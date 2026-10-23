# WorkBuddy Token 消耗看板（离线版）

> 一个**单文件、零依赖、纯本地运行**的 AI 大模型 token（词元 / 令牌）用量统计看板。
> 它是线上站 [token.daeai.cn](https://token.daeai.cn/)（「Workbuddy Token 消耗看板」）的**离线孪生版（offline twin）**：
> 所有日志解析与图表绘制都在你的浏览器（browser）里完成，**数据不出本机，零上传（no upload）**。

## 特性（features）

- **纯前端（front-end）单文件**：双击即可在浏览器打开，无需安装、无需服务器、无需联网。
- **彻底离线**：已剥离原站全部外链（推广横幅、远程图标、访问统计接口），断网可用。
- **多维统计**：按工作空间 / 会话 / 模型 / 日期统计 token 用量、缓存命中（cache hit）、会话分布，并提供趋势图、散点图与明细表。

## 使用方法（how to use）

1. 下载仓库里的 `index.html`（即 `Token消耗看板-本地版.html`）。
2. 用 **Chrome 或 Edge** 双击打开（Firefox 也可，走目录选择兜底方案）。
3. 点击「选择日志目录」，选中你本地存放 `.jsonl` 日志的文件夹。
4. 工具会自动扫描并生成统计图表。

> 在线预览：本仓库可通过 GitHub Pages 直接访问 `https://chengwerit.github.io/workbuddy-token-dashboard/`
> （需在仓库 **Settings → Pages** 中把来源设为 `main` 分支、目录 `/root` 并保存后生效）。

## 日志格式要求（data format）

本看板读取 **每行一个 JSON** 的 `.jsonl` 日志，且需要包含 token 用量字段，典型结构：

```json
{
  "timestamp": "2026-10-23T10:00:00Z",
  "sessionId": "xxx",
  "role": "assistant",
  "providerData": {
    "rawUsage": {
      "prompt_tokens": 1234,
      "completion_tokens": 567,
      "total_tokens": 1801,
      "cached_tokens": 100
    }
  }
}
```

关键字段：`providerData.rawUsage`（或 `usage`）下的 `total_tokens` / `prompt_tokens` / `completion_tokens` / `cached_tokens`，以及 `timestamp`；可选 `sessionId`、`role`、`content` 用于分组。

> 注意：不同 WorkBuddy 构建 / 导出产出的日志格式可能不同。若你的本地日志不含上述 `providerData.rawUsage` 字段，看板会读不到 token 记录（显示为空）。请确保喂给它的日志带有真实的用量统计。

## 隐私（privacy）

- 不发起任何网络请求，不收集、不上传你的日志。
- 全部计算在浏览器本地完成。

## 许可证（license）

[MIT](LICENSE) © 2026 chengwerit
