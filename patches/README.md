# 自用定制补丁存档

## retry-failed-msg.patch

- 功能：聊天面板里最新一轮请求失败时，在最后一条用户消息下方显示「发送失败 · ↻ 重试」卡片；点击后不重发用户消息（消息已落库），仅以最新 API 配置重新请求一次 AI 回复。
- 基线：上游 `Sui-IB/InternalBeyond-Mobile` 提交 `949669c`（V1.3.0b）。
- 范围：仅改 `index.html`，+30 行，零新增 CSS（复用 `.ws-op-card.fail` / `.ws-file-btn`）；仅一对一聊天生效，群聊与手动中止不显示。
- 同步上游后若该定制被冲掉，在仓库根目录执行：

  ```bash
  git apply --3way patches/retry-failed-msg.patch
  ```

  若上游改了同一区域导致无法直接应用，按补丁里的函数锚点（`genReply` 的 try 开头与 catch 非中止分支、`_showRetryPillM`）手动重挂即可。若上游官方实现了同款功能，直接弃用本补丁。
