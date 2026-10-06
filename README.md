# Masri Tech Explainer

An agent skill that makes Claude (and other coding agents) explain technical topics in **natural Egyptian Arabic (Masri)**, laid out so the text stays readable when Arabic is mixed with English terms, code, commands, and acronyms.

## The problem

Arabic is right-to-left. Code and English terms are left-to-right. When they're mixed carelessly, the renderer's bidi algorithm scrambles the word order: periods jump to the start of the line, parentheses flip, and sentences read out of order.

❌ Without the skill:

> لما Django بيعمل select_for_update() فهو بيضيف FOR UPDATE للـSQL query وبالتالي الـrows اللي رجعت من الـdatabase بتبقى locked.

✅ With the skill:

> لما تستخدم:
>
> `select_for_update()`
>
> ساعتها Django بيضيف للـquery الجملة دي:
>
> `FOR UPDATE`
>
> بعد كده الـdatabase بتعمل lock على الـrows اللي الـquery رجعتها.

## What it does

- Writes friendly, senior-engineer Masri, not formal MSA, and keeps technical terms in English.
- Starts every Arabic line with an Arabic word, so the line keeps a right-to-left base direction.
- Puts code, commands, and SQL on their own lines instead of mid-sentence.
- Limits language switches per sentence, and uses tables and ASCII diagrams for English-heavy content.
- Explains the big picture first (what problem, what idea), then the internals.
- Handles "why" questions, source-code walkthroughs, and correcting someone's mental model.

It triggers automatically when you ask a technical question in Arabic (including Franco/Arabizi), e.g. `اشرحلي database replication`, `يعني إيه race condition`, or "explain this in Egyptian Arabic".

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add Abdelrhamaan/masri-tech-explainer
/plugin install masri-tech-explainer@masri-tech
```

### Any agent via the skills CLI ([skills.sh](https://skills.sh))

```bash
npx skills add Abdelrhamaan/masri-tech-explainer
```

### Manual

Copy `skills/masri-tech-explainer/` into `~/.claude/skills/` (personal) or `.claude/skills/` (per project).

### claude.ai

Zip the `skills/masri-tech-explainer/` folder and upload it under **Settings → Capabilities → Skills**.

## Layout

```text
.claude-plugin/
  plugin.json          plugin manifest
  marketplace.json     lets this repo act as a Claude Code marketplace
skills/
  masri-tech-explainer/
    SKILL.md           the skill instructions
    references/
      example.md       a full example answer
```

## Contributing

Issues and PRs are welcome, especially new before/after examples of text that scrambles in a specific renderer or terminal.

## License

[MIT](LICENSE)
