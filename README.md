# Echophrase Scoop Bucket

A [Scoop](https://scoop.sh) bucket for [Echophrase](https://echophrase.com) - a
privacy-first, GPU-accelerated speech-to-text desktop app that transcribes
locally on your machine.

## Install

```powershell
scoop bucket add echophrase https://github.com/imperium42/scoop-bucket
scoop install echophrase
```

## Update

```powershell
scoop update echophrase
```

Echophrase's built-in updater is disabled for Scoop installs, so it will not
fight Scoop's version tracking. The app detects the Scoop install and points you
at `scoop update echophrase` instead of updating itself.

## Notes

- Windows x64 only. The installer is an Authenticode-signed NSIS package,
  published to
  [imperium42/echophrase-releases](https://github.com/imperium42/echophrase-releases).
- The manifest runs the real installer silently rather than extracting it,
  because Echophrase registers the `echophrase://` deep-link scheme that sign-in
  callbacks depend on. A plain extract would break signing in.
- Your settings (`%APPDATA%\com.imperium42.echophrase`) and downloaded speech
  models (`~\.cache\huggingface\hub`) live outside the Scoop prefix, so they
  survive uninstall. Remove them by hand for a completely clean removal.
- The install directory cannot contain a space (an NSIS `/D=` limitation); the
  manifest fails early with a clear message if it does.

Echophrase is also on [winget](https://github.com/microsoft/winget-pkgs)
(`winget install Imperium42.Echophrase`) and Homebrew
(`brew install --cask imperium42/tap/echophrase`).

## Maintenance

`bucket/echophrase.json` is kept current by the scheduled
[excavator workflow](.github/workflows/excavator.yml), which runs Scoop's own
`checkver`/autoupdate against
[imperium42/echophrase-releases](https://github.com/imperium42/echophrase-releases)
and commits the new version and hash automatically.
