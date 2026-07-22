# GitHub Actions — Maven + GitHub Packages

Reusable composite actions and configuration files for Maven projects
that consume packages from GitHub Packages.

## Contents

### `maven-setup/`

Composite action that:
1. Copies a versioned `settings.xml` into `~/.m2/`
2. Sets up JDK via `actions/setup-java` with `overwrite-settings: false`
3. Configures authentication for GitHub Packages

**Usage:**

```yaml
steps:
  - uses: actions/checkout@v4

  - uses: bazoocaze/github-actions/maven-setup@v1
    with:
      java-version: "21"
      settings-path: ".github/workflows/settings.xml"

  - name: Build with Maven
    run: mvn -B compile --file pom.xml
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

> **Note:** You still need to pass `GITHUB_TOKEN` via `env:` in every Maven step
> that needs to authenticate against GitHub Packages.