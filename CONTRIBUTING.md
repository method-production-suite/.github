# Contributing to the Method Production Suite

Thanks for helping. Bug reports, small fixes and larger patches are all welcome. Each app
lives in its own repository; this file is the default for all of them, and a repository's
own README, `CLEAN-ROOM.md`, `AGENTS.md` or `CONTRIBUTING.md` wins where they differ.

## No code needed

Most of what these apps need is film knowledge, not code. If you make films, you can help
without writing a line:

- **Check the numbers.** Import an old budget or schedule (an invented one, or your own
  that you keep to yourself) and tell us where a figure, a fringe or a day count differs
  from what you expect.
- **Check your region.** Rates, fringes, holidays, currencies and union rules vary. Tell us
  what your region does that the apps get wrong or don't know yet.
- **Test on your devices.** Method Reader needs people with Kobo, tolino and reMarkable
  readers to try a book and report what they see.
- **Share how you work.** The report layouts, boards, call sheets and charts of accounts
  your productions use (as blank templates), so the apps match real practice.
- **Make samples.** Invented scripts, budgets and schedules for tests and tutorials.
- **Translate and explain.** Translations, plainer wording in the apps and guides for people
  doing the job for the first time.

Open an issue in the app's repository and say what you checked and what you found, or
start a conversation in
[GitHub Discussions](https://github.com/method-production-suite/.github/discussions). Every
release names the people who helped, film knowledge included.

## The one hard rule: clean room

The apps are independent, clean-room work. When you contribute:

- Never decompile, disassemble or debug another vendor's software, and never read the
  inside of its app bundle or its native project files.
- Never copy another vendor's code, help text, icons, templates, presets, fonts or bundled
  data (rate books, fringe libraries and the like).
- Never copy GPL, LGPL or AGPL code into the apps.
- Learning how film and TV production works, using other tools normally, and reading the
  open files they export for their users are all fine.

If you are not sure whether something is allowed, ask in an issue before you write the
code. The repository's `CLEAN-ROOM.md` has the full rules.

## Never attach real production material

Budgets, schedules, call sheets and unreleased scripts are confidential. Please never
attach a real one to an issue or a pull request. An invented file that shows the problem is
always enough, and most apps can make one for you (for example `method sample` in Method
Budget).

## Reporting a bug

Open an issue in the app's repository with the version, your operating system, what you
did, what you expected and what happened. If the app crashed, say so in the title: crashes
are fixed first.

Security problems are different: report them privately, as [SECURITY.md](SECURITY.md)
describes, never in a public issue.

## Sending a change

1. Open an issue first for anything bigger than a small fix, so we can agree on the shape
   before you spend time on it.
2. Fork the repository and make your change on a branch.
3. Run the repository's checks before you push. In the Rust apps that is usually
   `cargo xtask ci`, or `cargo fmt --check`, `cargo clippy --workspace --all-targets -- -D warnings`
   and `cargo test --workspace`. The README says which.
4. Open a pull request that says what changed and why, and links the issue.

### AI-assisted changes

AI-assisted changes are welcome on an accepted issue, with passing tests, from an author
who can explain every line. Say in the pull request if you used AI tools. The apps
themselves contain no generative AI, and changes that add it won't be accepted.

### What every change keeps

- **Never crash.** No `unwrap`, `expect`, `panic!` or `unsafe` in product code (tests may
  use them). Treat every number that comes from a file, a setting or the command line as
  hostile. A crash fix comes with a test that crashed before.
- **Never lose work.** Saves are atomic, and nothing a user typed is thrown away without
  asking.
- **Everything is a command.** New actions are named commands that the menus, shortcuts,
  command line and agents all reach the same way.
- **Open, documented files.** A change to a file format updates its specification in the
  same pull request.
- **Openly licensed assets only.** Every image, icon or font needs a licence that allows
  it and an attribution entry.

## Licence

Unless a repository says otherwise, the apps are dual-licensed under MIT or Apache-2.0, at
your option. By sending a contribution you agree that it is licensed under the same terms,
with no additional conditions (Apache-2.0, section 5).

## Conduct

Everyone taking part follows the [Code of Conduct](CODE_OF_CONDUCT.md).
