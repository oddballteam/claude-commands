# Accuracy Guidelines

These guidelines ensure AI-assisted analysis is thorough, verified, and trustworthy.

## Core Principle

**Verify, don't just trust.** Never rely solely on stated claims or documentation without checking primary sources.

---

## Accuracy Assessment Framework

### 1. State Your Confidence Level

After completing any analysis, state your accuracy/confidence percentage:

| Confidence | Meaning | Action |
|------------|---------|--------|
| **90-100%** | Verified against primary sources | Proceed |
| **70-89%** | Partially verified, some assumptions | Note what wasn't verified |
| **Below 70%** | Significant uncertainty | **Dig deeper before proceeding** |

### 2. If Below 90%, Dig Deeper

When confidence is below 90%:

1. Identify what's uncertain or unverified
2. Check primary sources (actual data, systems, code, files)
3. Document what you checked and what you found
4. Re-assess confidence after verification
5. Repeat until 90%+ or clearly document blockers

### 3. Document Your Verification

Include what you verified and how:

| Claim | Verified? | How |
|-------|-----------|-----|
| Example claim | ✅ Yes | Checked [source], found [result] |
| Another claim | ⚠️ Partial | Verified X, could not verify Y |
| Third claim | ❌ No | Unable to access [source] |

---

## What to Verify vs. Trust

### Always Verify
- Claims of "no impact" or "no changes"
- Security-related assertions
- Data or system integration claims
- Configuration states

### Trust with Caution
- Descriptions of intent or goals
- Planning information
- Business requirements

### Trust but Note
- Future plans
- Opinions on approach
- Estimates

---

## Anti-Patterns

| Bad | Good |
|-----|------|
| "The doc says X, so X is true" | "The doc says X. I verified by checking [source]" |
| "I'm 95% confident" (no evidence) | "I'm 95% confident because I verified [list]" |
| Skipping verification for "simple" tasks | Verify even simple claims against primary sources |

---

## Summary

1. **State your confidence percentage**
2. **If below 90%, dig deeper**
3. **Verify against primary sources**
4. **Document what you verified**
