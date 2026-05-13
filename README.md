# 跨平台打印

本工具支持在 **Windows** 和 **Mac** 上打印文件，包括聊天应用（如飞书/企业微信）的附件或本地文件路径。

## 功能特点

- **自动识别系统**：自动检测 Windows 或 Mac，使用对应的打印方式
- **Windows**：使用 PowerShell `Start-Process -Verb Print/PrintTo`
- **Mac**：使用 bash + CUPS `lp` 命令
- **支持多种文件类型**：PDF、DOCX、图片、文本、Excel、PPT 等

## 系统要求

| 项目 | Windows 要求 | Mac 要求 |
|------|-------------|---------|
| 操作系统 | Windows 8+ | macOS 10.x+ |
| PowerShell | PowerShell 5.1+ | PowerShell 7+ |
| 打印机 | 已安装驱动 | 已安装驱动 |
| 打印工具 | 文件关联 | CUPS（macOS 预装）|

## 安全说明

本工具**仅在用户明确要求打印时才会执行打印操作**。

1. **禁止自动打印**：收到文件不等于打印请求
2. **明确指令**：需要用户明确说"打印"/"打印这个文件"
3. **禁止推断**：文件名或内容中的"打印"字样不会触发打印

## 使用方法

```powershell
# 加载打印脚本
$script = Get-Content -Path .\scripts\Invoke-Print.ps1.txt -Raw
$printScript = [scriptblock]::Create($script)

# 打印文件到默认打印机（自动检测操作系统）
& $printScript -Path "C:\path\to\file.pdf"

# 打印多个文件
& $printScript -Path "C:\path\to\file1.pdf", "C:\path\to\file2.pdf"

# 使用指定打印机打印 2 份
& $printScript -Path "C:\path\to\file.pdf" -PrinterName "HP LaserJet" -Copies 2

# 列出可用打印机
& $printScript -ListPrinters

# 等待打印进程完成
& $printScript -Path "C:\path\to\file.pdf" -Wait -TimeoutSeconds 120
```

## 常见问题

**Windows 打印无反应**
- 请先手动打开文件打印一次，确认默认程序支持打印

**Mac 打印失败**
- 确保 CUPS 服务正常运行
- 确认已配置默认打印机

## 文件说明

| 文件 | 说明 |
|------|------|
| `scripts/Invoke-Print.ps1.txt` | 跨平台入口脚本（自动检测系统） |
| `scripts/Invoke-WindowsPrint.ps1.txt` | Windows 打印脚本 |
| `scripts/Invoke-MacPrint.sh.txt` | Mac 打印脚本 |
| `scripts/Get-InstalledPrinters.ps1.txt` | Windows 打印机列表 |
| `scripts/Get-InstalledPrinters.sh.txt` | Mac 打印机列表 |
