# Claude Commands

A collection of Claude Code slash commands for engineering workflows. Useful for developers, product managers, and teams of all sizes.

## Purpose

These commands provide **AI-assisted guidance** for common engineering tasks. They are designed to:

- **Guide, not execute** - AI provides recommendations and analysis; engineers make decisions and take actions
- **Enhance productivity** - Streamline research, reviews, and documentation tasks
- **Maintain security** - No credentials, secrets, or PII handling; all sensitive operations require human action
- **Follow best practices** - Align with industry standards and compliance requirements

## Important Guidelines

### AI as Assistant, Not Actor

These commands are designed with a clear principle: **AI assists, humans decide and act.**

- Commands **analyze** code, tickets, and documentation
- Commands **suggest** approaches and identify issues
- Commands **guide** through processes with recommendations
- Engineers **review** AI suggestions before acting
- Engineers **execute** all commits, pushes, and deployments
- Engineers **approve** all changes to production systems

### Security & Compliance

- **No credential storage** - Commands never store or transmit credentials
- **No auto-commit/push** - All git operations require explicit user action
- **No PII handling** - Commands follow strict data handling guidelines
- **Human review required** - All AI suggestions must be reviewed before implementation

### Accuracy & Verification

All commands should follow the [Accuracy Guidelines](commands/general/accuracy-guidelines.md):

- **State confidence percentage** - After analysis, state how confident you are (90%+ is ideal)
- **If below 90%, dig deeper** - Verify against primary sources before proceeding
- **Document verification** - Note what was checked and what was found
- **Never trust without verifying** - Claims like "no changes" must be verified against actual data/code/systems

### Attribution

All commands should follow the [Attribution Guidelines](commands/general/attribution.md):

- **Commits** - Include `Co-Authored-By: Claude <noreply@anthropic.com>` in commit messages
- **PRs, tickets, reviews, reports** - Include `Generated with Claude Code` footer
- **Terminal-only output** - No attribution needed for conversational responses

## Command Structure

```
commands/
├── general/              # Broadly applicable commands
│   ├── accuracy-guidelines.md  (reference guidelines for all commands)
│   ├── attribution.md           (attribution standards for all commands)
│   ├── git-pr.md
│   ├── pr-review.md
│   ├── review-docs.md
│   └── ticket-create.md
│
└── veterans-affairs/     # VA.gov specific commands
    ├── backlog-audit.md
    ├── ci-check.md
    ├── collab-review.md
    ├── collab-review-checklist.md  (helper file for collab-review)
    ├── collab-triage.md
    ├── on-call.md
    ├── sprint-monitor.md
    └── ticket-pointing.md
```

## Available Commands

### General Commands

These commands work for any project:

| Command | Description |
|---------|-------------|
| `/pr-review` | PR code review guidance with security and quality focus |
| `/git-pr` | Git workflow guidance for creating branches and preparing PRs |
| `/review-docs` | Review documentation for grammar, technical accuracy, and best practices |
| `/ticket-create` | Create well-structured GitHub issues with user stories and acceptance criteria |

*Note: `accuracy-guidelines.md` and `attribution.md` are reference files for all commands - not standalone commands.*

### VA.gov Specific Commands

These commands are tailored for VA.gov Platform work:

| Command | Description |
|---------|-------------|
| `/backlog-audit` | Audit open GitHub backlog tickets for likely-done, duplicate, or overlapping work |
| `/ci-check` | Check CI status for commits on vets-api master branch |
| `/collab-review` | Backend Engineering reviews for Collaboration Cycle (Architecture Intent & Staging Review) |
| `/collab-triage` | Quick triage of Collab Cycle tickets - time estimate, missing artifacts, complexity assessment |
| `/on-call` | Incident response guidance for vets-api with diagnostic commands and escalation paths |
| `/sprint-monitor` | Track ticket progress, A/C completion, stale items, and teammate review needs on a GitHub Project board |
| `/ticket-pointing` | Point tickets using complexity-based story points for sprint refinement |

*Note: `collab-review-checklist.md` is a supporting reference file used by `/collab-review` - not a standalone command.*

## Getting Started (Non-Programmers Welcome!)

New to Claude Code or the command line? No problem! Here's a step-by-step guide.

### What is Claude Code?

Claude Code is an AI assistant that runs in your terminal (the command line application on your computer). These "slash commands" are like shortcuts that tell Claude Code how to help you with specific tasks.

### Step 1: Install Claude Code

If you haven't installed Claude Code yet:

1. Open **Terminal** (Mac) or **Command Prompt** (Windows)
2. Follow the installation instructions at [claude.ai/claude-code](https://claude.ai/claude-code)

### Step 2: Download These Commands

**Option A: Download from GitHub (easiest)**

1. Go to [github.com/oddballteam/claude-commands](https://github.com/oddballteam/claude-commands)
2. Click the green **"Code"** button
3. Click **"Download ZIP"**
4. Unzip the downloaded file

**Option B: Use git (if you have it installed)**

Open Terminal and run:
```bash
git clone https://github.com/oddballteam/claude-commands.git
```

### Step 3: Install the Commands

1. Open **Terminal** (Mac) or **Command Prompt** (Windows)
2. Create the commands folder if it doesn't exist:
   ```bash
   mkdir -p ~/.claude/commands
   ```
3. Copy the commands you want. For example, to copy all general commands:
   ```bash
   cp -r /path/to/claude-commands/commands/general/* ~/.claude/commands/
   ```

   Replace `/path/to/` with where you downloaded/unzipped the files.

### Step 4: Use a Command

1. Open Terminal
2. Type `claude` to start Claude Code
3. Type a slash command like `/pr-review` followed by what you need

**That's it!** You're ready to use the commands.

### Tips for Non-Programmers

- **Don't worry about breaking anything** - These commands only provide suggestions; they don't make changes automatically
- **Ask for help** - Type questions to Claude Code in plain English
- **Start simple** - Try `/review-docs` with a document you're working on

---

## Installation (For Developers)

### Option 1: Copy specific commands

Copy only the commands you need:

```bash
# Clone the repo
git clone https://github.com/oddballteam/claude-commands.git

# Copy general commands
cp claude-commands/commands/general/* ~/.claude/commands/

# Copy VA-specific commands (if working on VA.gov)
cp claude-commands/commands/veterans-affairs/* ~/.claude/commands/
```

### Option 2: Symlink for easy updates

```bash
# Symlink entire directories
ln -s /path/to/claude-commands/commands/general/* ~/.claude/commands/
ln -s /path/to/claude-commands/commands/veterans-affairs/* ~/.claude/commands/
```

### Option 3: Use as a reference

Browse the commands and adapt them for your own workflows.

## Usage

Invoke any command by typing it in Claude Code:

```
/pr-review https://github.com/your-org/your-repo/pull/123
```

```
/review-docs path/to/your/document.md
```

```
/ci-check
```

## Customization

These commands are designed to be adapted. Common customizations:

- **Change output paths** - Update `~/discoveries/` or `~/doc-reviews/` to your preferred locations
- **Add team-specific patterns** - Extend checklists with your team's conventions
- **Modify language** - Adjust tone and terminology for your organization

## Contributing

Contributions are welcome! When adding or modifying commands:

1. **Follow the AI-as-guide principle** - Commands should analyze and recommend, not autonomously execute
2. **No secrets or credentials** - Never include or reference sensitive information
3. **Keep commands general** - Put project-specific commands in the appropriate subdirectory
4. **Test thoroughly** - Verify commands work as expected before submitting

### Adding New Commands

- **General commands** go in `commands/general/`
- **VA-specific commands** go in `commands/veterans-affairs/`
- **Other project-specific commands** - Create a new subdirectory (e.g., `commands/your-project/`)

## License

MIT License - Feel free to use, modify, and distribute.

## Support

- GitHub Issues: [Report bugs or request features](https://github.com/oddballteam/claude-commands/issues)
- For VA.gov specific questions: Slack `#vfs-platform-support`
