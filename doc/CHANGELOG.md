---
name: project-changelog
description: 变更日志
metadata:
  version: "1.0.0"
  lang: "zh-CN"
---

# 变更日志

## 多语言

**简体中文** | [English](en/CHANGELOG.md) | [Español](es/CHANGELOG.md)

## 文档

- 项目概览: [README](../README.md)

- 设计思路: [DESIGN](DESIGN.md)

- 项目状态: [LOG](LOG.md)
- 历史记录: [HISTORY](HISTORY.md)
- 变更日志: [CHANGELOG](CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## 变更日志

### user-v1.0(V3)- 2026-11-05

- 新增: 本仓库的首个 Release, 提供完整 9008 刷机包分卷, `SHA256SUMS.txt` 和模块列表.
- 说明: BP1A 底包线从 v1.0 起独立编号, 补丁集与 AP3A 线的 user-v1.4 对齐.
- 变更: 人脸解锁按官方 BP1A 的 `services.jar` 重新适配.
- 变更: 隐藏导航栏换新方案: 启动器收起高度 1dp, 底部是 Taskbar 时不强切导航模式, 修复"上滑多任务中途掉头后 App 点不动, 侧滑失效".
