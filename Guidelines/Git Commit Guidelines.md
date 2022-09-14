### Git commit guidelines

This project follows [conventional-commits](https://conventionalcommits.org) for commiting code. Specifically, we follow a slight variation on the [Angular commit conventions](https://github.com/angular/angular.js/blob/31fb6fa6db826d90b9268997b5d1e3b8b0ae010a/DEVELOPERS.md#commits), so read that and become familiar. This enables us to automatically generate CHANGELOGs for each package, and calculate semver.

We use `yarn commit` instead of `git commit`. This uses the [`commitizen-cli`](https://github.com/commitizen/cz-cli) with a custom adaptor to assist in writing the commit according to the correct structure.

The commit message structure is:

```
type(scope): summary

description

breaking
```

i.e.

```
fix(survey): update api endpoint for survey submit

```

Any line of the commit message cannot be longer 100 characters! This allows the message to be easier
to read on GitHub as well as in various git tools.

### Type

Must be one of the following:

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  semi-colons, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing or correcting existing tests
- **chore**: Changes to the build process or auxiliary tools and libraries such as documentation
  generation

#### Commit Summary Wording

When writing your commit summary:

- Explain why, not how.
  - Bad: "use overflow-wrap and word-break"
  - Good: "prevent long URLs from overflowing"
- Write in the [imperative case](https://chris.beams.io/posts/git-commit/#imperative).

If in doubt, try and complete the following sentence:

> If applied, this commit will...

i.e.

- **Bad (how, not why):** If applied, this commit will _use overflow-wrap and word-break_.
- **Bad (not imperitive):** If applied, this commit will _fix a bug causing long URLs to overflow_.
- **Good:** If applied, this commit will _prevent long URLs from overflowing_.
