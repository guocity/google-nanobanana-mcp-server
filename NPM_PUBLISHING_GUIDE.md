# Publishing nanobanana-mcp to npm

This guide will walk you through publishing the `nanobanana-mcp` package to npm.js.com.

## Prerequisites

1. **npm Account**: Create an account at [npmjs.com](https://www.npmjs.com) if you don't have one
2. **Node.js & npm**: Ensure you have Node.js 18+ and npm installed
3. **Git**: Make sure you're in the git repository and all changes are committed
4. **2FA (Optional but Recommended)**: Enable two-factor authentication on your npm account for security

## Step-by-Step Publishing Instructions

### 1. Prepare Your Local Environment

First, navigate to the mcp-server directory:

```bash
cd mcp-server
```

Verify the package.json is correctly configured:

```bash
cat package.json | head -20
```

You should see:
- `"name": "nanobanana-mcp"`
- `"version": "1.0.0"` (or your desired version)
- Repository and homepage URLs configured
- Keywords for discoverability
- License specified

### 2. Build and Test the Package

Build the TypeScript code:

```bash
npm run build
```

Verify the build was successful by checking the dist folder:

```bash
ls -la dist/
```

Run type checking:

```bash
npm run typecheck
```

### 3. Login to npm

Authenticate with your npm account:

```bash
npm login
```

You'll be prompted to enter:
- **Username**: Your npm username
- **Password**: Your npm password
- **Email**: Your registered email
- **OTP (if 2FA enabled)**: One-time password from your authenticator

Verify you're logged in:

```bash
npm whoami
```

### 4. (Optional) Perform a Dry Run

Before publishing, you can perform a dry run to see what will be published:

```bash
npm publish --dry-run
```

This shows you:
- Which files will be included (based on `files` in package.json)
- The package size
- Any warnings or issues

### 5. Publish to npm

Publish your package:

```bash
npm publish
```

If you have 2FA enabled, you'll need to provide an OTP code when prompted.

You should see output like:
```
npm notice 📦 nanobanana-mcp@1.0.0
npm notice === Tarball Details ===
npm notice name:          nanobanana-mcp
npm notice version:       1.0.0
npm notice filename:      nanobanana-mcp-1.0.0.tgz
npm notice package size:  XX KB
npm notice unpacked size: XX KB
npm notice shasum:        [hash]
npm notice integrity:     sha512-[integrity-hash]
npm notice total files:   X
npm notice === Dist Files ===
...
+ nanobanana-mcp@1.0.0
```

### 6. Verify the Publication

Verify your package is published:

```bash
npm view nanobanana-mcp
```

Or visit: https://www.npmjs.com/package/nanobanana-mcp

### 7. Test Installation

Test that the package can be installed from npm:

```bash
npm install -g nanobanana-mcp
```

Verify it works:

```bash
nanobanana-mcp --help
```

Or check the version:

```bash
nanobanana-mcp --version
```

## Publishing Updates

When you have bug fixes or new features to release:

### 1. Update Version

Use semantic versioning in package.json:

```bash
# For patch updates (bug fixes)
npm version patch

# For minor updates (new features, backwards compatible)
npm version minor

# For major updates (breaking changes)
npm version major
```

This automatically updates package.json, creates a git tag, and commits the change.

### 2. Update CHANGELOG

Update the root [CHANGELOG.md](../CHANGELOG.md) with version history.

### 3. Commit and Push

```bash
git push
git push --tags
```

### 4. Publish

```bash
npm publish
```

## Troubleshooting

### "npm ERR! 403 Forbidden"

This usually means:
- You're not logged in: Run `npm login`
- The package name is already taken: Try a different name
- Your account doesn't have permission: Verify ownership

**Solution**: 

```bash
npm login
npm publish
```

### "npm ERR! 404 Not Found"

The registry can't find your package. This is normal for a new package. Try:

```bash
npm logout
npm login
npm publish
```

### "npm ERR! You do not have permission"

You may not have publish rights to this package name. Verify:

```bash
npm owner list nanobanana-mcp
```

### Package Size Too Large

If your package is too large, clean up:

```bash
# Remove node_modules
rm -rf node_modules dist

# Ensure .gitignore prevents these from being packaged
cat .gitignore
```

Update package.json `files` array to only include necessary files:

```json
"files": [
  "dist",
  "README.md",
  "LICENSE"
]
```

### Need to Unpublish

**Important**: You can only unpublish within 72 hours of publishing, and only for v6.0.0+

```bash
npm unpublish nanobanana-mcp@1.0.0
```

To remove all versions:

```bash
npm unpublish nanobanana-mcp --force
```

## After Publishing

### Update Documentation

Update the main [README.md](../README.md) to include npm installation instructions:

```bash
npm install -g nanobanana-mcp
```

### Set Up CI/CD (Optional)

Consider setting up GitHub Actions to automatically publish on release:

Create `.github/workflows/publish.yml`:

```yaml
name: Publish to npm

on:
  release:
    types: [published]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
          registry-url: 'https://registry.npmjs.org'
      - working-directory: ./mcp-server
        run: npm run build
      - working-directory: ./mcp-server
        run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Add npm Badge

Add to README.md:

```markdown
[![npm version](https://badge.fury.io/js/nanobanana-mcp.svg)](https://www.npmjs.com/package/nanobanana-mcp)
```

## NPM Registry Settings

### Set Package Visibility

By default, packages are public. To keep it that way, ensure in package.json:

```json
"private": false
```

### Add Organization

If publishing to an organization:

```bash
npm publish --access public
```

### Configure npm Registry Scopes

For scoped packages (optional):

```json
"name": "@yourorg/nanobanana-mcp"
```

## Security Best Practices

1. **Use npm 2FA**: Enable two-factor authentication
2. **Use Tokens**: For CI/CD, use npm tokens instead of passwords
3. **Review package.json**: Ensure all URLs are correct before publishing
4. **Keep Dependencies Updated**: Run `npm audit` and fix vulnerabilities
5. **Sign Commits**: Use git commit signing

## Resources

- [npm Official Publishing Guide](https://docs.npmjs.com/packages-and-modules/contributing-packages-to-the-registry)
- [npm Semantic Versioning](https://docs.npmjs.com/about-semantic-versioning)
- [npm Security Best Practices](https://docs.npmjs.com/packages-and-modules/npm-package-security)
- [Model Context Protocol Documentation](https://modelcontextprotocol.io/)

## Next Steps

After publishing, share your package:

- Tweet about it: Include `@npmjs` and relevant hashtags
- Add to Awesome Lists: Check if there's an Awesome MCP list
- Update your portfolio/website
- Share in relevant communities (Reddit, Discord, etc.)

Happy publishing! 🎉
