# Action Wrapper

GitHub Action metadata lives at the repository root so users can install Review Gate with:

```yaml
- uses: LVTD-LLC/review-gate@v0
```

Implementation scripts and release download helpers can live in this directory as the wrapper grows.

The composite action stays thin: it should collect inputs from GitHub Actions, pass them to the Rust binary, and let the Rust crates own review logic, scoring, OpenRouter request construction, and GitHub summary publishing.

Required installation permissions:

```yaml
permissions:
  contents: read
  pull-requests: write
  checks: write
```

Required secret:

```yaml
OPENROUTER_API_KEY
```

The action must update the existing PR summary comment containing `<!-- review-gate-summary -->` instead of creating duplicate summary comments on every commit.
