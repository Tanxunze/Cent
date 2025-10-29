# Security Audit Report for Cent Repository

**Date:** October 29, 2025  
**Repository:** Tanxunze/Cent  
**Audit Conducted By:** GitHub Copilot Coding Agent

## Executive Summary

This security audit examined the Cent repository for malicious dependencies and code vulnerabilities. The repository was found to be **SECURE** with no malicious code detected. One security vulnerability was identified in a development dependency (Vite) and has been **FIXED**.

## Audit Scope

The security audit covered:
1. NPM dependency vulnerability scanning against GitHub Advisory Database
2. Source code security analysis
3. Detection of malicious patterns (eval, innerHTML, obfuscated code)
4. Hardcoded secrets and credentials check
5. External domain and network request analysis
6. Package audit using pnpm audit

## Findings Summary

### ✅ No Issues Found

1. **NPM Dependencies Clean**: All 59 runtime and development dependencies passed GitHub Advisory Database checks
2. **No Malicious Code Patterns**: No suspicious JavaScript patterns detected (eval, Function constructor, etc.)
3. **No Hardcoded Secrets**: No hardcoded credentials, API keys, or tokens found in source code
4. **No XSS Vulnerabilities**: No dangerous DOM manipulation methods (innerHTML, dangerouslySetInnerHTML) detected
5. **Code Quality**: Linting passed with no errors (145 files checked)

### ⚠️ Issues Found and Fixed

#### 1. Vite Development Dependency Vulnerabilities (FIXED)

**Severity:** 1 Moderate, 2 Low

**Details:**
- **GHSA-93m4-6634-74q7** (Moderate): Vite allows server.fs.deny bypass via backslash on Windows
  - Affected versions: >=7.1.0 <=7.1.10
  
- **GHSA-g4jq-h2w9-997c** (Low): Vite middleware may serve files starting with the same name with the public directory
  - Affected versions: >=7.1.0 <=7.1.4
  
- **GHSA-jqfw-vq24-v9c3** (Low): Vite's `server.fs` settings were not applied to HTML files
  - Affected versions: >=7.1.0 <=7.1.4

**Resolution:**
- Updated Vite from version ^7.1.2 to ^7.1.11 in package.json
- Installed version 7.1.12 which includes all security patches
- Verified fix with `pnpm audit` - no vulnerabilities remaining

**Impact:** 
These vulnerabilities only affected the development server and would not impact production deployments. However, they could potentially expose local development files on Windows systems.

## Detailed Analysis

### 1. Dependency Analysis

All dependencies were checked against the GitHub Advisory Database:

**Runtime Dependencies (45):**
- @dnd-kit/* (drag and drop components) ✅
- @radix-ui/* (UI components) ✅
- React 19.1.1 and related packages ✅
- octokit 5.0.3 (GitHub API client) ✅
- date-fns, dayjs, echarts, immer, lodash-es, uuid, zod, zustand ✅
- All other dependencies ✅

**Development Dependencies (14):**
- TypeScript 5.8.3 ✅
- Vite 7.1.12 (updated, previously vulnerable) ⚠️ → ✅
- ESLint, Biome (linters) ✅
- Tailwind CSS ✅
- Workbox (PWA service worker) ✅

### 2. Code Security Analysis

**Checked for:**
- Dynamic code execution: `eval()`, `Function()` constructor - ✅ None found
- DOM manipulation: `innerHTML`, `dangerouslySetInnerHTML`, `document.write` - ✅ None found
- Code obfuscation: Base64 encoded code, `fromCharCode` chains - ✅ None found (only legitimate base64 for file conversion)
- Dynamic script loading: Unauthorized external scripts - ✅ Only legitimate React lazy loading

### 3. External Domains Analysis

All external domains used in the application are legitimate:

1. **https://oncent-backend.linkai.work** - OAuth backend for GitHub authentication
2. **https://github.com** - GitHub repository operations
3. **https://raw.githubusercontent.com** - GitHub raw file access for assets
4. **https://glink25.github.io** - Project documentation and blog
5. **https://s3.bmp.ovh** - Apple touch icon CDN (PWA manifest)
6. **http://localhost:8787** - Local development backend (commented out)

### 4. Data Storage Analysis

The application uses:
- **localStorage**: For theme preferences, OAuth tokens, and sync settings
- **IndexedDB**: For bill storage via the Gitray library
- **No cookies**: Application does not use cookies

All data storage is client-side only, with data synced to user's own GitHub repositories.

### 5. Service Worker Analysis

The PWA service worker (`src/sw.ts`) uses Workbox for:
- Precaching static assets
- Navigation route handling with Safari compatibility fix

No suspicious behavior detected in the service worker.

## Recommendations

### Implemented ✅
1. **Update Vite dependency** - COMPLETED
2. **Verify no vulnerabilities remain** - COMPLETED

### Best Practices (Already Followed)
- ✅ No eval or dangerous code execution patterns
- ✅ No hardcoded secrets in source code
- ✅ Proper use of environment variables (.env.example provided)
- ✅ Security-conscious localStorage usage
- ✅ Linting and type checking enabled
- ✅ Dependencies kept relatively up-to-date

### Future Recommendations
1. **Add Dependabot**: Configure GitHub Dependabot to automatically check for dependency updates
2. **Add CodeQL scanning**: Set up GitHub Actions with CodeQL for continuous security scanning
3. **Content Security Policy**: Consider adding CSP headers when deploying
4. **Subresource Integrity**: Add SRI hashes for CDN resources (apple-touch-icon)

## Conclusion

The Cent repository is **SECURE and SAFE** to use. No malicious code or dependencies were found. The one security vulnerability identified in the Vite development dependency has been successfully patched. The codebase follows security best practices and does not exhibit any concerning patterns.

All runtime dependencies are clean and from trusted sources. The application architecture is sound, with proper separation between client-side data storage and GitHub-based synchronization.

---

**Audit Status:** ✅ PASSED  
**Vulnerabilities Fixed:** 3 (1 moderate, 2 low)  
**Malicious Code Found:** None  
**Recommended Action:** Safe to use and deploy
