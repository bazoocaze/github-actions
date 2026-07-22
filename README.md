# GitHub Actions — Maven + GitHub Packages

Reusable composite actions for Maven projects that consume packages from
GitHub Packages.

## Contents

### `maven-setup/`

Composite action that:
1. Generates a `~/.m2/settings.xml` with GitHub Packages repository (wildcard URL)
   and authentication configured.
2. Sets up JDK via `actions/setup-java` with `overwrite-settings: false`.

**Usage:**

```yaml
steps:
  - uses: actions/checkout@v4

  - uses: bazoocaze/github-actions/maven-setup@v1
    with:
      java-version: "21"
      github-owner: "bazoocaze"

  - name: Build with Maven
    run: mvn -B compile --file pom.xml
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

> **Note:** You still need to pass `GITHUB_TOKEN` via `env:` in every Maven step
> that needs to authenticate against GitHub Packages.