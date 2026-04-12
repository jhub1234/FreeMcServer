# FreeMcServer 自动续订

> ⭐ 觉得有用？给个 Star 支持一下！
>
> 注册地址：[https://freemcserver.net](https://freemcserver.net)

自动续订 [FreeMcServer](https://freemcserver.net) 免费 Minecraft 服务器，防止到期被删除。

通过 GitHub Actions 定时运行，使用 SeleniumBase 模拟浏览器操作完成续订，支持多账号、Telegram 通知、代理连接。

## 功能

- 自动登录并续订所有服务器
- 续订成功后自动启动已关机的服务器
- 自动处理 Cloudflare Turnstile 验证和 AdBlocker 检测
- 支持多账号批量处理
- Telegram 机器人推送续订结果（含截图）
- 支持 Hysteria2 代理
- 每 3 小时自动执行，也可手动触发

## 配置

### Secrets 说明

在仓库 `Settings → Secrets and variables → Actions` 中添加：

| Secret 名称 | 必填 | 说明 | 示例 |
|---|---|---|---|
| `FREEMCSERVER` | ✅ | FreeMcServer 账号信息 | 见下方格式 |
| `TG_BOT_TOKEN` | ❌ | Telegram Bot Token | `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11` |
| `TG_CHAT_ID` | ❌ | Telegram Chat ID | `123456789` |
| `HY2_URL` | ✅ | Hysteria2 代理地址 | `hysteria2://password@server:port?sni=example.com` |

### FREEMCSERVER 格式

每行一个账号，邮箱和密码之间用 `-----` 分隔：

```
admin@example.com-----your_password_123
user@domain.com-----another_password
```

## 使用

### GitHub Actions（推荐）

1. Fork 本仓库
2. 配置 `FREEMCSERVER` Secret
3. 脚本会按 cron 计划自动运行（每 3 小时）
4. 也可在 Actions 页面手动触发 `workflow_dispatch`

## 注意事项

- Cloudflare 验证存在一定失败概率，脚本内置多轮重试机制
- 工作流自动清理历史运行记录，仅保留最近 2 次
- 日志中的邮箱、服务器 ID、URL 均做脱敏处理

---

**⚠️ 免责声明**：本脚本仅供学习交流使用，使用者需遵守 [FreeMcServer](https://freemcserver.net) 的服务条款。因使用本脚本造成的任何问题，作者不承担任何责任。
```
