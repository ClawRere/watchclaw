# WatchClaw 🐾

OpenClaw 网关监控与自动重启工具，包含记忆备份系统。

## 功能

- 🔍 **网关监控**: 实时监控 OpenClaw 网关状态
- 🔄 **自动重启**: 网关异常时自动重启
- 💾 **记忆备份**: 备份和恢复 OpenClaw 完整状态
- 📊 **状态报告**: 定期推送运行状态

## 快速开始

### 备份 OpenClaw

```powershell
# 完整备份
.\watchclaw.ps1 backup

# 压缩备份
.\watchclaw.ps1 backup -Compress

# 查看备份列表
.\watchclaw.ps1 list
```

### 恢复 OpenClaw

```powershell
# 从默认位置恢复
.\watchclaw.ps1 restore

# 从指定路径恢复
.\watchclaw.ps1 restore -Source "D:\backups\openclaw-backup"
```

### 监控网关

```powershell
# 启动监控服务
.\watchclaw.ps1 monitor
```

## 备份内容

### 核心数据
- `~/.openclaw/workspace/` - 工作区文件
  - MEMORY.md - 长期记忆
  - SOUL.md - 身份定义
  - USER.md - 用户信息
  - AGENTS.md - 操作规则
  - skills/ - 技能目录
  - memory/ - 日常记忆
- `~/.openclaw/openclaw.json` - 主配置文件

### 可选数据
- `~/.openclaw/agents/` - Agent 配置
- `~/.openclaw/cron/` - 定时任务
- `~/.openclaw/logs/` - 日志文件

## 自动化

### Windows 任务计划程序

```powershell
# 每天凌晨 2 点自动备份
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
  -Argument "-ExecutionPolicy Bypass -File C:\path\to\watchclaw.ps1 backup -Compress"
$trigger = New-ScheduledTaskTrigger -Daily -At 2am
Register-ScheduledTask -TaskName "WatchClaw Backup" -Action $action `
  -Trigger $trigger -RunLevel Highest
```

## 注意事项

⚠️ **恢复前请停止网关**：
```bash
openclaw gateway stop
```

✅ **恢复后重启网关**：
```bash
openclaw gateway restart
```

## 版本历史

- **v1.0.0** (2026-03-08)
  - 初始版本
  - 支持完整备份/恢复
  - 支持压缩备份

## 许可证

MIT License

## 作者

ClawX @ OpenClaw Community
