What are the [Octokit](https://github.com/octokit) and [Terraform](https://github.com/integrations/terraform-provider-github) conventions around
Pull Requests and Issues?

Since we have many repos across many languages we favor using informal (and in some cases [more formal](https://github.com/octokit/octokit.js/blob/main/MAINTAINING.md)) standards when it comes to communicating on Issues and PRs.
We generally like to follow the [conventional commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#specification) specification when no other approach has been specified in the repository itself.

By following these guidelines we can improve communication, improve understanding, promote consistent workflows, help automation, and enhance our release notes.

### So what does all of this look like?

All of the Octokit.js libraries use [semantic-release](https://github.com/semantic-release/semantic-release) so those approaches should remain unchanged but here's a quick review of how all of that works:

1. `fix:` ... or `fix(scope name):` ... prefix in subject: bumps fix version, e.g. `1.2.3` → `1.2.4`
2. `feat:` ... or `feat(scope name):` ... prefix in subject: bumps feature version, e.g. `1.2.3` → `1.3.0`
3. `BREAKING CHANGE:` in **body** and in the **title** bumps breaking version, e.g. `1.2.3` → `2.0.0`

Given that the following should be used when crafting issues and pull requests...

#### ISSUES prefixes
- `bug:` The title of the **bug** issue (i.e. "bug: This thing is broken")
- `docs:` The title of the **docs** issue (i.e. "docs: This thing is wrong in the docs")
- `deps:` The title of the **dependency** issue  (i.e. "deps: Updating from this to this") - this one will be rare, given automation.
- `feat:` The title of the **feature** issue  (i.e. "feat: This is a new thing")

#### PR prefixes
- `fix:` The title of the **fix** pull request (i.e. "fix: This is the fixed thing")
- `docs:` The title of the **docs** pull request (i.e. "docs: Adds this thing to the docs")
- `deps:` The title of the **dependency** pull request (i.e. "deps:  Updating from this to this")
- `feat:` The title of the **feature** pull request (i.e. "feat: Adds this new thing")
- `BREAKING CHANGE:` Title & body of the pull request (i.e. "BREAKING CHANGE: This thing will break old things")
