# CLAUDE.md

## What This Is

A single-file Ruby CLI tool (`bin/issue-md`) distributed via Homebrew (`modulotech/tap`) that exports a GitLab issue as clean Markdown. Takes an issue URL, fetches the issue via the GitLab API, and outputs the title, description, all non-system comments, image references, and related issues as a Markdown document.

## Running

```bash
# Print markdown to stdout
./bin/issue-md https://gitlab.example.com/group/project/-/issues/123

# Write to file
./bin/issue-md -o issue.md https://gitlab.example.com/group/project/-/issues/123

# Download images locally and rewrite references
./bin/issue-md -d ./images https://gitlab.example.com/group/project/-/issues/123

# Override token
./bin/issue-md -t glpat-xxxx https://gitlab.example.com/group/project/-/issues/123
```

Dependencies are installed automatically via `bundler/inline`.

## Configuration

Settings resolved in 4 layers (highest priority wins):

1. **Defaults** — none required
2. **Config file** — `~/.issue-md/config.yml`
3. **Environment variables** — `GITLAB_API_TOKEN`
4. **CLI flags** — `-t`

### Config file format

```yaml
gitlab_api_token: glpat-xxxxxxxxxxxxxxxxxxxx
```

## Architecture

Single-file CLI with these internal modules:

- **Config** — 4-layer configuration loading
- **UrlParser** — extracts `base_url`, `project_path`, `issue_iid` from a GitLab issue URL
- **ImageDownloader** — downloads GitLab `/uploads/` images, rewrites markdown references
- **IssueFormatter** — formats issue header, comments, and related links as markdown
