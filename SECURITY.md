# Security policy

## Reporting a problem

Please report security problems privately, never in a public issue, discussion or pull
request.

Use GitHub's private vulnerability reporting: open the repository of the affected app, go
to the **Security** tab and choose **Report a vulnerability**. Only the maintainers can see
the report.

Please include:

- which app and version (Help > About, or the command line's `--version`),
- your operating system,
- what you found and how to reproduce it, ideally with an invented file that triggers it
  (never a real budget, schedule or script).

We aim to acknowledge a report within a week, agree a fix and a disclosure date with you,
and credit you in the release notes if you would like.

## Supported versions

The apps are in early development. Fixes ship in the next release, and only the latest
release (or the `main` branch, for apps without releases yet) is supported.

## Scope

The apps are local desktop programs: your files stay on your disk, and there is no server
or account. Problems we especially want to hear about:

- a file (project, budget, schedule, script or import) that crashes an app, hangs it, or
  makes it run code or touch files it should not,
- anything that sends data off your computer without you asking,
- a way to get an unsigned or tampered update installed,
- the command line, MCP server or control channel reaching outside the folders or address
  it was given.

Each app's own `SECURITY.md`, where there is one, describes its network use and security
model in detail.
