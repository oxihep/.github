# Contributing to oxihep

Thanks for helping. oxihep is a personal project, kept by one person, so a
short issue before a large change saves us both time: it settles whether the
change fits and how before the code is written. Small fixes (a bug, a typo, a
missing case) can go straight to a pull request.

These notes apply to every repository of the organization: oxiroot, oxihist,
oxiplot, oxifit, oxistats and oxiparticle.

## Reporting a bug

Open an issue in the repository of the crate that misbehaves, with the
version (its git tag), what you ran, and what you expected. For a file that
reads or writes wrongly in oxiroot, say what ROOT or uproot does with the same
file, and attach the file, or a small one that shows the same problem, if you
can share it.

A security problem goes through [SECURITY.md](SECURITY.md) instead, not a
public issue.

## Making a change

1. Fork the repository and branch from `main`.
2. Build and test as its README's *Build & test* section says. Before you
   push, at least:
   ```sh
   cargo fmt --all --check
   cargo clippy --workspace --all-targets --all-features -- -D warnings
   cargo test --workspace --all-features
   ```
   Where the repository has a `.pre-commit-config.yaml`, `pre-commit install`
   runs these for you.
3. Add a test that fails without your change. In oxiroot, a change to how a
   file is read or written is checked against ROOT C++ and uproot (the
   `interop` examples and `scripts/interop_local.sh`); CI runs both.
4. Add a line to `CHANGELOG.md` under `[Unreleased]`, saying what changes for
   someone who uses the crate.
5. Open the pull request. CI must be green before it is merged; it is merged
   by squashing, so its title becomes the commit message.

Public items get doc comments. Docs and comments say what the code does and
why, in plain words.

## Releases

Releases are cut by the maintainer, in dependency order, as
[oxiroot's RELEASING.md](https://github.com/oxihep/oxiroot/blob/main/RELEASING.md)
describes. The crates are used from GitHub, pinned to release tags, and are
not on crates.io yet.

## License

By contributing, you agree that your contribution is licensed under the MIT
license of the repository you contribute to.
