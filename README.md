# cron

Parses cron expressions, computes their next times in a time zone, and runs loops and functions on a schedule with coroutines.

```lus nocheck
local cron = require("https://atmosp.here/2.0/cron.lus")

print(cron.next("0 9 * * mon-fri", time.now(), "Europe/Paris"):iso())

-- A loop that sleeps until each match.
for at in cron.ticks("0 * * * *", { limit = 3 }) do
    print("on the hour", at:iso())
end

-- The same loop in a detached coroutine, which is the handle of the schedule.
local cleanup = cron.schedule("*/5 * * * *", function(at)
    print("cleanup at", at:iso())
end, { zone = "America/New_York" })
coroutine.close(cleanup)
```

The package requires Lus 2.0. It needs `network:udp` for the timer of `cron.ticks` and `cron.schedule`, which waits on the receive timeout of an unbound UDP socket. `cron.parse` and `cron.next` need no permissions. It calls no `pledge` of its own, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `cron.lus`. Run `lus doc cron.lus` to print it.
