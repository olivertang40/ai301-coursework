# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

olivertang40

**Plan comment**

[Plan comment permalink](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6011873888)

````markdown
Plan for #73, built from [my reproduction above](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5918700667) at `f89c06f`.

**Diagnosis:** `.env.example` is the file that's out of date. In my repro, `README.md:24` and `docs/SETUP.md:47` both say to set `OPENROUTER_API_KEY`, and `core/config.py:20-22` declares `openrouter_api_key`, `openrouter_base_url` and `openrouter_model`. But the copied `.env.example` had `0` matches for the key. Two docs and the config agree, and only the template is missing it.

**Change:** I'll edit `.env.example` and nothing else. Under the existing `OPENAI_API_KEY` line I'll add `OPENROUTER_API_KEY`, `OPENROUTER_BASE_URL` and `OPENROUTER_MODEL`, with the URL and model set to the same defaults `core/config.py` already uses. Out of scope: README/SETUP wording, runtime or config code, and removing `OPENAI_API_KEY` (embeddings still reference it).

**Test:** I'll re-run my repro commands on the branch. The `OPENROUTER_API_KEY` count in a fresh copy of `.env.example` should go from `0` to `1`. I'll also load the copied template through `core.config.Settings` to confirm all three keys land on their fields.

**Open question:** I couldn't find code that reads `llm_provider` or the `openrouter_*` settings, so I don't know which `LLM_PROVIDER` value is meant to select OpenRouter. I'm leaving the `# Options:` comment as it is rather than guessing. If a maintainer knows the intended value, I'll add it.

**Relation to PR #77:** PR #77 also targets this issue. It adds `"openrouter"` to the `LLM_PROVIDER` options and changes the README to say "set `LLM_PROVIDER=openrouter`". My plan is narrower on purpose: I couldn't find code that acts on `llm_provider`, so I can't show that the value works, and I'd rather not document it. Both add the same `OPENROUTER_API_KEY` line. Mine also adds the base URL and model with their code defaults. If maintainers prefer #77's direction, I'll drop my PR or rebase it onto theirs.

I used an AI assistant (Claude Code) to help trace the config and draft this plan. I checked the file contents above against my own checkout.
````

---

## Your branch

**Branch**

fix/73-env-example-openrouter-key

**Evidence**

Before (my Unit 2 repro commands on `main` at `f89c06f`, Windows PowerShell):

```text
PS> git log -1 --format="%H %ad" --date=short
f89c06fc3ff292df2a04a39ac51319d32a76b779 2026-09-16
PS> git grep -n "OPENROUTER_API_KEY" HEAD -- README.md docs/SETUP.md .env.example
HEAD:README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
HEAD:docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
PS> Copy-Item .env.example .env.repro -Force
PS> @(Select-String -Path .env.repro -Pattern "OPENROUTER_API_KEY").Count
0
PS> Select-String -Path .env.repro -Pattern "^# LLM provider|^# Options|^LLM_PROVIDER=|^OPENAI_API_KEY=|^OPENROUTER_"
.env.repro:16:# LLM provider
.env.repro:17:# Options: "mock" (default, no API key needed), "openai"
.env.repro:18:LLM_PROVIDER=mock
.env.repro:19:OPENAI_API_KEY=sk-your-key-here
```

The copied template, loaded through the real config loader:

```text
$ uv run --no-project --with pydantic-settings python -c "from core.config import Settings; s = Settings(_env_file='.env.repro'); print(repr(s.openrouter_api_key), s.openrouter_base_url, s.openrouter_model)"
'' https://openrouter.ai/api/v1 google/gemma-3-27b-it:free
```

After (same commands on `fix/73-env-example-openrouter-key` at commit `cd71201`):

```text
PS> git log -1 --format="%H %ad" --date=short
cd712011309d24487fad49d8676e08ac8115d403 2026-10-06
PS> git branch --show-current
fix/73-env-example-openrouter-key
PS> git grep -n "OPENROUTER_API_KEY" HEAD -- README.md docs/SETUP.md .env.example
HEAD:.env.example:21:OPENROUTER_API_KEY=sk-or-your-key-here
HEAD:README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
HEAD:docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
PS> Copy-Item .env.example .env.repro -Force
PS> @(Select-String -Path .env.repro -Pattern "OPENROUTER_API_KEY").Count
1
PS> Select-String -Path .env.repro -Pattern "^# LLM provider|^# Options|^LLM_PROVIDER=|^OPENAI_API_KEY=|^OPENROUTER_"
.env.repro:16:# LLM provider
.env.repro:17:# Options: "mock" (default, no API key needed), "openai"
.env.repro:18:LLM_PROVIDER=mock
.env.repro:19:OPENAI_API_KEY=sk-your-key-here
.env.repro:21:OPENROUTER_API_KEY=sk-or-your-key-here
.env.repro:22:OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
.env.repro:23:OPENROUTER_MODEL=google/gemma-3-27b-it:free
```

```text
$ uv run --no-project --with pydantic-settings python -c "from core.config import Settings; s = Settings(_env_file='.env.repro'); print(repr(s.openrouter_api_key), s.openrouter_base_url, s.openrouter_model)"
'sk-or-your-key-here' https://openrouter.ai/api/v1 google/gemma-3-27b-it:free
```

Unit suite on the branch (`make` isn't installed on Windows, so I ran the same target's pytest directly):

```text
$ .venv/Scripts/python.exe -m pytest tests/unit -q
375 passed, 53 xfailed, 4 warnings in 12.05s
```

## Eval iterations

**Run history**

1. Partial `--only pkg-03,pkg-04,pkg-09,pkg-20`: 4/4. A smoke test of the two comms checks on both thread-convention packages and two accepts from repos with AI policies.
2. Full run 1: 18/19 scored, with pkg-02 errored. pkg-14 disagreed (failed grounded-cause and executable). pkg-02 never reached the grader: on Windows, `subprocess` encodes stdin as cp1252, and pkg-02 contains an emoji, so `claude -p` received no input. Because an item errored, this run wasn't written to `eval-run.txt`.
3. Partial `--only pkg-14,pkg-02` plus canaries pkg-17, pkg-18, pkg-10 (unbuildable) and pkg-16, pkg-07, pkg-01 (wrong-cause): 7/7 scored. pkg-14 flipped to agree and every canary held. pkg-02 errored again.
4. Partial `--only pkg-02` with `PYTHONUTF8=1`: 0/1. pkg-02 now graded, and it was a false reject on bounded-scope.
5. Partial `--only pkg-02` plus canaries pkg-06, pkg-12, pkg-15, pkg-19 (all of scope-creep): 5/5.
6. Full run 2 (confirming, written to `eval-run.txt`): **20/20**. Categories: clear-accept 7/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4.

**Package analysis**

`pkg-14` (zellij-org/zellij#5174). In full run 1 my rubric decided **reject**; the gold label is **accept**.

It failed two checks. On grounded-cause, the grader read the cache control (`rm -rf ~/.cache/zellij` makes the next attach clean) as something the plan's stdin-wiring cause "only hand-waves". But nothing in the repro rules the cause out. The plan does explain the cache control, just briefly, and the 0.44.1 control and the fresh-attach control both support it. My check said "explains what the repro shows", and the grader treated a thin explanation as a failed one. On executable, it failed "exact functions to be pinned in the PR after tracing the query issuance with debug logs", treating that as a location left to investigation. But the plan names the component (the client attach/reattach path in `zellij-server`'s connection handling) and commits to one mechanism (drain OSC responses before pane input is wired). What's left open is which function, not which layer or which approach. I changed grounded-cause to fail only on contradiction, and executable to accept a named component plus a decided mechanism. pkg-14 then agreed, and the unbuildable and wrong-cause canaries all held.

**Check rationale**

From the `rubric.md` uploaded to `tools/plan-check/`, the `bounded-scope` check reads:

> Every piece of work the plan commits to doing is needed to fix or regression-test the reproduced behavior. Fail if the plan commits to any extra front: a refactor or rewrite of surrounding code, a dependency upgrade or migration, a new option/setting/UI, a new framework, or porting the fix to other components "while in the area", even when the core fix is correct. Work that is explicitly deferred to a follow-up or listed as not in scope does not count against it. Applying the same fix to (or auditing) other occurrences of the same defect in the same function or file is part of the fix, not an extra front. Carrying it into other components or modules is an extra front.

The first version stopped after "does not count against it". It caught all four scope-creep packages, but once pkg-02 actually reached the grader, that version failed it. The pkg-02 plan clamps the subtraction the issue names, applies the same clamp to the sibling cursor advance in the same function, and audits the two other `cursor_max - cursor` sites. The grader asked "is the bug still fixed without the sibling clamp?", answered yes, and failed it. But fixing the same defect where it recurs in the same function is what a careful maintainer wants. It's the opposite of scope creep. The last two sentences draw the line at what kind of work it is and where it reaches, not how many lines it touches. The same fix in the same file is part of the fix. The same fix carried into another component (pkg-19's TransitionGroup port) is a new front.

**Trade-offs**

The same-file exception gives something up. A plan that touches many sites in one large file under the label "the same defect" could pass, even if a reviewer would call it a sweep. The rubric doesn't count sites; it trusts that "same defect" is true. Because the change loosened the check, I re-ran all four scope-creep packages (pkg-06, pkg-12, pkg-15, pkg-19) as canaries with `--only` before the confirming run. All four still rejected, and the confirming full run kept scope-creep at 4/4.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
