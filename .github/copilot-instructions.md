# Global Copilot Instructions

## ⚠️ 绝对规则一：所有思考和输出必须使用中文

**无一例外**，所有输出——包括推理过程（thinking）、解释说明、代码注释之外的文字、提问——必须使用**中文**。

```
IF:   你正在生成任何输出（思考、回复、解释、提问）
THEN: 必须使用中文 — 无一例外
```

**禁止行为：**
- ❌ 用英文写回复正文（代码、命令、专有名词除外）
- ❌ 用英文写推理过程或 thinking
- ❌ 用英文向用户提问或解释

**适用场景（无一例外）：**
- ✅ 简短的一句话回答
- ✅ 代码解释和任务说明
- ✅ 计划制定和确认步骤
- ✅ 报错说明和"我不知道"的回复
- ✅ 字面上每一条回复

---

## ⚠️ 绝对规则二：每次回复结束前必须调用 ask_user 工具

**无一例外**，每次回复的**最后一个动作**必须是调用 `ask_user` 工具。

```
IF:   你即将结束对用户的任何一条回复
THEN: 必须将 ask_user 工具调用作为最后一个动作 — 无一例外
```

**禁止行为：**
- ❌ 用"还有什么需要帮忙的？"等纯文本结束回复，而不调用 `ask_user`
- ❌ 用总结段落结束回复而不调用 `ask_user`
- ❌ 因为"问题很简单"或"任务已完成"就跳过 `ask_user`
- ❌ 用文字提问代替调用 `ask_user` 工具
- ❌ 以任何理由、任何方式结束回复而不调用 `ask_user`

**适用场景（无一例外）：**
- ✅ 简短的一句话回答
- ✅ 代码补全和解释
- ✅ 任务完成（如编辑文件后）
- ✅ 报错或"我不知道"的回复
- ✅ 计划制定或确认步骤
- ✅ 字面上每一条回复，没有例外

## ⚠️ 绝对规则三：所有 Python/pip 相关命令必须在 conda 环境中执行

**无一例外**，任何涉及 Python 解释器、pip 安装、包管理或脚本运行的命令，必须先激活指定的 conda 环境，再在该环境内执行。

```
IF:   你即将执行任何 python / pip / pytest / jupyter 或其他依赖 Python 环境的命令
THEN: 必须先执行 conda activate <env_name>，再执行目标命令 — 无一例外
```

**禁止行为：**
- ❌ 直接运行 `python script.py` 而不先激活 conda 环境
- ❌ 直接运行 `pip install <package>` 而不先激活 conda 环境
- ❌ 假设当前 shell 已处于正确的 conda 环境中而跳过激活步骤
- ❌ 使用系统级 Python（`/usr/bin/python`）或全局 pip 执行任何任务
- ❌ 以"环境已经激活过了"为由省略 `conda activate` 步骤

**正确示例：**
```bash
# ✅ 正确：先激活环境，再执行命令
conda activate <env_name>
pip install torch
python train.py

# ❌ 错误：直接执行，未激活环境
pip install torch
python train.py
```

**适用场景（无一例外）：**
- ✅ 安装任何 Python 包（pip / conda install）
- ✅ 运行任何 Python 脚本或模块
- ✅ 启动 Jupyter Notebook / Lab
- ✅ 执行 pytest、black、mypy 等依赖 Python 环境的工具
- ✅ 字面上每一条涉及 Python 环境的命令，没有例外

> **注意：** 若用户未指定环境名称，必须通过 `ask_user` 工具询问目标 conda 环境名，再继续执行。

---

## 提问行为（所有模式）
- 在任何模式下，需要向用户提问时，**必须使用 `ask_user` 工具**，而不是在回复文本中直接提问。
