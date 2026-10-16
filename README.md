# PixInsight Workflow Skill

A Codex/agent skill for carrying out astronomy image workflows through an already available PixInsight MCP connection. The main skill instructions are written in Chinese. It guides inspection, evidence-based parameter trials, preprocessing and integration, SHO mosaics, LRGB refinement, recovery, and delivery checks. It does not install PixInsight or provide an MCP server.

## Install

Invoke it with `$pixinsight-workflow`, for example: `Use $pixinsight-workflow to inspect my astronomy images and refine the result through the available PixInsight MCP.`

Copy `skills/pixinsight-workflow` into your Codex skills directory, usually `$CODEX_HOME/skills` (or `~/.codex/skills` when `CODEX_HOME` is unset). Install PixInsight and configure a compatible PixInsight MCP connection separately. Tool names and capabilities vary; the skill asks agents to inspect the tools available in their current environment.

## Scope and limits

The workflow requires actual processing and visual review through the available tools. Suggested parameters are starting points for measured trials, not universal presets. The WBPP branch in this release has not been validated end to end against a live PixInsight environment. Preserve original data, check storage and memory demands, and run one PI processing task at a time.

## Upstream references

The workflow may consult the public documentation and projects below for ideas. They are independent projects; this skill is not affiliated with or endorsed by their maintainers, and it does not redistribute their code.

- [pardovot/pixinsight-mcp](https://github.com/pardovot/pixinsight-mcp)
- [iftahs/pixinsight-mcp](https://github.com/iftahs/pixinsight-mcp)
- [AutoIntegrate](https://github.com/jarmoruuth/AutoIntegrate)
- [mxcoppell/pixinsight-connector-skills](https://github.com/mxcoppell/pixinsight-connector-skills)

## 中文说明

这是一个面向 Codex/Agent、基于现有 PixInsight MCP 的天文图像处理 skill；不包含 PixInsight 或 MCP 安装。将 `skills/pixinsight-workflow` 复制到 `$CODEX_HOME/skills`（未设置时通常为 `~/.codex/skills`），并另行安装 PixInsight、配置可用的 MCP。具体工具能力以当前环境实测为准。本发布版的 WBPP 分支尚未在实际 PixInsight 环境完成端到端验证；参数须按当前素材试跑，原始素材保持只读，注意内存与磁盘负荷，并逐个执行 PI 处理任务。
