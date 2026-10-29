---
name: safe-chain
description: >
  Safely install, audit, and verify project dependencies using Aikido Safe Chain.
  Use when adding npm or python packages, running package installations, auditing
  the supply chain for malware or typosquatting, or inspecting dependency risks.
---

# Safe Chain: Supply Chain Security

Aikido Safe Chain protects this project against malicious packages, dependency confusion, and typosquatting.

## When to Use

1. Before installing any new dependency with `npm`, `pnpm`, `pip`, or `uv`.
2. When scanning project lockfiles or dependencies for supply-chain risks.
3. When verifying package age gates (blocking packages published less than 48 hours ago).

## Procedures

### 1. Verify Safe Chain is Available Locally
Run in workspace:
```powershell
npx safe-chain --version
```

### 2. Installing Packages Safely
Instead of raw `npm install <package>`, run:
```powershell
npx safe-chain npm install <package>
```
Or use the npm script configured in `package.json`:
```powershell
npm run safe-install -- <package>
```

### 3. Scanning Installed Dependencies
To scan the project dependencies for known vulnerabilities and malware:
```powershell
npx safe-chain scan
```

### 4. Handling Blocked Packages
If Safe Chain blocks a download:
- Inspect the alert reason (e.g., typosquatting warning, known malicious payload, package age < 48 hours).
- If it is a newly published package (< 48h) needed for an urgent fix, verify the repository source and commit history before overriding.
