# Windows 安装：Codex CLI

## 安装方式选择

推荐优先顺序：

1. 官方安装脚本：适合希望一步安装的用户。
2. npm 全局安装：适合已经配置好 Node.js 和 npm 的用户。
3. GitHub release：适合需要手动下载二进制文件的环境。

如果在中国大陆网络环境下某一种方式失败，不要急着反复重试。先确认是下载失败、证书失败、代理失败，还是权限失败。

## 方式一：官方安装脚本

PowerShell:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -Command "irm https://chatgpt.com/codex/install.ps1 | iex"
```

安装完成后验证：

```powershell
codex --version
codex --help
```

更谨慎的做法是先下载脚本、人工检查，再执行：

```powershell
irm https://chatgpt.com/codex/install.ps1 -OutFile install-codex.ps1
Get-Content .\install-codex.ps1
powershell -NoProfile -ExecutionPolicy Bypass -File .\install-codex.ps1
```

## 方式二：npm 全局安装

先确认 Node.js 和 npm 可用：

```powershell
node -v
npm -v
```

安装 Codex CLI：

```powershell
npm install -g @openai/codex
```

验证：

```powershell
where.exe codex
codex --version
```

如果提示权限不足，可以尝试以管理员身份打开 PowerShell，或配置 npm 的用户级全局安装目录。

## 方式三：GitHub release 手动安装

适合公司网络无法稳定访问 npm，但可以通过浏览器或内部软件源下载 release 的情况。

基本步骤：

1. 打开 OpenAI Codex 官方 GitHub 仓库。
2. 在 Releases 中下载 Windows 对应版本。
3. 解压到固定目录，例如 `C:\Tools\codex`。
4. 将该目录加入用户级 `PATH`。
5. 重新打开 PowerShell 后运行 `codex --version`。

## 常见安装失败

### npm 下载失败

现象：

```text
ETIMEDOUT
ECONNRESET
ENOTFOUND
```

优先检查：

- 当前 PowerShell 是否配置了代理。
- npm 是否配置了 proxy 和 https-proxy。
- 公司网络是否允许访问 npm registry。

### codex 命令无法识别

优先检查：

```powershell
where.exe codex
npm config get prefix
```

可能原因：

- 安装目录没有加入 `PATH`。
- 安装完成后没有重新打开 PowerShell。
- npm 全局目录与当前用户环境变量不一致。

### 证书错误

如果出现 `certificate`、`self signed certificate`、`unable to verify` 等错误，通常和公司代理证书有关。

不要直接关闭 TLS 校验作为长期方案。更好的做法是联系 IT 获取公司根证书，并按公司要求配置 Node.js、Git 或系统证书。
