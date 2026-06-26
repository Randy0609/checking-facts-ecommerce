# 事实洁癖 — 电商创业者版

**交付前,把 AI 编造或未经核实的数字、证言、资质拦下来。**

电商内容天然充满数字、证言、承诺——恰好是 AI 最爱编的东西。这个 Skill 在你交付销售页、详情页、推广文案、合作方案之前,逐条扫描每个具体事实,逼你做一个动作:给出处 / 降级为判断 / 标待核实 / 删掉。

## 快速安装

### OpenAI Codex（推荐）

Codex 支持本地 Agent Skills。用户级 Skill 推荐安装到 `$HOME/.agents/skills`。

用 Git 克隆安装：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/Randy0609/checking-facts-ecommerce.git \
  "$HOME/.agents/skills/checking-facts-ecommerce"
```

如果你不想保留 Git 仓库，也可以只下载 Skill 文件：

```bash
mkdir -p "$HOME/.agents/skills/checking-facts-ecommerce/agents"

curl -L https://raw.githubusercontent.com/Randy0609/checking-facts-ecommerce/main/SKILL.md \
  -o "$HOME/.agents/skills/checking-facts-ecommerce/SKILL.md"

curl -L https://raw.githubusercontent.com/Randy0609/checking-facts-ecommerce/main/agents/openai.yaml \
  -o "$HOME/.agents/skills/checking-facts-ecommerce/agents/openai.yaml"
```

验证方式：

```bash
ls "$HOME/.agents/skills/checking-facts-ecommerce/SKILL.md"
```

使用方式：

- 在 Codex CLI / IDE 里输入 `/skills` 查看是否出现。
- 也可以在提示词里直接写 `$checking-facts-ecommerce` 显式调用。
- 如果没有立刻出现，新开一个 Codex 会话；Codex App 也可以从命令菜单 Reload skills。

### Claude Code
```bash
mkdir -p ~/.claude/skills/checking-facts-ecommerce
cp SKILL.md ~/.claude/skills/checking-facts-ecommerce/SKILL.md
```

### OpenCode / 其他支持 `SKILL.md` 的 Agent 工具
```bash
mkdir -p ~/.config/opencode/skills/checking-facts-ecommerce
cp SKILL.md ~/.config/opencode/skills/checking-facts-ecommerce/SKILL.md
```

不同客户端的刷新机制可能不同。复制后如果没有立即出现,新开一个会话或按客户端要求刷新 Skills。

## 什么时候触发

写完要**交付**的内容时自动触发:
- 销售页 / 详情页 / 推广文案 / 投放素材
- 合作方案 / 对外 PPT / 融资 BP / 招商材料
- 含具体数字(GMV / 转化率 / ROI / 客单价 / 复购率)
- 客户证言 / 案例 / 达人背书
- 复用外部 AI(MANUS / GPT / Codex / DeepSeek)写的内容

也可以手动说:核查 / 查证 / 事实洁癖 / QC 一下 / 别编 / 这数字哪来的

**不触发**:普通聊天、头脑风暴、选品讨论、初稿构思。

## 核心机制

```
总闸:这条事实,我能不能指到出处?
 ↓ 指不到
四个出口(必须走一个):
 ✅ 有据 — 能指到出处,留
 🔻 降级 — 改成"约/估计/初步判断"
 ❓ 存疑 — 标【待核实】,回头查
 ✂️ 删  — 既无据又非必要,删掉
```

盯七类高危:数字统计 · 客户证言 · 创始人资质 · 产品认证 · 交付承诺 · 引用出处 · 归因断言。另加广告合规高风险用语初筛。

## 输出

每次审计输出两段:
1. **🚩 事实审计** — 逐条判定 + 缺什么出处
2. **✅ 清理版** — 落实修改后的全文,存疑项标【待核实】

## 致谢

- 设计受 [KKKKhazix/khazix-skills](https://github.com/KKKKhazix/khazix-skills) neat-freak 启发
- "四个出口"机制替代逐句打标签,逼动作而非贴字

## License

MIT
