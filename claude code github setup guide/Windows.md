# Claude Code GitHub Actions - Windows Complete Setup Guide

**From Zero to Automated PR Reviews**

Windows | November 2025

---

## Introduction

Welcome to the complete guide for setting up Claude Code GitHub Actions. This documentation will take you from absolute zero to having fully automated AI-powered code reviews running on every pull request.

💡 **WHO THIS IS FOR**: Complete beginners welcome! This guide assumes you have never used Claude Code, GitHub CLI, or automated code reviews before. We'll walk through every single step.

### What You'll Accomplish

By following this guide, you will:

- Install and configure all required tools (GitHub CLI and Claude Code)
- Set up automated PR reviews that catch bugs before production
- Integrate Claude AI directly into your GitHub workflow
- Configure security-focused code analysis
- Have a professional development workflow that prevents costly mistakes

### Prerequisites

Before starting, ensure you have:

- A GitHub account with access to at least one repository
- Claude subscription or API key: Claude Pro ($20/month), Claude Max ($100/month), or Anthropic API access
- Operating System: Windows 10+
- Administrator access on your computer (for installing software)
- 20-40 minutes of uninterrupted setup time

---

## PART 2: Windows Complete Setup

This section contains all steps for Windows users. Follow these steps in order from start to finish.

### Step 1: Install GitHub CLI (Windows)

GitHub CLI (gh) is the official command-line tool for GitHub. It allows you to interact with GitHub from your terminal.

#### Open PowerShell or Command Prompt

1. Press Windows Key or click the Start button
2. Type **PowerShell** or **cmd**
3. Right-click and select **Run as administrator** (recommended)
4. A terminal window will open with a command prompt

#### Install GitHub CLI with WinGet

Run the following command:

```powershell
winget install --id GitHub.cli
```

Accept any prompts. Installation typically takes 1-2 minutes.

#### Restart Your Terminal

Close and reopen PowerShell/Command Prompt for the PATH to update.

- Close the window (click X or type exit)
- Reopen PowerShell/Command Prompt as administrator

#### Verify Installation

Confirm GitHub CLI is installed:

```powershell
gh --version
```

You should see output like: `gh version 2.40.0`

✅ **SUCCESS**: If you see a version number, GitHub CLI is installed correctly!

💡 **ALTERNATIVE INSTALLATION METHODS**:
- **Chocolatey**: `choco install gh`
- **Scoop**: `scoop install gh`
- **MSI Installer**: Download from cli.github.com

⚠️ **TROUBLESHOOTING: Command Not Found**

If 'gh' is not recognized after installation:

1. Restart your terminal completely
2. If still not working, check PATH environment variable
3. Try running as administrator

---

### Step 2: Authenticate GitHub CLI (Windows)

Now that GitHub CLI is installed, connect it to your GitHub account.

#### Start the Authentication Process

In your terminal, run:

```powershell
gh auth login
```

#### Select Account Type

You'll see a prompt:

```
? What account do you want to log into?
```

Use arrow keys to select **GitHub.com** (for most users) and press Enter.

#### Select Protocol

Next prompt:

```
? What is your preferred protocol for Git operations?
```

Select **HTTPS** (recommended for most users) and press Enter.

#### Authenticate with GitHub Credentials

You'll see:

```
? Authenticate Git with your GitHub credentials? (Y/n)
```

Type **Y** and press Enter.

#### Choose Authentication Method

Next prompt:

```
? How would you like to authenticate GitHub CLI?
```

Select **Login with a web browser** (recommended) and press Enter.

#### Complete Browser Authentication

1. You'll see a one-time code displayed, example: `ABCD-1234`
2. Copy this code (select the text and press Ctrl+C)
3. Press Enter - your browser will open automatically
4. GitHub will ask you to paste the code - paste it and click Continue
5. Click **Authorize github** to grant permissions
6. You'll see a success message in the browser
7. Return to your terminal - authentication is complete!

#### Verify Authentication

Confirm you're logged in:

```powershell
gh auth status
```

You should see output showing you're logged into GitHub.com with your username.

✅ **SUCCESS**: You are now authenticated with GitHub!

---

### Step 3: Install Claude Code CLI (Windows)

Claude Code is Anthropic's AI coding assistant that runs in your terminal.

#### Open PowerShell as Administrator

1. Press Windows Key, type **PowerShell**
2. Right-click **Windows PowerShell**
3. Select **Run as administrator**

#### Run Installation Command (Native Method - Recommended)

In PowerShell, run:

```powershell
irm https://claude.ai/install.ps1 | iex
```

This downloads and runs the official Claude Code installer. Wait 1-2 minutes.

#### Restart PowerShell

Close and reopen PowerShell for PATH to update.

- Close PowerShell window
- Reopen PowerShell (can be normal mode, admin not required)

#### Verify Installation

Check Claude Code is installed:

```powershell
claude --version
```

You should see a version number like: `0.2.114`

✅ **SUCCESS**: Claude Code is installed!

💡 **ALTERNATIVE INSTALLATION METHOD**:
- **NPM** (requires Node.js 18+): `npm install -g @anthropic-ai/claude-code`

⚠️ **TROUBLESHOOTING**:
- **Permission Denied**: Run PowerShell as administrator
- **Command Not Found**: Restart PowerShell and try again
- **Execution Policy Error**: Run: `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

---

### Step 4: Authenticate Claude Code (Windows)

Connect Claude Code to your Claude account to enable AI features.

#### Launch Claude Code

In your terminal, simply run:

```powershell
claude
```

If this is your first time, you'll see the authentication setup wizard.

#### Choose Authentication Method

You'll see two options:

- **Claude Console** - For API users (requires console.anthropic.com account)
- **Claude Pro/Max Subscription** - For claude.ai subscribers (recommended)

💡 **WHICH SHOULD I CHOOSE?**
- **Claude Pro/Max**: Fixed monthly cost ($20 or $100), predictable billing. Best for most users.
- **API Console**: Pay-per-use, can get expensive with heavy usage.

#### Option A: Claude Pro/Max (OAuth) - Recommended

1. Use arrow keys to select **Claude Pro/Max**
2. Press Enter
3. Your browser will open to claude.ai
4. Log in with your claude.ai credentials
5. Click **Authorize** to allow Claude Code access
6. Return to terminal - you're now authenticated!

#### Option B: API Console (Alternative)

1. Go to console.anthropic.com in your browser
2. Navigate to **Settings → API Keys**
3. Click **Create Key**
4. Copy the API key (starts with `sk-ant-`)
5. Return to terminal and paste when prompted

#### Test Authentication

You should now see the Claude Code interface. Test it by typing:

```
Hello Claude!
```

Claude should respond, confirming everything works!

#### Exit Claude Code

To exit Claude Code and return to your terminal, type:

```
/exit
```

Or press Ctrl+C twice.

✅ **SUCCESS**: Claude Code is authenticated and ready!

---

### Step 5: Install GitHub Integration (Windows)

This is the crucial step that connects Claude Code to your GitHub repositories for automated PR reviews.

#### Launch Claude Code

In your PowerShell/Command Prompt:

```powershell
claude
```

#### Run Installation Command

Once Claude Code is running, type:

```
/install-github-app
```

Press Enter. This starts the GitHub App installation wizard.

💡 **WHAT HAPPENS NEXT**: The wizard will guide you through installing the Claude GitHub App, setting up your API key as a GitHub Secret, and creating the workflow file. Just follow the prompts!

#### Browser Opens - Install GitHub App

Your browser will open to GitHub's app installation page. Follow these steps:

- You'll see the Claude Code app installation page
- Choose repository access (All repositories or Select repositories)
- Select your target repository(ies)
- Review permissions
- Click **Install & Authorize**

#### Return to Terminal

After authorization, return to your terminal and follow all prompts to:

- Add your `ANTHROPIC_API_KEY` to GitHub Secrets
- Create the workflow file automatically

#### Manual Secret Setup (If Needed)

If you need to add the API key manually:

- Go to repository → Settings → Secrets and variables → Actions
- Click **New repository secret**
- Name: `ANTHROPIC_API_KEY`
- Value: Your API key from console.anthropic.com
- Click **Add secret**

⚠️ **SECURITY NOTE**: Never commit API keys to your code! Always use GitHub Secrets.

✅ **SUCCESS**: GitHub integration is complete!

---

### Step 6: Testing Your Setup (Windows)

Let's verify everything works.

#### Create or Open a Pull Request

- Go to your repository on GitHub.com
- Create a new PR or open an existing one

#### Mention @claude in a Comment

In the PR, add a comment:

```
@claude please review this PR
```

Click **Comment**

#### Watch GitHub Actions

- Go to the **Actions** tab
- You should see a Claude Code workflow running
- Wait 1-3 minutes for completion

#### Check Claude's Response

Return to your PR. Claude should have posted a review with analysis and feedback!

✅ **SUCCESS**: Claude is now reviewing your PRs on Windows!

Your Windows setup is complete. Continue to the next section for next steps.

---

## PART 3: Next Steps & Customization

This section applies to both macOS and Windows users.

### Create a CLAUDE.md File

Add project-specific guidelines for Claude:

- Create `CLAUDE.md` in your repository root
- Define coding standards, review focus areas, and project rules
- Claude will automatically read and follow these guidelines

### Set as Required Check

Make Claude's review mandatory before merging:

- Repository → Settings → Branches
- Add branch protection rule
- Require status checks: Claude Code

### Customize Review Prompts

Modify the workflow to focus on specific concerns:

```yaml
- uses: anthropics/claude-code-action@v1
  with:
    anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
    prompt: "Review for security and performance"
```

### Monitor Usage & Costs

- **Claude Pro/Max**: Check usage at claude.ai
- **API**: Monitor at console.anthropic.com
- **GitHub Actions**: Check minutes in repository settings

---

## Troubleshooting Guide

### Claude Doesn't Respond

- Check Actions tab - Is the workflow running?
- Verify API key in Secrets
- Check workflow permissions

### API Key Errors

- **Invalid key**: Regenerate at console.anthropic.com
- **Quota exceeded**: Check billing
- **Secret not found**: Ensure name is `ANTHROPIC_API_KEY`

### Installation Issues

- **Command not found**: Restart terminal, check PATH
- **Permission denied**: Run with admin/sudo
- **Network errors**: Check firewall/proxy

### Getting Help

- **Docs**: docs.claude.com
- **Support**: support@anthropic.com
- **GitHub Issues**: github.com/anthropics/claude-code-action/issues

---

## Quick Reference

### All Commands

| Task | Command |
|------|---------|
| Install GitHub CLI (Windows) | `winget install --id GitHub.cli` |
| Authenticate GitHub CLI | `gh auth login` |
| Install Claude Code (Windows) | `irm https://claude.ai/install.ps1 \| iex` |
| Launch Claude Code | `claude` |
| Install GitHub Integration | `/install-github-app` |
| Exit Claude Code | `/exit` |
| Trigger PR Review | `@claude please review` |

### Cost Summary

| Option | Cost | Best For |
|--------|------|----------|
| Claude Pro | $20/month | Individual developers |
| Claude Max | $100/month | Heavy users, teams |
| API (Sonnet 4.5) | $3-15/1M tokens | Pay-per-use, scale |
| GitHub Actions | Free tier or $0.008/min | Runner costs |

---

## Conclusion

Congratulations! You've successfully set up Claude Code GitHub Actions. Your repository now has AI-powered code reviews that will help catch bugs, improve code quality, and prevent costly production issues.

### What You've Accomplished:

- Installed and configured GitHub CLI
- Installed and authenticated Claude Code
- Connected Claude to your GitHub repositories
- Set up automated PR reviews
- Tested the integration successfully

🎉 **You're now preventing bugs before they reach production!**

### Keep Learning:

- Explore docs: docs.claude.com
- Join community: github.com/anthropics/claude-code/discussions
- Share feedback to improve Claude Code!

**Happy Coding! 🚀**
