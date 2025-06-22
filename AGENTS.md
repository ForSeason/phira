# Guidelines for Working on This Repository

This repository is a Rust workspace containing several crates that together make up the Phira rhythm game and related tools. The crates include:

- **prpr** – the core game engine and utilities.
- **prpr-avc** – audio/video support layer.
- **prpr-pbc** – a chart pack converter tool.
- **prpr-l10n** – localization utilities and language files.
- **phira** – the main game library.
- **phira-main** – minimal crate that links to `phira` for building the game executable.
- **phira-monitor** – a monitoring tool that connects to the multiplayer server.

## Building

Use the workspace `Cargo.toml` to build individual crates or the whole project.

- Build the game for desktop:
  ```bash
  cargo build --release -p phira-main
  ```
- Build the monitor tool:
  ```bash
  cargo build --release -p phira-monitor
  ```
- Build for WebAssembly (produces files in `dist/`):
  ```bash
  ./build_wasm.sh
  ```

The project expects the Rust toolchain `nightly-2023-02-01`. When setting up a fresh environment, install required system libraries as done in the CI workflow:

```
sudo apt-get update
sudo apt-get install librust-alsa-sys-dev libglib2.0-dev libasound2t64 libatk-adaptor \
    libgail-common libgtk-3-dev
```

## Testing

Run tests before submitting changes. The same commands are used in CI:

```bash
cargo test -p phira --no-default-features -- --skip test_parse_chart
cargo test -p prpr --no-default-features
cargo test -p prpr-l10n
```

## Code Style

Format all code using `rustfmt` with the workspace configuration:

```bash
cargo fmt --all --config-path=rustfmt.toml
```

The configuration sets a maximum line width of 150 and excludes several generated `inner.rs` modules from formatting.

## Pull Requests

- Keep pull requests focused and clearly describe the changes.
- Ensure code compiles and all tests pass.
- Use meaningful commit messages.

