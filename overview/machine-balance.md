New threads go to the machine with the most free CPU and memory, weighted by a
preference you set per machine. It is the rule T3 Code uses to balance threads
across machines.

## What you get

- Every new thread starts on the best machine for its project. The composer
  opens on bb's usual machine, then moves to the chosen one. A machine you
  pick by hand stays picked until you send the thread, and a draft that points
  at a folder on one machine stays on that machine.
- A **Machines** section in this plugin's settings with each machine's live
  load, its score, the machine chosen right now, and a preference: Prefer,
  Normal, Less often, or Manual only.
- A `bb balance` command and a bundled skill, so agents can spawn child threads
  on the least-busy machine: `bb balance pick --project <id>` prints the
  machine to pass to `bb thread spawn --machine`.

## How it works

Each connected machine samples its own CPU (two readings 200 ms apart) and
available memory, cached for five seconds. A machine scores preference weight ×
cores × idle CPU × free memory. It is skipped when it is offline, lacks a
source for the project, is set to Manual only, does not answer within three
seconds, has CPU at 95% or more, or has 5% or less memory free. When no
machine qualifies, the composer stays on bb's usual machine and a notice
names the reasons.

Preferences are stored in this plugin's storage on the bb server. Nothing
leaves your machines.

## Requirements

BB 0.50 or newer, and at least two connected machines to have an effect.
