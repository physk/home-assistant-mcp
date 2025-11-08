# GitHub Actions Setup for Automated NPM Publishing

## 🎯 What This Does

GitHub Actions will **automatically publish** your package to NPM when you:
- Create a GitHub Release
- Push a git tag (e.g., `v1.0.1`)

---

## 🔐 Step 1: Create NPM Automation Token

### 1. Login to NPM

Go to: https://www.npmjs.com/settings/YourUsername/tokens

### 2. Create New Token

- Click **"Generate New Token"**
- Select **"Automation"** (this type works with CI/CD without 2FA)
- Copy the token (you'll only see it once!)

**Example token:**
```
npm_aBcDeFgHiJkLmNoPqRsTuVwXyZ1234567890
```

⚠️ **Save this token securely! You won't be able to see it again.**

---

## 🔑 Step 2: Add Token to GitHub Secrets

### 1. Go to Your Repository Settings

Open: https://github.com/Coolver/mcp-home-assistant/settings/secrets/actions

### 2. Create New Secret

- Click **"New repository secret"**
- **Name:** `NPM_TOKEN`
- **Value:** Paste your NPM token
- Click **"Add secret"**

---

## ✅ Step 3: Verify Setup

### Check GitHub Actions are enabled:

1. Go to: https://github.com/Coolver/mcp-home-assistant/settings/actions
2. Ensure **"Allow all actions and reusable workflows"** is selected

### Verify Workflows Exist:

Your repository now has:

```
.github/
└── workflows/
    ├── publish.yml  # Auto-publish on release/tag
    └── test.yml     # Auto-test on push
```

---

## 🚀 How to Use

### Method 1: Create Release (Recommended)

1. **Update version:**
```bash
cd /Users/Coolver_1/Projects/smart-home/mcp-home-assistant

# Update version
npm version patch  # or minor/major

# Push changes and tags
git push && git push --tags
```

2. **Create Release on GitHub:**
   - Go to: https://github.com/Coolver/mcp-home-assistant/releases/new
   - Select tag: `v1.0.1`
   - Title: `v1.0.1`
   - Description: Copy from CHANGELOG.md
   - Click **"Publish release"**

3. **GitHub Actions will automatically:**
   - ✅ Checkout code
   - ✅ Setup Node.js
   - ✅ Install dependencies
   - ✅ Build package
   - ✅ Publish to NPM

### Method 2: Push Tag Directly

```bash
# Update version
npm version patch

# Push (tag is auto-created by npm version)
git push && git push --tags
```

GitHub Actions triggers automatically when tag is pushed!

---

## 📊 Monitor Workflow

### Watch the Action Run:

1. Go to: https://github.com/Coolver/mcp-home-assistant/actions
2. Click on the running workflow
3. Watch real-time logs

### Successful Run Looks Like:

```
✅ Checkout code
✅ Setup Node.js
✅ Install dependencies
✅ Build package
✅ Publish to NPM
   + @coolver/mcp-home-assistant@1.0.1
```

---

## 🔍 What Each Workflow Does

### `publish.yml` - Automated Publishing

**Triggers:**
- When you create a GitHub Release
- When you push a tag matching `v*` (e.g., `v1.0.1`)

**Actions:**
1. Checks out your code
2. Sets up Node.js 20
3. Installs dependencies with `npm ci`
4. Builds project with `npm run build`
5. Publishes to NPM with `--access public`

### `test.yml` - Continuous Integration

**Triggers:**
- Every push to `main` branch
- Every pull request to `main`

**Actions:**
1. Tests on Node.js 18 and 20
2. Installs dependencies
3. Builds project
4. Verifies build output exists

---

## 🛠️ Workflow Customization

### Change Node.js Version

Edit `.github/workflows/publish.yml`:

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20'  # Change to 18, 20, 21, etc.
```

### Add Tests Before Publishing

Add before `Publish to NPM` step:

```yaml
- name: Run tests
  run: npm test
```

### Add Dry Run Option

Test publishing without actually publishing:

```yaml
- name: Dry run publish
  run: npm publish --dry-run
```

---

## 🐛 Troubleshooting

### "NPM_TOKEN not found"

**Solution:** Make sure you added `NPM_TOKEN` to GitHub Secrets (Step 2)

### "403 Forbidden" when publishing

**Solutions:**
- Check NPM token has **publish** permission
- Verify token is **Automation** type (not Classic or Granular)
- Make sure package name isn't taken

### Workflow doesn't trigger

**Check:**
- Actions are enabled in repository settings
- Tag format matches `v*` (e.g., `v1.0.0` not `1.0.0`)
- You pushed the tag: `git push --tags`

### Build fails

**Check:**
- `npm ci` requires `package-lock.json` in repository
- All dependencies are in `package.json`
- Build script works locally: `npm run build`

---

## 📝 Complete Workflow Example

### Full Update and Publish Process:

```bash
# 1. Make your changes
cd /Users/Coolver_1/Projects/smart-home/mcp-home-assistant

# 2. Update version
npm version patch
# This:
# - Updates package.json version
# - Creates git commit
# - Creates git tag

# 3. Update CHANGELOG.md manually
# Add your changes to CHANGELOG.md

# 4. Commit changelog
git add CHANGELOG.md
git commit -m "Update changelog for v1.0.1"

# 5. Push everything
git push && git push --tags

# 6. Create GitHub Release (optional but recommended)
# Go to: https://github.com/Coolver/mcp-home-assistant/releases/new
# Select the tag, add release notes, publish

# 7. Watch GitHub Actions automatically publish to NPM!
# https://github.com/Coolver/mcp-home-assistant/actions
```

**That's it!** NPM package will be published automatically! 🎉

---

## 🎯 Benefits of This Setup

✅ **Automated** - No manual npm publish needed  
✅ **Consistent** - Same build process every time  
✅ **Secure** - Token stored in GitHub Secrets  
✅ **Tested** - Builds verified before publishing  
✅ **Tracked** - Full audit trail in Actions logs  
✅ **Fast** - Publish happens in ~1-2 minutes  

---

## 🔄 Workflow Diagram

```
Developer                GitHub                    NPM
    |                       |                       |
    |-- git push v1.0.1 -->|                       |
    |                       |                       |
    |                       |-- Trigger Workflow    |
    |                       |-- Checkout Code       |
    |                       |-- Setup Node          |
    |                       |-- Build Package       |
    |                       |-- npm publish ------->|
    |                       |                       |
    |                       |<----- Success --------|
    |<--- Notification -----|                       |
    |                       |                       |
```

---

## ✅ Setup Checklist

- [ ] NPM account created
- [ ] NPM Automation token generated
- [ ] Token added to GitHub Secrets as `NPM_TOKEN`
- [ ] GitHub Actions workflows committed (`.github/workflows/`)
- [ ] GitHub Actions enabled in repository settings
- [ ] First manual publish completed: `npm publish --access public`
- [ ] Tested with version bump: `npm version patch && git push --tags`

---

**Now your package publishes automatically!** 🚀

Every time you create a release or push a tag, GitHub Actions handles the rest!

