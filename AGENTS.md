# AGENTS.md

Guidance for coding agents working in this repository.

## Project overview

This is a monorepo of TradingView indicators written in Pine Script. **Each top-level directory is one indicator.** The indicators are not published on TradingView (see "TradingView Hosting Notice" in `README.md`); users copy `mod.pine` into the Pine Editor themselves.

Current indicators:

| Directory | Title |
| --- | --- |
| `4h-sweep-close/` | Super Crooks - 4H Sweep/Close |
| `breakers/` | Super Crooks - Breakers |
| `daily-highs-lows/` | Super Crooks - Daily Highs/Lows |
| `htf-separators/` | Super Crooks - HTF Separators |
| `session-highs-lows/` | Super Crooks - Session Highs/Lows |

## Pine Script version

Always use the latest Pine Script version, currently **v6** (`//@version=6`). Never write v5 or older code, and if you touch a script still on an older version, migrate it.

Watch for v6 semantics that differ from v5:

- `bool` values can never be `na`; `na()`, `nz()` and `fixnan()` don't accept bools.
- `and` / `or` short-circuit (evaluate lazily).
- No implicit `int`/`float` → `bool` casting; write `x != 0` instead.
- Dividing two const `int`s can return a fractional result; wrap with `int()` / `math.floor()` when you need an integer.
- `request.*()` calls are dynamic by default (can be used in loops, conditionals and with series arguments).
- `timeframe.period` always includes a multiplier (e.g. `"1D"`, not `"D"`).

If unsure whether a built-in exists or how it behaves in v6, check the Pine Script v6 reference manual and release notes instead of relying on memory.

## Directory layout

```
<indicator-name>/      # kebab-case
├── mod.pine           # the entire script
└── README.md          # Overview, Concepts, How to Use, Features
```

- Each `mod.pine` must be self-contained and paste-able into the Pine Editor. Don't share code between directories (no imported libraries unless the user asks for one).
- One indicator per directory; don't put multiple scripts in one directory.

## Script template

New indicators start from this skeleton:

```pine
// This Pine Script® code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © crookse
// GitHub: https://github.com/crookse
// Website: https://supercrookstradingbros.com

//@version=6
indicator("Super Crooks - <Title>", overlay = true, max_labels_count = 500, max_lines_count = 500)

const string SCRIPT_VERSION = "1.0.0"

////////////////////////////////////////////////////////////////////////////////
// INPUTS
////////////////////////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////////////////////////
// HELPERS
////////////////////////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////////////////////////
// STATE
////////////////////////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////////////////////////
// LOGIC
////////////////////////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////////////////////////
// DRAWING
////////////////////////////////////////////////////////////////////////////////
```

- Every indicator title is prefixed with `Super Crooks - `.
- Add `max_boxes_count = 500` (or other limits) when the script draws those objects.
- Omit sections that end up empty.

## Coding conventions

- Match the style of the file you're editing. For new scripts, follow the majority convention: `snake_case` for variables (`input_history`, `is_new_day`), `camelCase` for functions (`getStyle`, `isUpClose`), and `UPPER_SNAKE_CASE` for `const` values. (`4h-sweep-close` uses `camelCase` variables; keep that file consistent with itself.)
- Prefix input variables with `input_` in new scripts, and give inputs a `group =` and a `tooltip =` when the meaning isn't obvious from the label.
- Use `var` for persistent state and drawing arrays (`var line[] high_lines = array.new_line()`).
- Stay under drawing limits: keep lines/labels/boxes in arrays and `delete` the oldest once a user-configurable history count is exceeded.
- Avoid repainting: base signals on confirmed bars (`barstate.isconfirmed`, or `[1]` offsets) and use `lookahead = barmerge.lookahead_off` with `request.security()` unless there's a deliberate reason not to.
- Guard history references so they can't index before the first bar (e.g. `bar_index - n >= 0`).
- Specify the timezone explicitly for session and time-of-day logic (existing scripts use `"GMT+0"` / `"UTC+0"`).
- Detect the chart timeframe with `timeframe.period` / `timeframe.in_seconds()`; document which timeframes a feature appears on in its tooltip.
- Indent with 4 spaces. Wrapped lines must be indented by a non-multiple of 4 spaces, or Pine treats them as a new block.

## Adding or changing an indicator

1. Create `<indicator-name>/mod.pine` from the template and a `README.md` with Overview, Concepts, How to Use and Features sections.
2. Add the title to the "Indicators" list in the root `README.md` and to the table above.
3. Don't bump `SCRIPT_VERSION` by hand; releasing sets it (see "Releases"). Instead, title the pull request so it resolves to the right version: `fix:` for fixes (patch), `feat:` for new features or inputs (minor), `feat!:` for breaking input changes (major).

## Releases

Each indicator is released on its own, tagged `<indicator-name>/<version>` (e.g. `4h-sweep-close/1.2.0`, no `v`).

1. On every push to `main`, `.github/workflows/release-drafter.yml` keeps one draft release per indicator that has changes since its last release. The draft lists only the merged pull requests that changed that directory, and works out the next version from their Conventional Commits titles: `feat!:` → major, `feat:` → minor, anything else → patch. An indicator's first release uses its current `SCRIPT_VERSION`.
2. Publish a draft on GitHub to release it. `.github/workflows/release-version.yml` then sets `SCRIPT_VERSION` in that indicator's `mod.pine` to the released version, adds the release notes to its `CHANGELOG.md` as `## [<version>] - <date>`, and pushes a `chore: bump <indicator-name> version` commit to `main`.

- Changelogs are written on release, so don't add entries by hand. If you do write one ahead of a release, head it `## [<version>] - Unreleased`; releasing that version fills in the date and keeps your text instead of the generated notes.

- New indicators are picked up automatically (any top-level directory with a `mod.pine`). `SCRIPT_VERSION` must be declared as `const string SCRIPT_VERSION = "x.y.z"` on one line.
- Shared release-note settings live in `.github/release-drafter.yml`.

## Verification

There is no local Pine compiler, so agents can't run scripts. Before handing work back:

- Re-read the script for compile errors: type mismatches, `na` used with bools, bad line-wrap indentation, undeclared variables, mutating a `var` with `=` instead of `:=`.
- Check drawing counts can't exceed the limits declared in `indicator()`.
- Tell the user to paste `mod.pine` into TradingView's Pine Editor, compile it, and add it to a chart on each timeframe the feature targets.

## Git

- Use Conventional Commits: `feat:`, `fix:`, `docs:`, `refactor:` (e.g. `feat: 4H sweep/close indicator`).
- Keep each commit to one indicator where possible.

## Disclaimer

Indicators are for educational purposes only (see `README.md`). Don't add language to scripts or docs that presents output as financial advice or trade recommendations.
