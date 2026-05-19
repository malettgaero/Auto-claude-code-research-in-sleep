# ARIS Tutorials

Long-form interview-prep cheat sheets, written in Markdown and rendered to single-file HTML via the `/render-html` skill (academic-newspaper template, sticky TOC, MathJax + highlight.js, cross-model codex review gate).

| Tutorial | MD source | Rendered HTML | Topics |
|---|---|---|---|
| **Attention 面试 Cheat Sheet** | [`attention_tutorial.md`](attention_tutorial.md) | [`attention_tutorial.html`](https://wanshuiyin.github.io/Auto-claude-code-research-in-sleep/tutorials/attention_tutorial.html) | Scaled-dot-product, MHA / MQA / GQA, RoPE / ALiBi, FlashAttention, KV cache, attention in diffusion, NaN-mask trap, 25 高频面试题 |
| **Flow Matching Quick Reference** | [`flow_matching_tutorial.md`](flow_matching_tutorial.md) | [`flow_matching_tutorial.html`](https://wanshuiyin.github.io/Auto-claude-code-research-in-sleep/tutorials/flow_matching_tutorial.html) | Conditional FM, Rectified Flow / VP / VE paths, training + sampling code, ODE solvers, SD3 / FLUX latent FM, 与 diffusion / score-matching 的桥 |

## How they were produced

The two pilots were drafted by hand and rendered via `/render-html`. Subsequent tutorials use the dedicated workflow skill:

```
/interview-cheatsheet "<TOPIC>"            # default: 600-line balanced effort
/interview-cheatsheet "<TOPIC>" — effort: max    # ~1000 lines + deeper proofs
```

`/interview-cheatsheet` ([`skills/interview-cheatsheet/SKILL.md`](../../skills/interview-cheatsheet/SKILL.md)) is an ARIS skill that:

1. Plans a 12-14 section structure (TL;DR · intuition · formula+derivation · from-scratch PyTorch · variants · 25 高频面试题 L1/L2/L3)
2. Drafts the MD following the canonical style of the two pilot tutorials (heading conventions, table-pipe escapes, callout-list separation rules — all bugs caught during the pilot reviews are now encoded into the style guide)
3. Cross-model `codex gpt-5.5 xhigh` review on math / code / interview-answer / citation correctness + personal-info redaction (fresh thread, never `codex-reply`)
4. Fix-and-loop up to 3 rounds
5. Renders via `/render-html` (which itself runs a 13-check codex review on the rendered output)
6. Writes a combined audit trail to `*.review.json`
7. **Stops — never auto-commits.** The user reviews and pushes manually.

> See [`skills/interview-cheatsheet/SKILL.md`](../../skills/interview-cheatsheet/SKILL.md) for the full skill protocol and [`skills/render-html/SKILL.md`](../../skills/render-html/SKILL.md) for the renderer.
