# XploitScan Security Scanner - GitHub Action

Scan your code for security vulnerabilities on every pull request. Built for AI-generated code from Cursor, Lovable, Bolt, Replit, and other vibe coding tools.

- 30 core security rules (up to 131 with Pro)
- SARIF output for GitHub Security tab
- PR comments with security grade and findings summary
- Configurable fail thresholds to block merges on critical/high issues

## Usage

Add this to `.github/workflows/xploitscan.yml`:

```yaml
name: Security Scan
on: [push, pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: bgage72590/xploitscan-action@v1
        with:
          fail-on: critical
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `path` | Path to scan | `.` |
| `fail-on` | Fail if findings at this severity or higher: `critical`, `high`, `medium`, `low`, `none` | `none` |
| `sarif-file` | Path to write SARIF output | `xploitscan-results.sarif` |
| `comment` | Post a summary comment on PRs | `true` |

## Outputs

| Output | Description |
|--------|-------------|
| `grade` | Security grade (A+ to F) |
| `score` | Security score (0-100) |
| `findings-count` | Total number of findings |
| `critical-count` | Number of critical findings |
| `high-count` | Number of high findings |
| `sarif-file` | Path to the SARIF output file |

## What it does

1. Installs and runs `xploitscan` against your codebase
2. Uploads SARIF results to the GitHub Security tab
3. Posts a security summary comment on pull requests
4. Optionally fails the check if findings exceed your threshold

## Example PR Comment

When code changes are detected:

> **Grade: B** | Score: 72/100 | 5 findings
>
> | Severity | Count |
> |----------|-------|
> | Critical | 1 |
> | High | 2 |
> | Medium | 2 |

When no scannable code is found (config/docs changes):

> **No scannable code found in this PR.** This PR may only contain config, docs, or text changes.

## Supported Languages

JavaScript, TypeScript, Python, Ruby, Go, Rust, Java, PHP, Swift, Kotlin, C#, and 30+ more. Also scans Dockerfile, Terraform, Kubernetes, CI/CD workflows, .env files, and package manifests.

## Links

- [XploitScan Website](https://xploitscan.com)
- [Documentation](https://xploitscan.com/docs)
- [CLI on npm](https://www.npmjs.com/package/xploitscan)
- [Changelog](https://xploitscan.com/changelog)

## License

MIT

---

Built by [Cipherline LLC](https://xploitscan.com) | [admin@xploitscan.com](mailto:admin@xploitscan.com)
