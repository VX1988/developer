---
title: Rust Tooling
type: docs
prev: docs/rust/
weight: 2
---

Using `rustfmt` and `Clippy` can boost productivity and improve code quality.

VS (Visual Studio) Code, rust-analyzer installed using CLI:

`code--install-extension rust-lang.rust-analyzer`

- https://rust-analyzer.github.io/manual.html -> full list of magic completions and other features of rust-analyzer

enables verbose mode and check mode:

`cargo fmt—--check -v`

Installing rustfmt & Run

```
rustup component add rustfmt
cargo fmt
```

Configuring rustfmt. adding a `.rustfmt.toml` configuration file to your project’s source tree

```toml
format_code_in_doc_comments = true 
group_imports = "StdExternalCrate" 
imports_granularity = "Module" 
unstable_features = true 
version = "Two" 
wrap_comments = true
```

- https://rust-lang.github.io/rustfmt/?version=v1.6.0&search= -> Configuring Rustfmt

Installing Clippy & Run

```bash
rustup component add clippy
cargo clippy
```

fix the code automatically, run Clippy with the `--fix` flag

`cargo clippy --fix -Z unstable-options`

Note that we pass the `-Z unstable-options` option as well because at the time of writing, the `--fix` feature is nightly only.

## Examining dependencies with cargo-tree

cargo-tree allows you to visualize project dependency trees.

```bash
cargo install cargo-tree
# Prints help
cargo help tree 
cargo tree
```

## cargo-watch

cargo-watch automates rerunning Cargo commands on code changes.

continuously watches your project’s source tree for changes and executes a command when the there’s a change.

```bash
cargo install cargo-watch
# Prints help
cargo help watch
# Runs cargo check continuously
cargo watch
# Continuously rebuilds documentation on changes.
cargo watch -x doc 
```
## Testing libFuzzer

Finding unexpected bugs, support based on LLVM’s libFuzzer. cargo-fuzz let’s you easily integrate with libFuzzer for fuzz testing.

- https://llvm.org/docs/LibFuzzer.html

```bash
cargo install cargo-fuzz
# Prints help
cargo help fuzz
# Creates a new fuzz test called myfuzztest
cargo fuzz new myfuzztest
# Runs the newly created test, which may take a long time
cargo fuzz run myfuzztest
```

## Debugging macros with cargo-expand

cargo-expand lets you expand macros to see the resulting code.

```bash
cargo install cargo-expand
# Prints help
cargo help expand
# Shows the expanded form of "outermod::innermod"
cargo expand outermod::innermod
```

## Reducing compile times with sccache

installing sccache and using it locally can save you
a lot of time recompiling code.

```bash
cargo install sccache
# The which sccache command returns the path of sccache, assuming it’s available in $PATH.
export RUSTC_WRAPPER=`which sccache` 
cargo build
```

## Integration with IDEs, including Visual Studio Code

```bash
rustup component add rust-src
# Install the VS Code extension from the command line
code --install-extension matklad.rust-analyzer
(optional) code .
```

## Nightly-only features

There are cases when you may want to use nightly-only features in published crates. When doing so, you should place these features behind a feature flag to support stable users. 

## Keeping packages up to date date with cargo-update

`cargo-update` makes it easy to update your Cargo packages.

Packages installed with Cargo may need to be updated occasionally(sometimes but not often).

```bash
cargo install cargo-update
# Print help
cargo help install-update
# Updates all installed packages.
cargo install-update -a
```
