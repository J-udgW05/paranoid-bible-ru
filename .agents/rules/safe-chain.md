# Safe Chain Supply-Chain Protection Rule

Before installing or introducing any new third-party dependencies into this project:
1. **Always Verify First**: Run `@aikidosec/safe-chain` to check packages against malware, typosquatting, and unvetted zero-day releases (< 48 hours old).
2. **Local Project Commands**:
   - For npm packages: `npx safe-chain npm install <package>` or `npm run safe-install -- <package>`
   - For auditing existing dependencies: `npx safe-chain scan` or `npm audit`
   - For Python dependencies: `npx safe-chain pip install <package>`
3. **Never Blindly Bypass Warnings**: If Safe Chain flags a package as malicious, suspicious, or under the 48-hour age gate, halt and investigate before proceeding.
