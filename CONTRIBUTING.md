# Contributing

The project is a skills-only plugin. Keep the main workflow provider-neutral and put detailed, rubric-specific guidance in `skills/pr-review/references/`.

Changes should preserve these boundaries:

- the main agent owns the review manifest, adjudication, and GitHub publication;
- rubric subagents are independent and read-only;
- findings require concrete evidence and a reproducible consequence;
- publication is the default for GitHub PR inputs, pinned to an exact PR head, suppressible with `local`/`dry-run`, and limited to the `pr-review:` label namespace;
- the plugin must not approve, merge, push, or modify the reviewed repository by default.

Validate the skill with:

```bash
python3 /home/axel/.codex-frenzy/skills/.system/skill-creator/scripts/quick_validate.py skills/pr-review
python3 -m json.tool plugin.json >/dev/null
```

Test substantive rubric changes against representative pull requests or fixtures. Record false positives and missed findings in the pull request description rather than weakening a rubric to fit one example.
