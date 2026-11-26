# Changelog

## 1.0.0

**Release date:** TBD

Version 1.0.0 is the first release of `cron`, which runs on Lus 2.0.

- Added the `cron` package.
  - `cron.parse`: Parses a cron expression of five or six fields, or a nickname such as `@daily`.
  - `cron.next`: Returns the first time after a given time that an expression matches, in a time zone.
  - `cron.ticks`: Returns an iterator that sleeps until each match of an expression.
  - `cron.schedule`: Runs a function at every match of an expression in a detached coroutine and returns that coroutine.
  - `cron.iserror`: Returns true for an error object that `cron.parse` raised.
