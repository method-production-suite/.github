# Method Production Suite

Free, open-source desktop apps for film and TV production, written in Rust. Each app keeps
your work as plain, documented files on your own disk, works offline and never needs an
account.

[methodproduction.com](https://methodproduction.com)

| App | What it does | Status |
|---|---|---|
| [Method Storyteller](https://github.com/method-production-suite/method-storyteller) | Screenwriting: Fountain, Final Draft `.fdx` import and export, industry pagination, PDF | Early (MVP), build from source |
| [Method Budget](https://github.com/method-production-suite/method-budget) | Production budgeting: topsheet, fringes, globals, versions, cost reports | In development, build from source ([methodbudget.com](https://methodbudget.com)) |

More apps are on the way.

## How the apps fit together

The apps talk through open files, not a shared server or account:

- **Script.** Method Storyteller writes Fountain (plain text) and `.fdx`, the formats
  scheduling and breakdown tools read.
- **Budget.** Method Budget keeps budgets as `.mthd` files, plain JSON with a published
  specification, and is planned to read shoot-day counts from a schedule's export to drive
  its globals.
- **Your tools.** Every app has a command line and an MCP server or control channel, so
  scripts and coding agents can use the same engine as the app.

Each file format is documented in its app's repository, so any tool can read or write it.

## Shared rules

- **Never crash, never lose work.** Hostile files are data, not a reason to fall over.
  Autosave, recovery copies and atomic saves come first.
- **Everything is a command.** Menus, shortcuts, the command line and agents all run the
  same named commands.
- **Clean room.** The apps are independent work. They use no other vendor's code, help
  text, icons, templates or data, and read other tools' work only through the open files
  those tools export. They are not affiliated with or endorsed by Final Draft,
  Entertainment Partners or Movie Magic; trademarks belong to their owners.

The apps follow the conventions of the [storytold Craft](https://github.com/storytold)
suite.

## Licence

The apps are dual-licensed under MIT or Apache-2.0, at your option. Contributions are
accepted under the same terms.

## Get involved

Bug reports and patches are welcome: read [CONTRIBUTING.md](https://github.com/method-production-suite/.github/blob/main/CONTRIBUTING.md)
and the clean-room rules of the repository you are working in. Please never attach a real
budget, schedule or unreleased script to an issue; an invented one that shows the problem
is always enough. Security problems go through private reporting
([SECURITY.md](https://github.com/method-production-suite/.github/blob/main/SECURITY.md)).
