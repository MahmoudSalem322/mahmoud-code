# mahmoud-code

An agent skill for building projects and large features in five stages, with a plan first and a full review, security check and report for every task. It works in both **Claude Code** and **Codex**.

[العربية](#بالعربي)

## The five stages

1. **Plan, then tasks.** A plan built on research and deep analysis, split into detailed numbered tasks (what each includes, what changes, expected outputs). Then a recommended approach, model and effort for each task. The agent stops and waits for you to write `task 1`, `task 2`, ...
2. **Execute the task** with [Superpowers](https://github.com/obra/superpowers).
3. **Code review and testing**, automatically after execution: a full code review and a test for every part of the task, with Superpowers.
4. **Security testing** with OWASP review, Semgrep/CodeQL static analysis, and Claude Code's `/security-review`.
5. **Detailed report:** task name, outputs, every modified file and whether best practices were used, the results of stages 2 to 4, remaining risks with proposed fixes, and a final evaluation.

The agent may use subagents, but it asks for your approval before starting any. During execution it suggests useful MCP servers or web sources, and asks for your approval before connecting to any of them. Code reviews and reports are written in the voice of a software engineering professor: expert and precise, but clear.

## Requirements

The skill calls these skills. Install them for the full workflow:

| Skill | Used in | Source |
| --- | --- | --- |
| Superpowers | Stages 2, 3, 4 | [obra/superpowers](https://github.com/obra/superpowers) |
| `owasp-security` | Stage 4 | [agamm/claude-code-owasp](https://github.com/agamm/claude-code-owasp) |
| `static-analysis` (Semgrep, CodeQL) | Stage 4 | [trailofbits/skills](https://github.com/trailofbits/skills) |
| `/security-review` | Stage 4 | Built into Claude Code |

If one of them is missing, the agent says so in the report and continues with the others.

## Install

**Claude Code** (all projects):

```bash
git clone https://github.com/MahmoudSalem322/mahmoud-code ~/.claude/skills/mahmoud-code
```

**Codex** (all projects):

```bash
git clone https://github.com/MahmoudSalem322/mahmoud-code ~/.agents/skills/mahmoud-code
```

Restart the agent after installing.

## Use

The skill runs only when you ask for it by name:

```text
use mahmoud-code: build a booking system for a clinic
```

Then run each task by its number: `task 1`, `task 2`, ...

Shortcuts: `/mahmoud-code` in Claude Code, `$mahmoud-code` in Codex.

---

## بالعربي

سكيل لبناء المشاريع والميزات الكبيرة على خمس مراحل، وبتشتغل على **Claude Code** و **Codex**.

1. **خطة ومهام:** خطة مبنية على بحث وتحليل معمّق، بتنقسم لمهام مرقمة ومفصلة. لكل مهمة بتقترح طريقة التنفيذ والنموذج والـ effort، وبعدها بتستنى لحتى تكتب `task 1`.
2. **تنفيذ المهمة** باستخدام Superpowers.
3. **مراجعة كود واختبار** لكل جزئية، بتبلش لحالها بعد التنفيذ.
4. **اختبار أمان** بسكيلز OWASP و Semgrep/CodeQL و `/security-review`.
5. **تقرير مفصل:** اسم المهمة، المخرجات، الملفات المعدّلة، نتائج كل مرحلة، المخاطر والحلول، والتقييم النهائي.

قبل ما تشغّل أي وكيل فرعي، بتستنى موافقتك. وخلال التنفيذ بتقترح MCP أو مصادر مفيدة، وما بتتصل بأي واحد منهم قبل موافقتك. والمراجعة والتقرير بيكونوا بأسلوب بروفيسور برمجة: احترافي ودقيق بس مفهوم.

**التشغيل:** قول للوكيل "استخدم سكيل mahmoud-code" واحكيله شو بدك تبني.

## License

MIT. See [LICENSE](LICENSE).
