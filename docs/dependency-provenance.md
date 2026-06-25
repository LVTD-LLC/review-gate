# Dependency Provenance

Review Gate commits `Cargo.lock` because the CLI and GitHub Action wrapper are executable artifacts.

The lockfile was regenerated with Cargo 1.96 using:

```bash
cargo generate-lockfile
```

The current Serde dependency shape is expected for the latest locked versions:

```text
serde 1.0.228
  serde_core 1.0.228
  serde_derive 1.0.228

serde_json 1.0.150
  itoa 1.0.18
  memchr 2.8.2
  serde 1.0.228
  serde_core 1.0.228
  zmij 1.0.21
```

`cargo metadata --locked` resolves these packages from the official crates.io index:

```text
serde       registry+https://github.com/rust-lang/crates.io-index 1.0.228
serde_core  registry+https://github.com/rust-lang/crates.io-index 1.0.228
serde_json  registry+https://github.com/rust-lang/crates.io-index 1.0.150
zmij        registry+https://github.com/rust-lang/crates.io-index 1.0.21
```

`cargo tree -i serde_core` shows `serde_core` is pulled by `serde` and `serde_json`.
`cargo tree -i zmij` shows `zmij` is pulled by `serde_json`.

CI installs and runs `cargo audit` so lockfile vulnerability checks are part of the normal gate once the workflow is active.
