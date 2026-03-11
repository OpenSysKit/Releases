# OpenSysKit Releases

统一发版仓库 — 手动触发工作流，完成全链路构建（前端 + 后端 + 驱动），生成便携版 ZIP 和 MSI 安装包，自动发布 GitHub Release。

## 使用方法

1. 编辑 `release-notes.json`，填入版本号和功能说明
2. 提交并推送到 main
3. 在 GitHub Actions 页面手动触发 `Release` 工作流，输入版本号（如 `v1.0.0`）
4. 工作流自动完成：
   - 构建前端（.NET 8 Avalonia）
   - 构建驱动（CMake WDK）
   - 构建后端（Go，注入前端 SHA256）
   - 打包便携版 ZIP
   - 构建 MSI 安装包（中文引导页面）
   - 创建 Release 并上传产物

## 产物

| 文件 | 说明 |
|------|------|
| `OpenSysKit-win-x64.zip` | 便携版（解压即用） |
| `OpenSysKit-Setup-x64.msi` | 安装版（中文引导，含快捷方式和开机自启选项） |

## 仓库结构

```
release-notes.json          # 功能说明 JSON，工作流据此生成 Release Notes
installer/                  # WiX MSI 安装包项目
  Package.wxs               # 主安装描述
  Variables.wxi             # 版本号等变量
  zh-CN.wxl                 # 中文本地化
  License.rtf               # 许可协议
.github/workflows/
  release.yml               # 全链路构建 + 发版工作流
```
