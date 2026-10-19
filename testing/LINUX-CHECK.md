# The Linux check: a hand-off for a Claude Code session

This is the whole brief for one Claude Code session on an Arch-based Linux machine (written
for Omarchy: Arch, Hyprland, Wayland). Paste this into the session, or clone this repository
and say "follow testing/LINUX-CHECK.md". The person at the machine does the steps that need
eyes and hands; the session does the rest and writes up the results.

The four apps are Method Budget, Method Schedule, Method Reader and Method Storyteller. Only
Mac builds have been checked by a person so far. This check covers Linux.

## Ground rules

- **Read-only on the code.** Clone, build and test; never push to any repository, never open
  a pull request, never tag. Results go into GitHub issues (step 6).
- **Nothing personal in public.** Issues are public: no names of people or companies, no
  file paths under a home folder, no screenshots showing other windows or personal files.
  Use the invented Field Station sample each app ships, never real scripts, budgets or
  schedules.
- **Ask before anything system-wide** beyond the packages in step 1 (no changes to the
  display server, the compositor, udev rules or other system settings).
- **Don't take over the screen without asking.** Before a step opens app windows, say so
  and wait for a yes; close what you opened afterwards.
- Plain words in the write-up: what you did, what you expected, what happened.

## 1. Set up the machine

```bash
sudo pacman -S --needed base-devel git curl wget file openssl gtk3 webkit2gtk-4.1 \
  libayatana-appindicator librsvg xdotool fuse2 udisks2 github-cli rustup
gh auth login        # the person signs in; read access is enough
```

`webkit2gtk-4.1` is for Budget and Schedule (their window is a web view); Reader and
Storyteller draw their own window. `fuse2` lets AppImages run. Each repository pins its own
Rust version in `rust-toolchain.toml`; Arch's `rustup` fetches it on the first build.

Record for the report: `uname -r`, `pacman -Q webkit2gtk-4.1 gtk3`, the compositor and its
version (`hyprctl version | head -1`), and whether the session is Wayland
(`echo $XDG_SESSION_TYPE`).

## 2. Build and test each app from source

```bash
mkdir -p ~/method && cd ~/method
for r in method-budget method-scheduling method-reader method-storyteller; do
  gh repo clone method-production-suite/$r
done
```

For each repository, read its `README.md` and `AGENTS.md` (or `CLAUDE.md`) for the exact
commands, then run its full checks. Usually that is `cargo xtask ci` where it exists,
otherwise `cargo fmt --check`, `cargo clippy --workspace --all-targets --locked -- -D
warnings` and `cargo test --workspace --locked`. Method Reader's workspace is in `rust/`.

Record per app: pass or fail, the failing test names and the first lines of each failure,
and how long the build and tests took.

## 3. Install the released Linux builds

Use the AppImage where there is one (Arch has no `.deb` or `.rpm` support out of the box):

| App | Release | Linux files |
|---|---|---|
| Method Budget | latest | `Method-Budget-linux-x86_64.AppImage` (and `.deb`) |
| Method Schedule | latest | `Method-Schedule-linux-x86_64.AppImage` (and `.deb`) |
| Method Reader | latest | `Method-Reader-linux-x86_64.AppImage` (and `.deb`, `.rpm`, command-line tool) |
| Method Storyteller | no release yet | build it: `cargo run --release` per its README |

```bash
gh release download -R method-production-suite/<repo> --pattern '*.AppImage' -D ~/method/releases
chmod +x ~/method/releases/*.AppImage
```

Check each file's SHA256 against the release's `SHA256SUMS` where one is attached.

## 4. The checks (the person does these, the session takes notes)

Open each app on the invented sample (`method-budget sample`, Schedule's and Storyteller's
Field Station sample, Reader's own test PDF from `tests/fixtures/`).

**Every app**
- It starts from the AppImage; the window draws correctly on Wayland, resizes, and follows
  the light and dark theme.
- Menus and keyboard shortcuts work with Ctrl (not Cmd); note any shortcut Hyprland grabs
  first.
- Open, edit, save, close, reopen: nothing lost. Saving is to a normal folder, not the
  AppImage's mount.
- Help menu: About, the user guide, Report a Bug and Licenses and Notices open. Check for
  Updates says updates are Mac-only for now, without an error.
- Text: fonts render cleanly, nothing clipped, high-DPI scaling looks right.

**Method Budget** (its roadmap item 2.25)
- Print the topsheet and the detail (to a PDF printer is fine).
- Menu keys: Alt+Up and Alt+Down, Ctrl+F, the setup keys.
- Double-click a `.mthd` to open it (file association), if the desktop offers one.
- The browser demo at methodbudget.com/try/ in the Linux browser.

**Method Schedule** (its M3 milestone)
- Printing and Save as PDF; the PDF's document properties.
- Pictures on elements in TIFF, HEIC and BMP: which show.
- Ctrl keys versus system keys; opening a second copy of the app (single instance).
- Double-click a schedule file to open it.

**Method Reader**
- Convert the test PDF to an e-book and preview it (the Preview tab).
- With an e-reader plugged in by USB (a Kindle or a Kobo), see whether the app finds it,
  copies the book and ejects it. Hyprland doesn't mount USB drives by itself: note whether
  the device had to be mounted by hand (`udisksctl mount -b /dev/sdX1`).
- The command-line tool: `method-reader <pdf>` and `method-reader --help`.

**Method Storyteller**
- Type a scene with Tab and Enter moving between elements; find and replace; Go To; rename
  a character.
- Save as Open Screenplay Format, Fountain and `.fdx`; reopen each.
- Export a PDF and check the page breaks look right.

## 5. What to watch for

Crashes and hangs (with the terminal output), anything that looks different from the Mac
pictures on each app's website, slow redraws, keys that do nothing, dialogs that open behind
the window, and anything confusing in the wording.

## 6. Report

One issue per app, in that app's repository, titled `Linux check: <date>, <distro>` with
the label `bug` only if something is broken. In it:

1. The machine line from step 1.
2. Source build and tests: pass or fail, with failures.
3. Each check from step 4 as a list: ✓ works, ✗ broken (what happened), or ? not tried.
4. Separate issues for anything serious, each linked from the summary.

```bash
gh issue create -R method-production-suite/<repo> --title "Linux check: <date>, Arch (Omarchy)" --body-file report-<app>.md
```

Then tell the person the four issue links. They pass them to MOrg, which routes each app's
findings to the session that owns it.
