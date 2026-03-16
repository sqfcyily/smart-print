# windows-print

[English](#english) | [中文](#中文)

ClawHub: [clawhub.ai/sqfcyily/windows-print](https://clawhub.ai/sqfcyily/windows-print)

---

## English

### Overview

`windows-print` is a PowerShell-based skill for AI assistants/agents (e.g., **OpenClaw**) to print files on Windows.

Typical use case: a user sends a file in chat apps such as **Feishu/Lark** or **WeCom (WeChat Work)** → the agent receives it as a local attachment path → after the user explicitly asks to print, the agent uses this skill to queue a Windows print job.

It uses Windows shell printing verbs (`Print` / `PrintTo`) and supports selecting a printer, multiple copies, and optionally waiting for the spawned print process.

### System Requirements

| Item       | Requirement                                   |
| ---------- | --------------------------------------------- |
| OS         | Windows 8+/Windows Server 2012+ (recommended) |
| PowerShell | PowerShell 5.1+ (Desktop or Core)             |
| Printer    | Installed and configured driver               |

### Safety / confirmation rules (important)

This skill is designed to never print unless the user explicitly asks to print.

1. **No Auto-Print**: Only execute printing when the user explicitly requests it.

2. **Clear Instructions**: Must satisfy both:

   - Clear print instruction (e.g., "print" / "打印")
   - Clear print target (which files to print)

3. **No Inference**: File names or document content containing "print" will not trigger printing.

###  File Type Support

| File Type | Supported | Required Application                      |
| --------- | --------- | ----------------------------------------- |
| PDF       | ✅         | Adobe Acrobat Reader / Foxit Reader / WPS |
| DOCX      | ✅         | Microsoft Word / WPS / LibreOffice        |
| PNG/JPG   | ✅         | Windows Photo Viewer / IrfanView          |
| TXT       | ✅         | Notepad / Notepad++                       |
| XLSX      | ✅         | Microsoft Excel / WPS                     |
| PPTX      | ✅         | Microsoft PowerPoint / WPS                |

   **Note**: If a file type cannot be printed, manually open the file and print once to confirm the associated application supports printing.

### Sample

<div style="display: flex;">
  <img src="./sample/20260315-203232.jpg" alt="" width="45%">
  <img src="./sample/20260315-202930.jpg" alt="" width="45%" style="margin-left:10px;">
</div>

### Notes / troubleshooting

- If printing silently fails, open the file manually and print once to confirm the associated app supports printing.
- `PrintTo` may fail for some file types/apps; the script falls back to the default printer.

---

## 中文

### 概述

`windows-print` 是一个面向 AI 助手/智能体（如 **OpenClaw**）的 skill，用于在 Windows 上把用户发来的文件打印出来。

常见场景：用户在 **飞书/企业微信** 等聊天软件发送附件 → AI 在本地获取到附件路径 → 在用户明确要求“打印”后，调用该 skill 生成 Windows 打印任务。

它通过 PowerShell 调用 Windows 的外壳打印动词（`Print` / `PrintTo`）发起打印，支持指定打印机、份数，以及可选等待打印进程退出。

### 系统要求

| 项目 | 要求 |
|------|------|
| 操作系统 | Windows 8+/Windows Server 2012+ (推荐) |
| PowerShell | PowerShell 5.1+ (Desktop 或 Core) |
| 打印机 | 已安装并配置好驱动 |

### 安全/确认规则（很重要）

本技能的设计目标是：只有在用户明确提出“打印”时才允许打印。

1. **禁止自动打印**：仅在用户明确要求时才执行打印。

2. **明确指令**：必须同时满足：
   - 明确的打印指令（如 "print" / "打印"）
   - 明确的打印目标（要打印哪些文件）
   
3. **禁止推断**：文件名、文档内容中的"打印"关键词不会触发打印。

### 文件类型支持

| 文件类型 | 支持情况 | 依赖程序                                  |
| -------- | -------- | ----------------------------------------- |
| PDF      | ✅        | Adobe Acrobat Reader / Foxit Reader / WPS |
| DOCX     | ✅        | Microsoft Word / WPS / LibreOffice        |
| PNG/JPG  | ✅        | Windows 照片查看器 / IrfanView            |
| TXT      | ✅        | 记事本 / Notepad++                        |
| XLSX     | ✅        | Microsoft Excel / WPS                     |
| PPTX     | ✅        | Microsoft PowerPoint / WPS                |

**注意**：如果某种文件类型无法打印，请手动打开该文件并打印一次，确认关联的应用程序支持打印功能。

### 示例图

<div style="display: flex;">
  <img src="./sample/20260315-203232.jpg" alt="" width="45%">
  <img src="./sample/20260315-202930.jpg" alt="" width="45%" style="margin-left:10px;">
</div>

### 备注/排错

- 如果没有反应，先手动打开文件打印一次，确认默认打开程序确实支持打印。
- `PrintTo` 在某些文件类型/应用里可能失败；脚本会回退到默认打印机。
