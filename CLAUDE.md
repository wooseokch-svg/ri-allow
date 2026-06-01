# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not** a software project — there is no build system, test suite, or
application source. The entire repository is a single remotely-fetched
configuration file, `allow.json`, that acts as a **remote kill switch and
allowlist** for the client `RealtimeInterpreter.exe`.

At startup, `RealtimeInterpreter.exe` fetches this `allow.json` (over GitHub's
raw CDN) and decides whether it is permitted to run. Editing and committing
`allow.json` is therefore the *only* meaningful "development" action in this
repo, and committing a change is effectively a production deploy.

## allow.json semantics

```json
{
  "enabled": true,
  "allowed": []
}
```

- `enabled: false` → **kill switch.** Every copy of the client stops immediately, on all machines.
- `enabled: true` + `allowed: []` (empty) → control by `enabled` only; **all PCs are allowed**.
- `enabled: true` + `allowed: ["<machineID>", ...]` → **only the listed PCs are allowed.** All others stop.

A machine's ID is obtained by running `RealtimeInterpreter.exe id` on that machine.

## Operational behavior (critical to understand before editing)

- **Propagation delay:** changes take effect within ~5 minutes after commit,
  due to GitHub CDN caching. Do not expect instant effect.
- **Offline grace period:** if a client loses internet access, it continues
  running on its last-known state for 24 hours.
- Because of the above, treat every commit to `allow.json` as a live change
  affecting real machines. Keep the JSON valid (it must parse) — a malformed
  file could break the client's ability to read its permission state.

## Conventions

- The README is written in Korean; mirror that language in `README.md` if you
  update it. Commit messages in history are also Korean — match the existing style.
- There is no CI, linting, or test command. The only validation that matters is
  that `allow.json` remains well-formed JSON and that `enabled`/`allowed`
  reflect the intended access policy.
