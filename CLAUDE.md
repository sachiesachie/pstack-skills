# Cloud session rules

These apply in every cloud session this environment starts.

## Worktrees

Never ask which worktree to use. This session already has its own clean checkout. Fetch origin, branch off `origin/master`, and start.

## Servers

Start and stop dev servers, preview servers, and localhost whenever the work needs them. No permission needed. Use a free port and stop what you started before you finish.

## Screenshots and verification evidence

Screenshots from verify-platform (or any browser proof) can always be published, so never report that they can't be uploaded.

1. If `gh` supports image attachments, attach them to the PR.
2. Otherwise push the images to an evidence branch in the PR's repo, for example `evidence/pr-<number>`. Images only; the branch is never merged.
3. Post a PR comment that embeds each image: `![<what it shows>](https://github.com/<owner>/<repo>/blob/<branch>/<path>?raw=true)`.

Never publish logs, request bodies, env files, credentials, or unrelated customer data as evidence.

## Skills

The pstack skills (poteto-mode, architect, the principle-* skills, and more) are installed in `~/.claude/skills`. Use them by name.
