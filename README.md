# Rust Registry Publish

![Latest Release](https://img.shields.io/github/v/release/p6m-actions/rust-registry-publish?style=flat-square&label=Latest%20Release&color=blue)

## Description

A GitHub Action that publishes Rust crates to a registry using [cargo-workspaces](https://github.com/pksunkara/cargo-workspaces). This action simplifies the process of publishing single crates or crates in a workspace, with support for various publishing options.

## Usage

```yaml
- name: Publish Rust crates
  uses: p6m-actions/rust-registry-publish@v1
  with:
    # Optional publishing parameters
    dry_run: false
    registry: crates.io
    # Additional options as needed
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `dry_run` | Perform a dry run without actually publishing | No | `false` |
| `crates_to_publish` | Specific crates to publish (comma-separated) | No | |
| `ignore_crates` | Crates to ignore during publishing (comma-separated) | No | |
| `registry` | Registry to publish to | No | `crates.io` |
| `no_verify` | Skip verification step | No | `false` |
| `allow_dirty` | Allow dirty working directory | No | `false` |
| `from_git` | Use current git tag as version | No | `false` |
| `exact` | Specify exact version dependencies between workspace crates | No | `true` |
| `all_features` | Activate all available features | No | `false` |

## Outputs

This action doesn't define any outputs.

## Examples

### Basic usage

```yaml
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Publish to crates.io
        uses: p6m-actions/rust-registry-publish@v1
```

### Publishing specific crates

```yaml
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Publish selected crates
        uses: p6m-actions/rust-registry-publish@v1
        with:
          crates_to_publish: "my-crate-1,my-crate-2"
```

### Publishing to a custom registry

```yaml
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Publish to custom registry
        uses: p6m-actions/rust-registry-publish@v1
        with:
          registry: my-custom-registry
```

### Dry run before actual publishing

```yaml
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Test publish (dry run)
        uses: p6m-actions/rust-registry-publish@v1
        with:
          dry_run: true
```