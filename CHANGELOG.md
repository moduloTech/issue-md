# Changelog

## [Unreleased]

### Fixed

- Comments are now displayed in chronological order (oldest first) instead of reverse.

## [0.1.0] - 2026-04-10

### Added

- Initial release: fetch a GitLab issue as clean Markdown (title, description, comments, related issues).
- Support for both `/-/issues/` and `/-/work_items/` URLs (GitLab work items).
- URL fragments (`#note_...`) are ignored during parsing.
- Image download mode (`-d DIR`) to save GitLab-hosted images locally and rewrite references.
- Output to file (`-o FILE`) or stdout (default).
- 4-layer configuration: defaults, `~/.issue-md/config.yml`, environment variables, CLI flags.
