# business-knowledge-update

基于本次需求、实际代码变更及相关测试，维护指定的业务知识库。将偏向代码分析记录的文档整理为便于开发人员阅读、便于 Agent 检索复用的中文业务知识。

本 Skill **仅手动触发**，不随需求开发或 Bug 修复自动执行。Skill 指令使用英文，生成和优化的知识文档使用中文。

## 安装

### 让 Codex 安装

在 Codex 中输入：

```text
使用 $skill-installer 安装 https://github.com/yuriwwwwwa/business-knowledge-update 中的 Skill，Skill 位于仓库根目录，安装名称为 business-knowledge-update。
```

### 手动安装

需要安装 Git。将仓库克隆到 Codex 的用户级 skills 目录。

Windows PowerShell：

```powershell
$skillsRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME "skills" } else { Join-Path $HOME ".codex/skills" }
git clone https://github.com/yuriwwwwwa/business-knowledge-update.git (Join-Path $skillsRoot "business-knowledge-update")
```

macOS / Linux：

```bash
git clone https://github.com/yuriwwwwwa/business-knowledge-update.git "${CODEX_HOME:-$HOME/.codex}/skills/business-knowledge-update"
```

安装后的目录结构：

```text
skills/
└── business-knowledge-update/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── README.md
```

如果目标目录已存在，请先检查已有安装，不要直接覆盖。安装后在下一轮尝试调用；如果未发现 Skill，开启新聊天再试。

## 使用

在完成业务变更、具备最终代码和相关测试证据后，在包含本次需求上下文的 Codex 聊天中调用：

```text
$business-knowledge-update <知识库文件或目录的路径>
```

Windows 示例：

```text
$business-knowledge-update E:\projectArchive\CCKG\cckg-toolkit\Concepts\CRM
```

也可以指定单个文档，路径含空格时建议加引号：

```text
$business-knowledge-update "E:\My Project\Concepts\订单管理.md"
```

路径是要维护的知识文档位置，不是业务代码仓库。Skill 会优先更新已有文档，仅在存在独立业务能力时新增文档。

如果当前聊天缺少上下文，请同时提供：

- 本次需求、已确认的业务规则和关键决策。
- 相关代码仓库或 worktree 路径。
- 本次变更的 Git 比较范围，例如基准分支、提交区间，以及是否包含未提交修改。
- 相关测试位置及已有运行结果。

示例：

```text
$business-knowledge-update E:\projectArchive\CCKG\cckg-toolkit\Concepts\CRM

请基于本次需求及已确认结论维护知识库。
代码仓库：E:\Projects\crm-worktree
比较范围：origin/develop...HEAD，并包含本次需求的未提交修改。
测试：请结合相关测试代码及本次聊天中已有的执行结果核验规则。
```

无法确定目标路径或比较范围时，Skill 会请求补充信息，不会把空的工作区 Diff 当作没有业务变更。

## 执行阶段

1. **业务规则提取**：读取需求上下文、Git Diff、最终源码和相关测试；检索已有业务术语、别名及规则文档，识别新增、修改、废弃的规则与受影响能力。
2. **知识文档生成**：优先更新已有内容，描述当前有效的行为、条件、优先级、例外及边界，维护规则 ID、术语和代码、测试关联。
3. **文档质量优化**：独立优化中文表达、业务组织和 Markdown 格式；不得改变上一阶段确定的业务规则、条件、状态和结果。
4. **规则一致性检查**：校验文档与代码、测试及已确认要求的一致性，检查可追溯性、链接与格式，并汇报结果。

## 输出与边界

完成后汇报更新的文档、涉及的业务能力、规则变化、主要结构调整及待确认事项；若无需更新，说明原因。

- 仅修改受本次需求影响的知识文档，不修改业务代码。
- 维护现行规则，不堆积需求迭代历史，也不重复沉淀等价业务能力。
- 保留现有业务 ID、规则 ID、术语引用和有效证据关联。
- 冲突、歧义和证据不足的内容标记待确认，不根据经验补全或写成确定事实。
- 必要时才查阅语雀历史需求；访问能力和权限需由使用环境提供。
- 区分已阅读的测试与实际运行通过的测试，不宣称执行了未执行的验证。
- 不自动发布远程文档；远程发布需要明确指令。

完整执行规范见 [SKILL.md](SKILL.md)。仅手动触发的配置见 [agents/openai.yaml](agents/openai.yaml)。
