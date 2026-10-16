# Release checklist for every Method app

Each app's releasing doc links this file and adds its own commands. Tick every line, in
order, for every release. Nothing is published until a person has checked the draft.

## Before the tag

- [ ] **Version bumped** in one place, and the app's version check passes.
- [ ] **Every check green** on the release commit: format, lint, tests, cargo-deny, the
      14-day crate-age check, and the app's own release checks.
- [ ] **Pictures retaken** with the app's capture command, from the invented Field Station
      material only. Old and new compared side by side; every picture matches the build
      being released (no stale screens, nothing real).
- [ ] **Release notes written** from the template: what's new in plain words, then fixes,
      then known gaps. At least one picture or short clip for any visible change. No em
      dashes, no hype, no other vendors' product names.
- [ ] **Helpers named**: everyone who contributed, film knowledge included.
- [ ] **README updated**: the platform status table and anything the release changes.

## The release

- [ ] **Tag** `vX.Y.Z` on the release commit. The workflow builds a DRAFT release.
- [ ] **A person checks the draft**: installs the macOS `.dmg` on an Apple silicon Mac
      (signed, notarized, opens without a warning), opens the sample file, and checks the
      update archive and `latest.json` are attached and signed.
- [ ] **Installer names are version-free** (`Method-<App>-macOS.dmg` and so on), so the
      website's and README's download links keep working.
- [ ] **Publish** the draft.

## After publishing

- [ ] **Update check works**: an installed older version finds and installs this one.
- [ ] **Website synced**: ask MOrg (or run `tools/sync.py <app>` in the website repo and
      open a pull request) for the app's page, and to change its `status` and `platforms`
      in `apps.toml` if they moved.
- [ ] **Downloads checked live** on the app's site: every link reaches a file.
- [ ] **Announced** where the app's contributors are: GitHub Discussions, and the release
      notes linked from wherever the release was asked for.
