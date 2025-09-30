# CodeAnt Quality Gate Scan Action

This GitHub Action runs CodeAnt CI quality gate scan with secret detection and code quality analysis on your repository. It integrates seamlessly with your CI/CD pipeline to provide automated scanning and will fail your workflow if secrets are detected or quality gates fail.

## Features

- 🔒 Secret detection and security scanning
- 📊 Code quality gate enforcement
- 🚀 Fast and efficient scanning
- 🔄 Seamless CI/CD integration
- 📈 Detailed reports and insights
- ⏱️ Configurable polling and timeout
- ✅ Pass/Fail workflow status based on scan results

## Inputs

| Name          | Description                                      | Required | Default                  |
|---------------|--------------------------------------------------|----------|--------------------------|
| access_token  | GitHub PAT or repository token for authentication | Yes      | -                        |
| api_base      | Base URL for CodeAnt API                         | No       | https://api.codeant.ai   |
| timeout       | Maximum time in seconds to wait for results      | No       | 300                      |
| poll_interval | Time in seconds between polling attempts         | No       | 15                       |

## Usage

### Basic Example

```yaml
name: CodeAnt CI Scan

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - name: Run CodeAnt Scan
        uses: CodeAnt-AI/codeant-ci-scan@v1
        with:
          access_token: ${{ secrets.GITHUB_TOKEN }}
```

### With Custom Configuration

```yaml
- name: Run CodeAnt Quality Gate Scan
  uses: CodeAnt-AI/codeant-ci-scan@v1
  with:
    access_token: ${{ secrets.ACCESS_TOKEN_GITHUB }}
    api_base: https://api.codeant.ai
    timeout: 600           # Wait up to 10 minutes for results
    poll_interval: 20      # Poll every 20 seconds
```

### Complete Workflow Example

```yaml
name: CodeAnt Quality Gate

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  quality-gate:
    name: Quality Gate Scan
    runs-on: ubuntu-latest
    steps:
      - name: Run CodeAnt Quality Gate Scan
        uses: CodeAnt-AI/codeant-ci-scan@v1
        with:
          access_token: ${{ secrets.GITHUB_TOKEN }}
          api_base: https://api.codeant.ai
          timeout: 300
          poll_interval: 15
```

## Testing from Another Repository

To test this action before publishing to the GitHub Marketplace:

1. **Push this action to a GitHub repository** (e.g., `CodeAnt-AI/codeant-ci-scan`)

2. **In another repository**, reference it using the repository path:

```yaml
- name: Test CodeAnt Scan
  uses: CodeAnt-AI/codeant-ci-scan@main  # or use a specific branch/tag
  with:
    access_token: ${{ secrets.GITHUB_TOKEN }}
```

3. **For testing specific commits or branches:**
```yaml
uses: CodeAnt-AI/codeant-ci-scan@feature-branch
# or
uses: CodeAnt-AI/codeant-ci-scan@abc1234  # commit SHA
```

## How It Works

1. **Checkout**: Checks out your repository code
2. **Fetch Script**: Downloads the quality gates scanning script from CodeAnt API
3. **Start Scan**: Initiates the quality gate scan on CodeAnt servers
4. **Poll Results**: Continuously polls for scan results until completion or timeout
5. **Report Status**: Reports pass/fail status with GitHub annotations

## Expected Output

### When Quality Gate Passes:
```
✅ Quality Gate PASSED - No secrets detected
```
The workflow continues successfully.

### When Quality Gate Fails:
```
❌ Quality Gate FAILED - Secrets detected or scan error
```
The workflow fails, preventing merge/deployment.

## Required Permissions

The `access_token` requires the following permissions:
- `repo` - Full control of private repositories (for reading code)
- `contents: read` - Read access to repository contents

## Publishing to GitHub Marketplace

Before publishing:

1. ✅ Create a release with semantic versioning (e.g., v1.0.0)
2. ✅ Add a LICENSE file
3. ✅ Test thoroughly from another repository
4. ✅ Ensure action.yml has proper branding and metadata

## Support

For issues, questions, or contributions, please visit the [GitHub repository](https://github.com/CodeAnt-AI/codeant-ci-scan).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
