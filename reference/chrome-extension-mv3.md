# Chrome / browser extension review (Manifest V3)

Used by the `pr-review-canvas` skill for category 5 (Performance & security) when a diff touches `manifest.json`, `content_scripts`, a `background`/`service_worker` file, or extension permission requests. Most general-purpose code-review skills don't cover this surface at all — extensions have a distinct trust model (page ↔ content script ↔ service worker ↔ remote server) that generic web-app checklists don't map onto.

## Permissions

- [ ] Does every requested permission in `manifest.json` map to a feature actually used in this diff? Flag any permission added "for later" — Chrome Web Store review will flag it too, and it's a real attack-surface increase in the meantime.
- [ ] Is `host_permissions` scoped to the specific domains needed, rather than `<all_urls>`? A new `<all_urls>` entry is always a blocking finding unless the PR description gives a specific reason it's unavoidable.
- [ ] If `activeTab` would satisfy the need instead of a persistent host permission, flag it as a lower-privilege alternative.

## Content scripts and injected code

- [ ] Does the content script write untrusted page or API-response content into the DOM via `innerHTML`, `outerHTML`, or `document.write` instead of `textContent`? This is the same XSS-class risk as any web app, but here it runs with elevated extension privileges.
- [ ] Is any script loaded from a remote URL (`<script src="https://...">`, dynamic `import()` of a remote module, or fetching and `eval`-ing a payload)? **This is close to an automatic Chrome Web Store rejection** and a blocking finding regardless of intent — MV3 requires all executed code to be bundled in the package, not fetched at runtime.
- [ ] Does message passing between content script and background/service worker validate the message shape and sender (`chrome.runtime.onMessage`, checking `sender.id` / `sender.origin`) rather than trusting any message that arrives?

## Storage and data handling

- [ ] Is `chrome.storage.local` used for anything that should arguably be `chrome.storage.session` (cleared on browser close) — e.g., a short-lived token?
- [ ] Does anything written to storage get logged to the console in a way that would leak it in a shared bug report or screen-share?
- [ ] If this PR touches licensing/entitlement logic (e.g. a Gumroad or similar license check), does a failed or offline verification fail closed (features locked) or fail open (features unlocked)? Fail-open on license checks is a business-logic bug worth flagging even though it's not a security bug in the traditional sense.

## Service worker / background specifics (MV3)

- [ ] Does the service worker assume it stays alive between events? MV3 service workers are non-persistent — any in-memory state that isn't re-derived or re-read from `chrome.storage` on wake-up is a latent bug, not just a performance concern.
- [ ] Are `chrome.alarms` used for anything that needs to survive a service worker restart, rather than `setTimeout`/`setInterval` (which do not survive termination)?

## Store listing / manifest hygiene

- [ ] Does a version bump in `manifest.json` match an actual user-facing change, so the Chrome Web Store changelog stays meaningful?
- [ ] Do new permissions added in this PR have a corresponding one-line justification the author could paste into the Chrome Web Store permission justification field? If they can't articulate it in a sentence, that's a signal the permission is broader than needed.
