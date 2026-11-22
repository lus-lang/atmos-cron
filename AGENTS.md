# AGENTS.md

`lus-lang/atmos-cron` is the repository of the `cron` package of the atmosphere registry. Programs load the package with `require("https://atmosp.here/2.0/cron.lus")`.

## Scope

`cron` parses cron expressions, computes their next times in a time zone, and runs loops and functions on a schedule with coroutines. The public API is every function that `cron.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `cron.lus` is the whole package. Its header doc comment contains the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load `cron.lus` from the parent of `TEST_DIR`, the directory that holds the test file.

## Commands

Run these commands from the root of the repository.

```sh
lus test tests          # run the tests
lus check cron.lus     # lint, including the package codes
lus doc cron.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose follows the `lus-writing` skill, which `lus agents init` installs and https://lus.dev/agents/skills/lus-writing/SKILL.md serves. In particular, prose has no dashes or semicolons and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
