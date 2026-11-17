# opencode-plugins

A trimmed copy of [rizal72/opencode-plugins](https://github.com/rizal72/opencode-plugins), keeping the four
plugins I actually run. Upstream is MIT; this repository keeps the same license and the original copyright.

| plugin | what it does | TUI | GUI | npm |
|---|---|---|---|---|
| [`oc-budget`](plugins/oc-budget/README.md) | how much credit is left on the account behind the model: sidebar, footer, `/budget` | sidebar, footer, `/budget` | header widget | `@rizal72/oc-budget` |
| [`oc-donsetch`](plugins/oc-donsetch/README.md) | keeps the `donsetch` binary current, once a day | none | none | not published |
| [`oc-notify`](plugins/oc-notify/README.md) | a push notification on the phone when a turn ends, through ntfy | none | settings page | `@rizal72/oc-notify` |
| [`oc-session-search`](plugins/oc-session-search/README.md) | `session_search`: keyword search over past session transcripts | none | none | `@rizal72/oc-session-search` |

The other plugins upstream (models-pro, plugin-updates, git, coffee, ponytail-widget, tps-meter, context) are
not copied here.

## Install

Three of the four are published on npm and install normally, which also keeps `opencode plugin check/update`
working:

```sh
opencode plugin add @rizal72/oc-budget
opencode plugin add @rizal72/oc-notify
opencode plugin add @rizal72/oc-session-search
```

`oc-donsetch` is not on npm, so it loads from this checkout by path — one entry in
`~/.config/opencode/opencode.jsonc`, adjusted to wherever the clone lives:

```jsonc
"plugins": [
  "@rizal72/oc-budget",
  "@rizal72/oc-notify",
  "@rizal72/oc-session-search",
  "C:/Users/MW/opencode-plugins/plugins/oc-donsetch"
]
```

It also needs the binary it maintains, which is a separate install:

```sh
npm i -g donsetch
```

`oc-notify` needs an ntfy topic in `~/.config/opencode/oc-notify.json`; see its README. `oc-budget` reads the
credentials already stored by `opencode auth login` and needs no configuration of its own.

## Layout

Each directory under `plugins/` is the upstream plugin, unmodified: source, `README.md`, `package.json`.
No build step is needed for the server parts. The GUI parts (`gui.tsx`) ship prebuilt in the npm packages;
a copy loaded by path would need `scripts/build-gui.mjs` from upstream, which is not included here.

## Updating

```sh
git -C C:/Users/MW/opencode-plugins pull     # oc-donsetch follows the checkout, nothing else to do
opencode plugin update                       # the three npm packages
```

Upstream: https://github.com/rizal72/opencode-plugins — issues and fixes belong there.
