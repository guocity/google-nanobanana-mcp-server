# Publishing Checklist for nanobanana-mcp

## Pre-Publishing Checklist

### Code Quality
- [ ] `npm run build` completes successfully
- [ ] `npm run typecheck` passes with no errors
- [ ] All TypeScript code compiles
- [ ] No console.error() messages in main code

### Package Configuration
- [ ] package.json name is `nanobanana-mcp`
- [ ] version is set correctly (e.g., `1.0.0`)
- [ ] description is accurate and concise
- [ ] keywords are relevant and helpful
- [ ] license is set to `Apache-2.0`
- [ ] repository URL points to GitHub
- [ ] homepage URL is correct
- [ ] bugs URL is correct
- [ ] author information is complete
- [ ] node engine requirement is `>=18.0.0`
- [ ] files array excludes node_modules and dist not built

### Documentation
- [ ] README.md is comprehensive and clear
- [ ] README includes installation instructions from npm
- [ ] README documents all available tools
- [ ] README includes usage examples
- [ ] README has troubleshooting section
- [ ] LICENSE file exists in root
- [ ] Main repo README mentions MCP server availability

### Git Repository
- [ ] All changes are committed
- [ ] git status is clean
- [ ] No uncommitted files
- [ ] README.md exists in mcp-server folder
- [ ] .gitignore properly configured

## Publishing Steps

### Setup
- [ ] Create npm account at npmjs.com
- [ ] Enable 2FA on npm account
- [ ] Run `npm login` and verify with `npm whoami`

### Pre-Publish Verification
- [ ] Run `npm publish --dry-run` to see what will be published
- [ ] Verify file list includes only necessary files
- [ ] Check package size is reasonable

### Publishing
- [ ] Run `npm publish` from mcp-server directory
- [ ] Enter OTP when prompted (if 2FA enabled)
- [ ] Wait for publish to complete

### Post-Publishing Verification
- [ ] Run `npm view nanobanana-mcp` to verify package exists
- [ ] Visit https://www.npmjs.com/package/nanobanana-mcp in browser
- [ ] Test installation: `npm install -g nanobanana-mcp`
- [ ] Verify command works: `nanobanana-mcp` runs without errors

### Documentation & Promotion
- [ ] Update main README.md with npm installation link
- [ ] Add npm badge to README
- [ ] Create GitHub release with release notes
- [ ] Share on social media (Twitter, Reddit, etc.)
- [ ] Add to Awesome MCP list if applicable
- [ ] Document in changelog

## Quick Command Reference

```bash
# Navigate to mcp-server directory
cd mcp-server

# Build and test
npm run build
npm run typecheck

# Login to npm
npm login

# Dry run
npm publish --dry-run

# Publish
npm publish

# Verify
npm view nanobanana-mcp
npm install -g nanobanana-mcp
```

## Files Modified/Created

### Modified:
- `mcp-server/package.json` - Updated package name to `nanobanana-mcp`, added npm publishing metadata
- `README.md` - Added mention of MCP server availability

### Created:
- `mcp-server/README.md` - Comprehensive MCP server documentation
- `NPM_PUBLISHING_GUIDE.md` - Detailed publishing instructions
- `PUBLISHING_CHECKLIST.md` - This file

## Troubleshooting Quick Links

| Issue | Solution |
|-------|----------|
| 403 Forbidden | Run `npm login` first |
| 404 Not Found | Verify package name is unique |
| Build failed | Check Node.js version (18+), run `npm install` |
| Type errors | Run `npm run typecheck` to identify issues |
| Files missing from package | Check `files` array in package.json |

## Next Steps After Publishing

1. Tag the release in git: `git tag v1.0.0 && git push --tags`
2. Create GitHub release with release notes
3. Update project website/portfolio
4. Share accomplishment in communities
5. Plan next features/improvements
6. Set up automated publishing (optional GitHub Actions)

---

**Package Name**: nanobanana-mcp  
**npm Registry**: https://www.npmjs.com/package/nanobanana-mcp  
**Repository**: https://github.com/gemini-cli-extensions/nanobanana
