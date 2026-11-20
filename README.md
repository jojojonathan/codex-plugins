# Jonathan 的 Codex 插件市场

## 安装 CodeGraph

CodeGraph 让 Codex 从本地项目索引中查找符号、追踪调用关系并分析改动影响。插件使用当前环境 `PATH` 中的 `codegraph` 启动 MCP 服务。[CodeGraph 上游项目](https://github.com/colbymchenry/codegraph)

1. 在运行 Codex 的环境中执行 `codegraph --version`。如果还未安装，可使用 `npm install -g @colbymchenry/codegraph`，也可使用上游提供的平台安装包。使用 WSL 运行 Codex 时，在对应的 Linux 发行版中执行这一步。
2. 在已获得此 GitHub 仓库读取权限的环境中添加市场并安装插件。

   ```sh
   codex plugin marketplace add jojojonathan/codex-plugins
   codex plugin add codegraph@jonathan-plugins
   ```

3. 进入想要分析的项目根目录，执行一次 `codegraph init` 建立索引。随后在该目录打开新的 Codex 会话，例如问「用 CodeGraph 找出谁调用了 `handleRequest`」，并将函数名换成项目中的实际符号。

## 添加插件

将插件放入 `plugins/<插件名>/`，在插件根目录的 `plugin.json` 中填写名称、版本和说明。提供 MCP 服务时，在同目录的 `mcp.json` 中声明启动方式。最后在市场清单中登记插件，将 `source.path` 设为相对仓库根目录的 `./plugins/<插件名>`。[市场清单](.agents/plugins/marketplace.json) · [OpenAI 插件打包规范](https://developers.openai.com/plugins/build/plugins)
