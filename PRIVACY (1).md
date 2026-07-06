# Privacy Policy — TabCost Pro

_Last updated: 2026-07-06_

TabCost Pro is a Chrome extension built on a zero-backend philosophy. This page explains, plainly, what that means for your data.

## What TabCost does NOT do

- ❌ No data is ever sent to a TabCost server — there is no server.
- ❌ No analytics, no telemetry, no session recording.
- ❌ No account registration, ever.
- ❌ No selling, sharing, or monetizing of any user data — there is none to sell.

## What TabCost stores, and where

All data TabCost generates — your hourly rate, tab activity timestamps, daily and historical cost totals, and your settings — is stored exclusively in `chrome.storage.local`, a storage area that lives on your own device and is never transmitted anywhere. Uninstalling the extension deletes this data permanently; there is no copy anywhere else.

## The one external network call

TabCost Pro makes exactly one external request: verifying a Pro license key against Gumroad's licensing API when you activate or periodically re-check a license. This call sends only the license key itself, nothing about your browsing activity, tab titles, or usage. If you never purchase Pro, this call never happens.

## Permissions

TabCost requests only the Chrome extension permissions needed to read tab state (title, activity, focus) and store data locally. It does not request host permissions to read the content of the pages you visit.

## Children's privacy

TabCost Pro is not directed at children and does not knowingly collect data from anyone, of any age, since it collects no data in the first place.

## Changes to this policy

If this policy changes, the "Last updated" date above will change and the update will be noted in [`CHANGELOG.md`](CHANGELOG.md) if it's material.

## Contact

Questions about this policy: [hello@projekta2.com](mailto:hello@projekta2.com)
