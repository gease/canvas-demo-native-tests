# canvas-demo native tests

Tests the `canvas-demo` site builds from
[canvas-storybook-ai](https://gitlab.com/freelygive/canvas-storybook-ai) on
macOS and Windows, which its GitLab CI cannot run. That CI packs the macOS and
Windows executables on Linux; this repository runs them on GitHub's free
runners.

`.github/workflows/test.yml` has two jobs:

- **conformance**: drupack's conformance suite on `canvas-demo-macos-arm64`
  (`macos-15`), `canvas-demo-macos-amd64` (`macos-15-intel`) and
  `canvas-demo-windows-amd64.exe` (`windows-2025`), after checking each file
  against the build's `checksums.txt`.
- **install**: the `drupal-demo-install` skill end to end on Ubuntu, both
  macOS runners and Windows (in Git Bash, plus its checks from PowerShell
  through Git's `bash.exe`), then its status checks from a new shell, a
  Storybook restart, the hand-over report and a stop.

It runs on every push to `main`, and by hand (Actions → Test canvas-demo
builds → Run workflow) with three optional inputs: the build's artifact folder
(`SITE_BUILD_URL`), the skill's branch, and the drupack tag the build used.
Failed jobs upload their logs as artifacts.

Nothing is published from here, and the repository holds no copy of the site
or the skill: both are downloaded at run time.
