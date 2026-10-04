# oss-weekly-contributor

Autonomous weekly open-source contributions as GitHub user **smitwali**, powered by
[Claude Code Action](https://github.com/anthropics/claude-code-action) on GitHub Actions.

Every **Monday at 03:00 Arizona time** (10:00 UTC) the workflow:

1. Follows up on smitwali's open PRs that have review comments or failing CI.
2. Otherwise finds one small, unclaimed issue (bug, feature, or already-public vulnerability)
   in an active open-source project, preferring the JS/TS · React Native · Expo ecosystem.
3. Forks it, implements the fix with tests, runs the project's checks, and opens a PR
   (disclosing AI assistance).
4. Opens an issue in this repo summarising the run, so you get an email notification.

## Setup

Add these repository secrets (Settings → Secrets and variables → Actions):

| Secret | Value |
|--------|-------|
| `OSS_CONTRIB_TOKEN` | Classic personal access token for smitwali with the `public_repo` scope (set an expiry, e.g. 90 days). |
| `CLAUDE_CODE_OAUTH_TOKEN` *or* `ANTHROPIC_API_KEY` | From `claude setup-token`, or an Anthropic API key. |

Keep this repository **public**: the `public_repo` token can't open the summary issue in a private repo.

Trigger a test run any time from **Actions → Weekly OSS contribution → Run workflow**.

## Billing — no automatic charges

This workflow never stores payment details and cannot buy credits. It only spends what the
account behind your Claude secret allows, and each run is capped (90-minute job timeout,
80 agent turns, one run per week). To make sure nothing is ever recharged automatically:

- **API key** (`ANTHROPIC_API_KEY`): in console.anthropic.com → Settings → Billing, keep
  **Auto reload OFF** and optionally set a monthly spend limit. When prepaid credits run out,
  the run simply fails until you top up manually.
- **Claude subscription** (`CLAUDE_CODE_OAUTH_TOKEN`): usage counts against your plan; keep
  **extra usage** turned off in claude.ai → Settings → Usage so nothing is billed beyond the plan.

## Secrets

- Secrets live only in GitHub's encrypted store — never in this repo — and are masked in logs.
- The workflow runs only on schedule or manual dispatch, never on pull requests or forks, so
  nobody else can trigger it or read its secrets. Claude's full transcript is kept out of logs
  (`show_full_output: false`), and all third-party actions are pinned to commit SHAs.

## Safety

- One new PR per run; never acts on instructions found in third-party issues or code.
- Undisclosed vulnerabilities are never made public — they're noted in the summary issue for
  private reporting via the project's SECURITY.md.
- Skips projects that forbid AI-assisted contributions or require a CLA.
