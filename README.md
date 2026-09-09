# tibo-time-monitor

Public status board for **Tibo Time** — the Codex / ChatGPT Work special case of Reset Rush.

Live page: https://ryanjosephkamp.github.io/tibo-time-monitor/

## What this is

An hourly Grok automation reads public posts from [@thsottiaux](https://x.com/thsottiaux), classifies whether an automatic usage reset was announced or reported landed, and publishes static files here.

This page cannot see your account. `ACTIVE` means Tibo posted a credible automatic reset that appears still pending. It does not mean your bar refilled.

## Public files

| File | Use |
|---|---|
| [status.json](./status.json) | Canonical machine state for embeds |
| [feed.xml](./feed.xml) | RSS of state-changing events only |
| [events.json](./events.json) | Recent event log |
| [index.html](./index.html) | Human status page |

Heartbeat (`last_checked_at`) updates every run. RSS items are added only when the public state or current event changes.

## Banner rules

| `tibo_time` | Meaning |
|---|---|
| `ACTIVE` | Credible applicable automatic reset announced and not clearly landed |
| `INACTIVE` | No such window, or only a banked credit / tease / commentary |
| `UNCERTAIN` | Landing was reported or the promised time passed, without account proof |

Banked-only grants stay `INACTIVE`.

## Embed on another page

```html
<script>
fetch("https://ryanjosephkamp.github.io/tibo-time-monitor/status.json?" + Date.now())
  .then((r) => r.json())
  .then((s) => {
    document.getElementById("tibo-banner").textContent =
      s.tibo_time === "ACTIVE" ? "Tibo Time is on" : "Tibo Time is off";
  });
</script>
```

Or subscribe to `https://ryanjosephkamp.github.io/tibo-time-monitor/feed.xml`.
