# GitHub Actions Claude Integration Setup Guide

Guide for setting up GitHub Actions that automatically triggers Claude Code when `@claude` is mentioned in Issue comments or PR review comments.

---

## Quick Setup

### 1. Get Anthropic API Key

1. Go to https://console.anthropic.com/
2. Get API key

### 2. Add API Key to Repository Secrets

1. **Repository Settings**
2. **Secrets and variables → Actions**
3. **New repository secret**
   - Name: `ANTHROPIC_API_KEY`
   - Value: Your API key

### 3. Enable Workflow

The workflow file `.github/workflows/claude-responder.yml` is already included in the template.

---

## Usage

### Comment on Issue

```
@claude Please implement this feature
```

Claude will:
1. Analyze the request
2. Create a branch
3. Implement the feature
4. Create a PR

### PR Review Comment

```
@claude Please fix based on this review
```

Claude will:
1. Analyze the comment
2. Make fixes
3. Push commits

---

## Optional Settings

### Using GLM API (Z.AI)

1. **Secrets** → Add:
   - Name: `ZAI_API_KEY`
   - Value: Z.AI API key

2. **Variables** → Add:
   - Name: `ANTHROPIC_BASE_URL`
   - Value: `https://api.z.ai/v1`

3. Modify workflow file:
```yaml
env:
  ANTHROPIC_API_KEY: ${{ secrets.ZAI_API_KEY }}
  ANTHROPIC_BASE_URL: ${{ vars.ANTHROPIC_BASE_URL }}
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Claude doesn't respond | Check API key validity |
| PR not created | Check write permissions |
| GL API error | Check BASE_URL |

---

## Security Notes

- Never commit API keys directly to code
- Rotate API keys regularly
- Limit action permissions to minimum required
