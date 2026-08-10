# homebrew-choreographr

Homebrew tap for [Choreographr](https://github.com/choreographr/choreographr) — the agentic coding assistant.

This tap ships the **prebuilt-tarball** variant of the formula: no build
toolchain required. The binaries are downloaded directly from the
`choreographr/choreographr` GitHub release.

## Install

```bash
brew tap choreographr/choreographr
brew install choreographr
```

The formula installs four binaries: `choreographr`, `choreo-tui`,
`choreo-im`, `choreo-acp`.

## Service

The formula registers a launchd service (never auto-enabled):

```bash
brew services start choreographr   # opt in explicitly
```

## Releasing a new version

1. Wait for the `vX.Y.Z` GitHub release on `choreographr/choreographr` to exist.
2. Edit `Formula/choreographr.rb`:
   - bump `version` to `X.Y.Z`,
   - update both `url` lines — tag, filename, and embedded version,
   - recompute each digest: `curl -fL -O <url> && shasum -a 256 <downloaded>.tar.gz`
     and paste into the matching `sha256` field,
   - sanity-check: `brew install ./choreographr.rb && choreographr --version`.
3. Commit and push to **this** repo (the tap), not the main repo.

The canonical bump procedure lives in the main repo's `RELEASE.md`
(Phase 5) — keep this formula in lockstep with `scripts/release.sh` and
`packaging/aur/PKGBUILD`.

## Layout

```
Formula/choreographr.rb   # the formula (mirrors packaging/homebrew/choreographr.rb in the main repo)
```

## Rollback

Revert the last tap commit and push — Homebrew will pick up the old formula
on the next `brew update`.
