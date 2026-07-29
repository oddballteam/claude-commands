---
description: Build a filtered PR review queue showing only vets-api PRs with teammate approval, sorted oldest-first, ready for /pr-review
---

# PR Review Queue Builder

You are a PR queue builder for the VA vets-api backend support rotation. Your job is to find all open PRs that are **ready for platform review** — meaning they have been approved by the author's own team — and present them as a prioritized queue.

## Arguments

`` — optional filter (e.g., `my-prs`, a GitHub username, or leave empty for full queue)

**Examples:**
- `/pr-review-queue` — full queue, all repos
- `/pr-review-queue vets-api` — vets-api only

## Process

### Step 1: Get identity and team membership

```bash
GH_HOST=va.ghe.com gh api user --jq .login
GH_HOST=va.ghe.com gh api orgs/software/teams/backend-review-group/members --paginate --jq '.[].login'
```

Save the backend-review-group member list. These are platform reviewers — their approvals do NOT count as "teammate approval."

### Step 2: Pull PRs requesting backend-review-group review

```bash
GH_HOST=va.ghe.com gh search prs --state open \
  --review-requested "software/backend-review-group" \
  --json number,title,author,labels,updatedAt,repository \
  --limit 50
```

### Step 3: Pull PRs with require-backend-approval label (broader net)

```bash
GH_HOST=va.ghe.com gh search prs --repo software/vets-api --state open \
  --label "require-backend-approval" \
  --json number,title,author,labels,updatedAt \
  --limit 50
```

Also check these repos individually:
- `software/vets-api-mockdata`
- `software/vets-json-schema`
- `software/platform-atlas`

Deduplicate by PR number across all sources.

### Step 4: Filter out ineligible PRs

Exclude:
- **Dependabot** — `author.login` contains `dependabot`
- **CI failing** — labels include `test-failure` or `lint-failure`
- **Exempt** — labels include `exempt-be-review`
- **Already reviewed by me** — run `GH_HOST=va.ghe.com gh search prs --state open --reviewed-by "@me" --json number,repository` and exclude those PR numbers

### Step 5: Check for teammate approval

For each remaining PR, fetch reviews:

```bash
GH_HOST=va.ghe.com gh pr view <NUMBER> --repo <OWNER/REPO> \
  --json reviews \
  --jq '[.reviews[] | select(.state=="APPROVED") | .author.login]'
```

A PR is **ready** if at least one approver is NOT in the backend-review-group member list (i.e., the approval came from the author's own team, not platform).

Discard PRs with no non-backend-review-group approvals.

### Step 6: Check for PRs already reviewed by other backend-review-group members

Optionally search reviewed-by for each backend-review-group member to catch PRs not explicitly in the queue:

```bash
GH_HOST=va.ghe.com gh search prs --state open \
  --reviewed-by "<member-login>" \
  --json number,title,author,repository \
  --limit 30
```

Add any new PRs found that have teammate approval and haven't been reviewed by the current user.

### Step 7: Sort and present

Sort the ready PRs:
1. **Priority team members first** (check memory for who these are)
2. **Oldest first** (lowest PR number = longest waiting = highest SLA risk)

Present as a table:

```
## Ready for Platform Review — N PRs

| # | Repo | Author | Title | Teammate Approval | Age |
|---|------|--------|-------|-------------------|-----|
| #NNNNN | vets-api | author | Title | Approver ✅ | X days |
...

## Excluded

| # | Author | Title | Reason |
|---|--------|-------|--------|
| #NNNNN | dependabot | ... | Dependabot |
| #NNNNN | author | ... | CI failing (test-failure) |
| #NNNNN | author | ... | No teammate approval yet |
```

Then ask: **"Want me to start the first batch of 6 (oldest-first)?"**

If yes, hand off to `/pr-review` with the first 6 PR URLs.

## What This Bot Does

- ✅ Searches across all backend-review-group repos
- ✅ Gets live backend-review-group member list from GitHub API
- ✅ Checks every PR for non-platform teammate approval
- ✅ Excludes CI-failing, dependabot, and exempt PRs
- ✅ Excludes PRs already reviewed by the current user
- ✅ Sorts oldest-first to protect 24hr SLA
- ✅ Presents a clean, actionable queue table

## What This Bot Does NOT Do

- ❌ Post reviews (use `/pr-review` for that)
- ❌ Approve PRs on GitHub
- ❌ Cache results — always fetches live data
