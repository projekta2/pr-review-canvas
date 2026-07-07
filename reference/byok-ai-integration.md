# BYOK AI Integration Review (bring-your-own-key)

Used by the `pr-review-canvas` skill for category 5 (Performance & security) when a diff touches API key storage, a provider adapter, or settings/options page for AI providers (OpenAI, Anthropic, Gemini, Groq, Ollama, etc.).

## API key handling

- [ ] Is the API key stored in `chrome.storage.local` or `chrome.storage.session`? Session is more appropriate for sensitive keys that should clear on browser restart. If using `local`, is there a reason the key needs to persist across browser restarts?
- [ ] Is the key ever logged to the console, included in error messages, or exposed in any way that would leak it in a bug report or screen-share? This should be a blocking finding.
- [ ] Is the key passed via HTTPS requests only, or is there any plaintext transmission? Flag any HTTP endpoint for key transmission as blocking.

## Provider abstraction

- [ ] Does the PR add a new AI provider (e.g., a new endpoint in `endpoints` object)? Check that the provider's API shape is normalized correctly — the skill expects OpenAI-compatible chat completion shape to be the common denominator.
- [ ] Are provider-specific headers (e.g., `x-api-key` for Anthropic, `Authorization: Bearer` for OpenAI) isolated in the provider's own `buildHeaders` method rather than conditional branches in the main `callProvider` function?
- [ ] Does the PR add streaming support? If so, does it handle service worker termination mid-stream (MV3) gracefully? This is a common failure point.

## Fallback and error handling

- [ ] If the user's key is invalid (401), does the error message guide them toward checking the key in their provider dashboard instead of showing a generic "API error"?
- [ ] If the provider is rate-limited (429), does the extension surface an actionable message (e.g., "Rate limit hit — wait a moment or switch providers in Settings") rather than failing silently?
- [ ] If the provider is unreachable, does the extension fall back to a cached response or show a clear error? The skill expects a pattern where providers can be disabled gracefully.

## Security of the key entry UX

- [ ] Is the API key input field type `password` (or equivalent) so the key is not visible on screen as the user types? This is a UX safeguard, not a security boundary, but it's a signal of good hygiene.
- [ ] Is the key validated with a test API call before being stored, so the user knows it works before they click "Save"?
