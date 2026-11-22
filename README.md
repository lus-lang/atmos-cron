# cron

`cron` parses cron expressions, computes their next times in a time zone, and runs loops and functions on a schedule with coroutines.

The following example schedules the recurring jobs of an application in two time zones.

```lus nocheck
local cron = require("https://atmosp.here/2.0/cron.lus")

print(cron.next("0 9 * * mon-fri", time.now(), "Europe/Paris"):iso())

-- A loop that sleeps until each match.
for at in cron.ticks("0 * * * *", { limit = 3 }) do
    print("on the hour", at:iso())
end

-- The same loop in a detached coroutine, which `cron.schedule` returns as the handle of the schedule.
local cleanup = cron.schedule("*/5 * * * *", function(at)
    print("cleanup at", at:iso())
end, { zone = "America/New_York" })
coroutine.close(cleanup)
```

The package requires Lus 2.0 and declares the permission `network:udp`, which only the timer of `cron.ticks` and `cron.schedule` uses. It never calls `pledge`, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `cron.lus`, which `lus doc cron.lus` prints.
