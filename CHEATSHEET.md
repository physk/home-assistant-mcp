# 📋 Quick Cheatsheet

## 🚀 First Time Publishing

```bash
# 1. Register on NPM
# Go to: https://www.npmjs.com/signup

# 2. Login
npm login

# 3. Publish
npm publish --access public
```

---

## 🤖 Setup GitHub Actions (One Time)

```bash
# 1. Create NPM Automation Token
# https://www.npmjs.com/settings/YourUsername/tokens
# Type: Automation

# 2. Add to GitHub Secrets
# https://github.com/Coolver/mcp-home-assistant/settings/secrets/actions
# Name: NPM_TOKEN
# Value: your_token
```

---

## 🔄 Update and Publish

### Automatic (with GitHub Actions):

```bash
npm version patch    # Bug fixes
npm version minor    # New features
npm version major    # Breaking changes

git push && git push --tags

# Then create Release on GitHub
# Actions will auto-publish to NPM!
```

### Manual:

```bash
npm version patch
npm run build
npm publish --access public
git push && git push --tags
```

---

## 📊 Check Status

```bash
# NPM package
open https://www.npmjs.com/package/@coolver/mcp-home-assistant

# GitHub Actions
open https://github.com/Coolver/mcp-home-assistant/actions

# Who am I?
npm whoami

# Test install
npx @coolver/mcp-home-assistant
```

---

## 🐛 Common Issues

**"Need to authorize"**
```bash
npm login
```

**"402 Payment Required"**
```bash
npm publish --access public  # Don't forget!
```

**"403 Forbidden"**
- Check `npm whoami`
- Verify token in GitHub Secrets

---

## 📝 Files Structure

```
mcp-home-assistant/
├── .github/workflows/
│   ├── publish.yml         # Auto-publish
│   └── test.yml           # Auto-test
├── src/                   # Source code
├── build/                 # Compiled code
├── README.md             # Main docs
├── QUICK_START.md        # Quick guide
├── FINAL_STEPS.md        # This guide
└── package.json          # NPM config
```

---

## ⚡ Quick Commands

```bash
# Build
npm run build

# Version bump
npm version patch

# Publish
npm publish --access public

# Test local
npm pack
npm install -g ./coolver-mcp-home-assistant-1.0.0.tgz

# Unpublish (within 72h only)
npm unpublish @coolver/mcp-home-assistant@1.0.0
```

---

## 🔗 Links

- Package: https://www.npmjs.com/package/@coolver/mcp-home-assistant
- GitHub: https://github.com/Coolver/mcp-home-assistant
- Actions: https://github.com/Coolver/mcp-home-assistant/actions

