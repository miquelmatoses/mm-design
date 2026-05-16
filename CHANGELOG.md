# Changelog

All notable changes to mm-design are documented here. The format
is based on Keep a Changelog (https://keepachangelog.com), and
this project adheres to Semantic Versioning (https://semver.org).

Until v1.0.0, breaking changes may occur in minor versions per
semver pre-release conventions.

## [0.2.0] — 2026-05-16

### Breaking

- Remove the `@import url('https://fonts.googleapis.com/...')`
  from `tokens/typography.css`. Consumers must now provide the
  fonts themselves. See the "Font provisioning" section of the
  README for recommended approaches. Migration guidance is
  documented in the README.

- Remove the `googleFontsUrl` key from `tokens/typography.json`.
  No internal consumer reads this key; external consumers that
  did rely on it should switch to documented font-provisioning
  methods.

### Changed

- Demo HTML pages (`index.html` and `components/*/*.html`) now
  load Google Fonts directly via `<link>` tags, independent of
  `tokens/typography.css`. This change is local to the demos and
  does not affect consumers.

- README adds a "Font provisioning" section documenting both
  `@fontsource` (recommended) and Google Fonts CDN approaches.

## [0.1.0] — pre-release baseline

First tagged release. `tokens/typography.css` includes an
`@import` that auto-loads Playfair Display and Roboto from the
Google Fonts CDN. Consumers receive fonts automatically without
additional configuration.

Tagged retroactively at the commit immediately preceding the
v0.2.0 changes, so consumers wishing to keep the auto-loading
behavior can pin to `github:miquelmatoses/mm-design#v0.1.0`.
