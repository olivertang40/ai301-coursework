# Plan: README and `.env.example` disagree about which LLM API key to set (#73)

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73
My reproduction: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5918700667

## Diagnosis

`.env.example` is behind `core/config.py`: the config declares the
OpenRouter settings, but the template doesn't list them. So both setup
docs tell a new contributor to set a key that the template they copy
doesn't contain. (I haven't checked git history for how it got this
way, and the fix doesn't depend on it.)

The evidence this rests on, from my reproduction at `f89c06f`:

```text
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
```

After `Copy-Item .env.example .env.repro`, searching for
`OPENROUTER_API_KEY` in the copy returned `0`. The provider section of the
copy was:

```text
# LLM provider
# Options: "mock" (default, no API key needed), "openai"
LLM_PROVIDER=mock
OPENAI_API_KEY=sk-your-key-here
```

And the config declares the OpenRouter fields:

```text
core/config.py:20:    openrouter_api_key: str = Field(default="")
core/config.py:21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
core/config.py:22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")
```

Two docs and the config agree that `OPENROUTER_API_KEY` is a real
setting. Only `.env.example` is missing it. So `.env.example` is the
file that should move, not the README.

## Scope

In scope:
- `.env.example` only. Add an OpenRouter block under `# LLM provider`
  with `OPENROUTER_API_KEY`, `OPENROUTER_BASE_URL` and
  `OPENROUTER_MODEL`. The base URL and model use the same defaults as
  `core/config.py`, so copying the template changes no behavior.

Not in scope:
- `README.md` and `docs/SETUP.md`. They already name the key that the
  config declares, so once the template has it they agree with it.
- `core/config.py` and any runtime code. I'm not adding or changing
  provider logic.
- The `LLM_PROVIDER` options comment. See Risks and unknowns: I haven't
  found code that reads `llm_provider`, so I won't add `"openrouter"`
  as an option I can't show works.
- Removing `OPENAI_API_KEY`. `ingestion/embeddings/provider.py` still
  documents it as required for embeddings.

## Files I'll touch

- `.env.example`. That's the only file.

## Approach

1. Branch from `main` on my fork: `fix/73-env-example-openrouter-key`.
2. In `.env.example`, directly under the existing
   `OPENAI_API_KEY=sk-your-key-here` line, add:

   ```text
   # OpenRouter (README and docs/SETUP.md ask for this key for AI features)
   OPENROUTER_API_KEY=sk-or-your-key-here
   OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
   OPENROUTER_MODEL=google/gemma-3-27b-it:free
   ```

3. Commit as `docs: add OpenRouter settings to .env.example (#73)`.

## Test plan

Re-run my unit 2 repro commands against the branch:

```powershell
git grep -n "OPENROUTER_API_KEY" HEAD -- README.md docs/SETUP.md .env.example
Copy-Item .env.example .env.repro
@(Select-String -Path .env.repro -Pattern "OPENROUTER_API_KEY").Count
Select-String -Path .env.repro -Pattern "^# LLM provider|^# Options|^LLM_PROVIDER=|^OPENAI_API_KEY=|^OPENROUTER_"
```

Expected after the fix:
- The count goes from `0` (before) to `1`.
- `git grep` lists `.env.example` next to `README.md:24` and
  `docs/SETUP.md:47`.
- The `Select-String` output shows the three `OPENROUTER_*` lines.

Because the repro was static inspection, I'll also check the template
through the real config loader, so the new keys map onto the fields in
`core/config.py`:

```bash
uv run --no-project --with pydantic-settings python -c "from core.config import Settings; s = Settings(_env_file='.env.repro'); print(repr(s.openrouter_api_key), s.openrouter_base_url, s.openrouter_model)"
```

- Before (template copied from `main`): `''` plus the code defaults,
  because the template sets nothing.
- After: `'sk-or-your-key-here' https://openrouter.ai/api/v1
  google/gemma-3-27b-it:free`. The key comes from the template, and the
  URL and model match the code defaults.

Finally, `make test-unit` should show no new failures. The change is a
template file, so I don't expect any.

## Risks and unknowns

- **Which `LLM_PROVIDER` value selects OpenRouter is unknown.** I found
  no code that reads `settings.llm_provider` or the `openrouter_*`
  fields. `ReviewGenerator` takes a `ReviewConfig`, but I haven't found
  where one is built from settings. So I'm not claiming OpenRouter works
  at runtime, and I'm leaving the options comment alone instead of
  guessing a value.
- **The placeholder value.** `sk-or-your-key-here` follows the existing
  `sk-your-key-here` style. If the template wanted the key to start
  empty instead, that's a one-line change in review.
- **Open PR #77 takes a broader direction.** It adds `"openrouter"` to
  the options comment and tells README readers to set
  `LLM_PROVIDER=openrouter`. I'm not following it on that point
  because of the unknown above. Both add the same
  `OPENROUTER_API_KEY` line. Mine also adds the base URL and model. If
  maintainers pick #77, I'll drop or rebase my PR.
- **Only checked on Windows.** I ran the repro on Windows PowerShell.
  I haven't run the Git Bash Quick Start path end to end.

## Deviations

The code change matches the plan: four lines added to `.env.example`
under `OPENAI_API_KEY`, and no other file touched. The re-run repro
gave the expected results: the count went from `0` to `1`, and
`Settings` read `'sk-or-your-key-here'` from the template.

One small difference in how I tested: the plan says `make test-unit`,
but `make` isn't installed on my Windows machine. I ran the same suite
directly with `.venv/Scripts/python.exe -m pytest tests/unit -q`:
375 passed, 53 xfailed, 0 failed. The posted plan is still accurate,
so this doesn't need a follow-up comment on the issue.
