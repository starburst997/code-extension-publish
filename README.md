# Code Extension Publish

A GitHub Action for building and publishing VSCode/Cursor extensions to VSCode Marketplace and Open VSX Registry.

## Features

- Build and package VSCode/Cursor extensions
- Publish to VSCode Marketplace and/or Open VSX
- Support for platform-specific builds
- Optional linting and version management
- Customizable build commands

## Usage

```yaml
- name: Publish Extension
  uses: starburst997/code-extension-publish@v1
  with:
    vsce-pat: ${{ secrets.VSCE_PAT }}
    ovsx-pat: ${{ secrets.OVSX_PAT }}
    platforms: "darwin-x64,darwin-arm64"
```

## Inputs

| Input           | Description                         | Default          | Required |
| --------------- | ----------------------------------- | ---------------- | -------- |
| `node-version`  | Node.js version to use              | `20`             | No       |
| `version`       | Version to set in package.json      | -                | No       |
| `lint`          | Run lint command before packaging   | `true`           | No       |
| `lint-command`  | Lint script name from package.json  | `lint`           | No       |
| `build-command` | Build script name from package.json | `package-bundle` | No       |
| `platforms`     | Target platforms (comma-separated)  | -                | No       |
| `vsce-pat`      | VSCode Marketplace PAT              | -                | No       |
| `ovsx-pat`      | Open VSX Registry PAT               | -                | No       |
| `package-name`  | Custom package name for VSIX files  | -                | No       |

## Examples

### Basic publish to both marketplaces

```yaml
- uses: starburst997/code-extension-publish@v1
  with:
    vsce-pat: ${{ secrets.VSCE_PAT }}
    ovsx-pat: ${{ secrets.OVSX_PAT }}
```

### Platform-specific builds

```yaml
- uses: starburst997/code-extension-publish@v1
  with:
    vsce-pat: ${{ secrets.VSCE_PAT }}
    platforms: "darwin-x64,darwin-arm64,linux-x64,win32-x64"
```

### Custom build and no linting

```yaml
- uses: starburst997/code-extension-publish@v1
  with:
    vsce-pat: ${{ secrets.VSCE_PAT }}
    lint: false
    build-command: "custom-build"
```

### With version update

```yaml
- uses: starburst997/code-extension-publish@v1
  with:
    version: "1.2.3"
    vsce-pat: ${{ secrets.VSCE_PAT }}
```

## Platform Values

Common platform values for the `platforms` input:

- `darwin-x64` - macOS Intel
- `darwin-arm64` - macOS Apple Silicon
- `linux-x64` - Linux 64-bit
- `linux-arm64` - Linux ARM 64-bit
- `win32-x64` - Windows 64-bit
- `win32-arm64` - Windows ARM 64-bit
- `alpine-x64` - Alpine Linux 64-bit
- `alpine-arm64` - Alpine Linux ARM 64-bit

## Requirements

Your extension's `package.json` should have:

- `package-bundle` script (or provide custom `build-command`)
- `lint` script if linting is enabled

## License

MIT
