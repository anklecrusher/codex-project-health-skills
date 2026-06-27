# Codex 项目健康检查 Skills

这是一组面向 Codex 的轻量 Skill，用来让长任务和复杂项目保持清晰：

- `project-health-audit`：扫描项目结构、入口文件、Skill 常驻面和导航健康度。
- `thread-handoff`：把长任务压缩成保真的上下文摘要，并可选投递给新线程。

英文文档：[README.md](README.md)

## 解决什么问题

AI 编程和知识库项目常见的问题不是“模型不聪明”，而是上下文和项目结构慢慢变乱：

- 项目规则越来越多，但不知道哪个文件才是入口；
- 常驻 Skill、工具和 MCP 太多，污染上下文；
- Obsidian vault、代码仓库和自动化目录被同一套标准误判；
- 长线程经过压缩或重启后丢失关键决策；
- 新线程拿到的是一大段历史，而不是能直接继续执行的交接单。

这两个 Skill 把事情拆开：

1. 先只读检查项目健康度；
2. 再把当前任务状态整理成可交接的 handoff；
3. 如果线程管理工具可用，并且用户要求交接，就把 handoff 直接发给新线程。

## 包含的 Skill

### `project-health-audit`

适合让 Codex 对一个 repo、workspace、Obsidian vault 或混合项目做只读健康检查。

它会检查：

- 项目边界和真实根目录；
- `AGENTS.md`、`CLAUDE.md`、`README.md`、`schema/`、`docs/` 等规则入口；
- `index`、`overview`、`log`、changelog 等导航面；
- source 和 reference 的回链、互链、薄弱链接；
- active skill 目录、重复 Skill、过宽的常驻 Skill；
- 把非代码项目误判成代码仓库时产生的假阳性。

输出会分成：

- 已确认问题；
- 可能是假阳性的提示；
- 可选优化；
- 需要用户确认后才能执行的动作。

### `thread-handoff`

适合在长任务、上下文压缩、换线程、交给另一个 agent 继续时使用。

它的核心目标是“压缩但不失真”：保留决策、约束、证据、当前状态和下一步，同时丢掉噪声。它不是项目健康检查 Skill。

它会整理：

- 当前角色和范围；
- 目标；
- 必须保留的约束；
- 当前状态；
- 已完成工作；
- 验证状态；
- 阻塞和风险；
- 下一步最安全动作；
- 不要重复的失败路径；
- 可能遗漏或尚未核验的上下文；
- 新线程可以忽略的旧上下文。

如果用户要求把 handoff 发给新线程或已有线程，这个 Skill 应该优先使用可用的 Codex 线程管理工具；如果没有投递工具或投递失败，再降级为可复制的 handoff 摘要。

## 安装

克隆仓库：

```bash
git clone https://github.com/anklecrusher/codex-project-health-skills.git
```

复制到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R codex-project-health-skills/skills/project-health-audit ~/.codex/skills/
cp -R codex-project-health-skills/skills/thread-handoff ~/.codex/skills/
```

Windows PowerShell：

```powershell
$skills = Join-Path $env:USERPROFILE .codex\skills
New-Item -ItemType Directory -Force -Path $skills | Out-Null
Copy-Item -Recurse -Force .\codex-project-health-skills\skills\project-health-audit $skills
Copy-Item -Recurse -Force .\codex-project-health-skills\skills\thread-handoff $skills
```

如果 Codex 当前线程没有立即看到新 Skill，重启 Codex 或新开线程。

## 怎么使用

示例提示词：

```text
Use project-health-audit to audit this workspace. Stay read-only and separate confirmed issues from false positives.
```

```text
Use project-health-audit to check whether my always-on skills are too broad or duplicated.
```

```text
Use thread-handoff to create a clean handoff for a new thread. Include verified work, open risks, and the next safest step.
```

```text
Use thread-handoff to compress this long task before context compaction.
```

## 什么情况下使用

使用 `project-health-audit`：

- 接手陌生项目时；
- 项目规则、入口文件或目录边界不清楚时；
- 知识库、仓库或自动化目录疑似结构漂移时；
- Codex Skill、MCP 或常驻上下文太吵时；
- 想先拿到审计报告，再决定是否清理时。

使用 `thread-handoff`：

- 当前线程已经很长；
- 任务已经或即将发生上下文压缩；
- 需要新线程或另一个 agent 接着做；
- 当前对话里有重要决策，但混在大量探索记录里。
- 希望旧线程在交接前检查摘要是否覆盖了继续任务所需的重要上下文。

两个一起用：

- 先用 `project-health-audit` 检查项目；
- 如果发现当前线程也变乱，再用 `thread-handoff` 生成交接单。

## 安全边界

这两个 Skill 都默认保守：

- 默认只读；
- 不在未确认时删除或移动文件；
- 把真实问题和项目特有例外分开；
- 不把缺少 Makefile、测试命令或 git 仓库一律判为失败；
- 保留验证证据，而不是只相信“已经完成”的说法；
- 不在线程管理工具成功前声称“已经发送到新线程”。

## 仓库结构

```text
skills/
  project-health-audit/
    SKILL.md
    agents/openai.yaml
    references/scan-checklist.md
  thread-handoff/
    SKILL.md
    agents/openai.yaml
    references/handoff-format.md
```

## License

MIT
