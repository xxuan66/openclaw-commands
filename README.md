# 🦞 OpenClaw 常用指令速查手册

> 📚 OpenClaw 命令行快速参考，日常操作一查即用

[![Updated](https://img.shields.io/badge/updated-2026--03--27-blue)](https://github.com/xxuan66/openclaw-commands)
[![License](https://img.shields.io/badge/license-MIT-blue)](https://github.com/xxuan66/openclaw-commands/blob/main/LICENSE)
[![Stars](https://img.shields.io/github/stars/xxuan66/openclaw-commands?style=social)](https://github.com/xxuan66/openclaw-commands/stargazers)

---

**⭐ 如果这个项目对你有帮助，请给个 Star！**

---

## 📋 目录

- [Gateway 管理](#gateway-管理)
- [模型配置](#模型配置)
- [会话管理](#会话管理)
- [插件管理](#插件管理)
- [Cron 定时任务](#cron-定时任务)
- [消息发送](#消息发送)
- [配置管理](#配置管理)
- [故障排查](#故障排查)

---

## Gateway 管理

```bash
# 查看 Gateway 状态
openclaw gateway status

# 启动 Gateway
openclaw gateway start

# 重启 Gateway（配置变更后）
openclaw gateway restart

# 停止 Gateway
openclaw gateway stop

# 查看 Gateway 日志
openclaw logs

# 查看健康状态
openclaw health
```

---

## 模型配置

```bash
# 查看已配置的模型
openclaw models list

# 切换默认模型
openclaw models set bailian/qwen3.5-plus

# 添加 fallback 模型
openclaw models fallbacks add <provider>/<model-name>

# 查看 fallback 列表
openclaw models fallbacks list

# 清除 fallback
openclaw models fallbacks clear

# 查看当前模型配置
openclaw config get agents.defaults.model.primary
```

---

## 会话管理

```bash
# 列出所有会话
openclaw sessions list

# 查看会话历史
openclaw sessions history --session-id <id>

# 发送消息到会话
openclaw sessions send --session-id <id> --message "你好"

# 删除会话
openclaw sessions delete --session-id <id>
```

---

## 插件管理

```bash
# 列出已安装插件
openclaw plugins list

# 启用插件
openclaw plugins enable feishu

# 禁用插件
openclaw plugins disable qqbot

# 查看插件状态
openclaw plugins status
```

---

## Cron 定时任务

```bash
# 列出所有定时任务
openclaw cron list

# 添加定时任务
openclaw cron add --schedule "0 9 * * *" --command "echo 早上好"

# 删除定时任务
openclaw cron remove --id <job-id>

# 查看任务状态
openclaw cron status
```

---

## 消息发送

```bash
# 发送消息到飞书
openclaw message send --channel feishu --target <chat_id> --message "Hello"

# 发送消息到 Telegram
openclaw message send --channel telegram --target @username --message "Hello"

# 发送带图片的消息
openclaw message send --channel feishu --target <chat_id> --media /path/to/image.png
```

---

## 配置管理

```bash
# 查看配置
openclaw config get models.providers

# 设置配置
openclaw config set models.providers.<provider>.apiKey "sk-xxx"

# 删除配置
openclaw config unset models.providers.<provider>

# 编辑配置文件
openclaw config edit
```

---

## 故障排查

### Gateway 无法启动

```bash
# 检查端口占用
lsof -i :10949

# 强制重启
openclaw gateway --force restart
```

### 模型调用失败

```bash
# 检查模型配置
openclaw config get models.providers

# 测试模型
openclaw agent -m "测试" --session-id test-$(date +%s)

# 查看 fallback 状态
openclaw models fallbacks list
```

### 插件不工作

```bash
# 检查插件状态
openclaw plugins status

# 重新启用插件
openclaw plugins disable <name> && openclaw plugins enable <name>

# 查看插件日志
openclaw logs | grep <plugin-name>
```

### Cron 任务不触发

```bash
# 查看任务执行历史
openclaw cron runs <job-id>

# 手动触发一次验证
openclaw cron run <job-id>

# 确认 Gateway 在运行（cron 依赖 Gateway）
openclaw gateway status
```

### Token / 认证过期

```bash
# 重新登录
openclaw auth login

# 查看当前认证状态
openclaw auth status

# 刷新 Token
openclaw auth refresh
```

---

## 快速命令别名

添加到 `~/.bashrc`：

```bash
# OpenClaw 快捷命令
alias oc='openclaw'
alias oc-status='openclaw gateway status'
alias oc-restart='openclaw gateway restart'
alias oc-models='openclaw models list'
alias oc-logs='openclaw logs --tail 100'
```

---

## 🔗 相关链接

| 链接 | 描述 |
|------|------|
| [📖 OpenClaw 官方文档](https://docs.openclaw.ai) | 完整文档 |
| [🦞 OpenClaw GitHub](https://github.com/openclaw/openclaw) | 官方仓库 |
| [🛒 ClawHub 技能市场](https://clawhub.ai) | 下载 Skill |
| [💬 Discord 社区](https://discord.com/invite/clawd) | 加入社区 |

---

## 📝 贡献

欢迎提交 Issue 和 PR！

- 发现错误？[提交 Issue](https://github.com/xxuan66/openclaw-commands/issues)
- 有新指令？[提交 PR](https://github.com/xxuan66/openclaw-commands/pulls)

---

**最后更新:** 2026-03-25  
**维护者:** [@xxuan66](https://github.com/xxuan66)

## 🆕 2026-03-25 更新

- ✅ 故障排查新增「Cron 任务不触发」和「Token 过期」两节
- ✅ 更新 badge 日期至 2026-03-25

---

## 🆕 2026-03-24 更新

- ✅ 更新 badge 日期至 2026-03-24
- ✅ 小幅优化文档格式

---

## 📊 仓库统计

> 统计数据由 OpenClaw Bot 每日自动更新，保存在本地 `github-stats/` 目录，**不上传到 GitHub** 以保护隐私。

