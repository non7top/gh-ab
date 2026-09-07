# gh-ab

A `gh` CLI extension: Actions/Packages/LFS budget report for a personal GitHub account.

GitHub's Free-plan quota (2,000 Actions minutes, 500MB Actions storage, etc.) only
applies to **private** repos — public repos get unlimited free Actions usage. This
tool splits your current billing-cycle usage into private (counts against quota) vs
public (always free), compares it to your account's included-usage dollar values,
and projects where you'll land by the end of the cycle.

## Install

```sh
gh extension install non7top/gh-ab
```

## Usage

```sh
gh ab
```

Prints a summary table plus colored budget bars (respects `NO_COLOR`).

## Notes

- Relies on `GET /users/{login}/settings/billing/usage?year=&month=` — calling it
  *without* year/month collapses results to one row per SKU per month and hides
  almost all your repos, so this always passes them explicitly.
- The included-usage dollar values (quota constants in the script) come from the
  account's own billing page (`github.com/settings/billing/usage`), since they
  aren't exposed by any API. Re-check there if your plan or GitHub's pricing changes.
- The projection is a naive linear extrapolation from day-of-cycle usage — a
  ceiling estimate, not a trend-aware forecast.
