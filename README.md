# Jonathan 的 Codex 插件市场

## 安装 CodeGraph

CodeGraph 让 Codex 从本地项目索引中查找符号、追踪调用关系并分析改动影响。插件使用当前环境 `PATH` 中的 `codegraph` 启动 MCP 服务。服务启动和单次工具调用的超时均为 30 秒。[CodeGraph 上游项目](https://github.com/colbymchenry/codegraph)

1. 在运行 Codex 的环境中执行 `codegraph --version`。如果还未安装，可使用 `npm install -g @colbymchenry/codegraph`，也可使用上游提供的平台安装包。使用 WSL 运行 Codex 时，在对应的 Linux 发行版中执行这一步。
2. 在已获得此 GitHub 仓库读取权限的环境中添加市场并安装插件。

   ```sh
   codex plugin marketplace add jojojonathan/codex-plugins
   codex plugin add codegraph@jonathan-plugins
   ```

3. 进入想要分析的项目根目录，执行一次 `codegraph init` 建立索引。随后在该目录打开新的 Codex 会话，例如问「用 CodeGraph 找出谁调用了 `handleRequest`」，并将函数名换成项目中的实际符号。

## 安装腾讯文档

在运行 Codex 的环境中设置 `TENCENT_DOCS_TOKEN`，值为腾讯文档签发的原始令牌。插件会自动加上 `Bearer` 前缀。Windows 桌面端可在「用户环境变量」中设置后重新启动 Codex；使用 WSL 运行 Codex CLI 时，在对应的 Linux 环境中设置。

首次使用此市场时运行 `codex plugin marketplace add jojojonathan/codex-plugins`。已添加市场时，运行 `codex plugin marketplace upgrade jonathan-plugins` 刷新插件列表。然后安装插件：

```sh
codex plugin add tencent-docs@jonathan-plugins
```

在新的 Codex 会话中提供有权访问的腾讯文档链接，例如「用腾讯文档总结这份文档的要点」。

## 安装 Next AI Draw.io

在运行 Codex 的环境中准备 Node.js 18 或更高版本，并确认 `npx --version` 可用。插件通过 `npx -y @next-ai-drawio/mcp-server@latest` 启动绘图服务。首次运行需要联网下载，Codex 最多等待 60 秒启动服务。[上游使用说明](https://github.com/DayuanJiang/next-ai-draw-io/tree/main/packages/mcp-server#readme)

首次使用此市场时运行 `codex plugin marketplace add jojojonathan/codex-plugins`；已添加市场时运行 `codex plugin marketplace upgrade jonathan-plugins`。然后安装插件：

```sh
codex plugin add next-ai-drawio@jonathan-plugins
```

在新的 Codex 会话中试试「用 draw.io 画出当前项目的架构图」。你可以在浏览器中预览和编辑图表，也可以让 Codex 导出 `.drawio` 文件。

## 添加插件

将插件放入 `plugins/<插件名>/`，在插件清单中填写名称、版本和说明。CodeGraph 使用 Codex 格式，由 `.codex-plugin/plugin.json` 引用插件根目录的 `.mcp.json`。最后在市场清单中登记插件，将 `source.path` 设为相对仓库根目录的 `./plugins/<插件名>`。[市场清单](.agents/plugins/marketplace.json) · [OpenAI 插件打包规范](https://developers.openai.com/plugins/build/plugins)
