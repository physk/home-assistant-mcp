# NPM Registration and Publishing Guide

## 📝 Step 1: Create NPM Account

### Register on NPM.com

1. Go to: https://www.npmjs.com/signup
2. Fill in:
   - **Username:** Choose your username (e.g., `coolver`)
   - **Email:** Your email address
   - **Password:** Strong password
3. **Verify email** - check your inbox and click verification link
4. **Optional:** Set up 2FA (Two-Factor Authentication) - highly recommended!

### Enable 2FA (Recommended for Security)

1. Go to: https://www.npmjs.com/settings/YourUsername/tfa
2. Choose **Authorization and Publishing** (most secure)
3. Scan QR code with authenticator app (Google Authenticator, Authy, etc.)
4. Save backup codes!

---

## 🔐 Step 2: Login via CLI

Open terminal and login:

```bash
npm login
```

You'll be asked:
```
Username: coolver
Password: ********
Email: your@email.com
```

If 2FA is enabled, you'll also need to enter OTP code.

**Verify login:**
```bash
npm whoami
# Should output: coolver
```

---

## 📦 Step 3: Publish Your Package

### First Time Publishing

```bash
cd /Users/Coolver_1/Projects/smart-home/mcp-home-assistant

# Make sure everything is built
npm run build

# Publish with public access (for scoped packages)
npm publish --access public
```

**Expected output:**
```
npm notice 
npm notice package: @coolver/mcp-home-assistant@1.0.0
npm notice === Tarball Contents === 
npm notice 46.5kB total
npm notice === Tarball Details === 
npm notice name:          @coolver/mcp-home-assistant
npm notice version:       1.0.0
npm notice filename:      coolver-mcp-home-assistant-1.0.0.tgz
npm notice package size:  10.8 kB
npm notice unpacked size: 46.5 kB
npm notice total files:   15
npm notice 
+ @coolver/mcp-home-assistant@1.0.0
```

**That's it!** Your package is now live! 🎉

---

## 🌍 Step 4: Verify Publication

### Check your package page:

- **NPM:** https://www.npmjs.com/package/@coolver/mcp-home-assistant
- **Install test:** `npm install -g @coolver/mcp-home-assistant`
- **NPX test:** `npx @coolver/mcp-home-assistant --help`

### Package should appear in:

- Your NPM profile: https://www.npmjs.com/~coolver
- Search results: https://www.npmjs.com/search?q=mcp-home-assistant
- Download stats: https://npm-stat.com/charts.html?package=@coolver/mcp-home-assistant

---

## 🔄 Step 5: Future Updates

When you want to publish a new version:

```bash
# 1. Make your changes to code

# 2. Update version (choose one):
npm version patch   # 1.0.0 -> 1.0.1 (bug fixes)
npm version minor   # 1.0.0 -> 1.1.0 (new features)
npm version major   # 1.0.0 -> 2.0.0 (breaking changes)

# 3. This automatically:
#    - Updates package.json version
#    - Creates git commit
#    - Creates git tag

# 4. Build
npm run build

# 5. Push to GitHub
git push && git push --tags

# 6. Publish to NPM
npm publish --access public
```

---

## ⚠️ Important Notes

### Scoped Packages (@coolver/package-name)

- Must use `--access public` when publishing
- Without it, npm tries to publish as private (requires paid account)

### Package Naming

- ✅ `@coolver/mcp-home-assistant` - scoped, organized
- ❌ `mcp-home-assistant` - might be taken, less organized

### Version Numbers (Semantic Versioning)

- **MAJOR** (1.0.0 → 2.0.0): Breaking changes
- **MINOR** (1.0.0 → 1.1.0): New features, backward compatible
- **PATCH** (1.0.0 → 1.0.1): Bug fixes only

---

## 🛡️ Security Best Practices

### 1. Enable 2FA

Always enable Two-Factor Authentication on NPM!

```bash
npm profile enable-2fa auth-and-writes
```

### 2. Use Automation Tokens for CI/CD

For GitHub Actions (we'll set up next):

```bash
# Create automation token (no 2FA required for CI)
npm token create --read-only
# or
npm token create --publish  # for publishing
```

Save this token for GitHub Actions setup.

### 3. Never Commit Tokens

Add to `.gitignore`:
```
.npmrc
.env
*.env
```

---

## 🎯 Common Issues

### "You need to authorize this machine"

**Solution:** Run `npm login` again

### "402 Payment Required"

**Solution:** Add `--access public` when publishing scoped packages

### "403 Forbidden"

**Solutions:**
- Check you're logged in: `npm whoami`
- Verify package name isn't taken
- Check you have publish rights

### "E404 Not Found"

**Solution:** Package name is available (good for first publish!)

---

## ✅ Checklist Before Publishing

- [ ] Logged in to NPM (`npm whoami`)
- [ ] Package built successfully (`npm run build`)
- [ ] Tests pass (if any)
- [ ] README.md is complete
- [ ] CHANGELOG.md updated
- [ ] Version bumped correctly
- [ ] Git committed and pushed
- [ ] No sensitive data in code

---

## 📊 After Publishing

Your package is now:

- ✅ Available worldwide via NPM
- ✅ Installable with `npm install`
- ✅ Usable with `npx`
- ✅ Discoverable in NPM search
- ✅ Versioned and tracked

**Next:** Set up automated publishing with GitHub Actions! 🚀

