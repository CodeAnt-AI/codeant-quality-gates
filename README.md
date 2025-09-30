# CodeAnt CI Scan Action

This GitHub Action runs CodeAnt CI security and code quality analysis on your repository. It integrates seamlessly with your CI/CD pipeline to provide automated code scanning and security insights.

## Features

- 🔒 Security vulnerability detection
- 📊 Code quality analysis
- 🚀 Fast and efficient scanning
- 🔄 Seamless CI/CD integration
- 📈 Detailed reports and insights

## Inputs

| Name          | Description                                      | Required | Default                  |
|---------------|--------------------------------------------------|----------|--------------------------|
| access_token  | GitHub PAT or repository token for authentication | Yes      | -                        |
| api_base      | Base URL for CodeAnt API                         | No       | https://api.codeant.ai   |

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

### Custom API Base URL

```yaml
- name: Run CodeAnt Scan
  uses: CodeAnt-AI/codeant-ci-scan@v1
  with:
    access_token: ${{ secrets.ACCESS_TOKEN_GITHUB }}
    api_base: https://custom.codeant.ai
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

[Add your license here]
