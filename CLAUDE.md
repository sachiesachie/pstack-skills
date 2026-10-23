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

## After you merge

- Watch the master Deploy run for your merge until it finishes (`gh run list --workflow Deploy --branch master`, then `gh run watch <id>`). This is the one CI wait that is required.
- If it fails, read the failing step, find whether your change caused it, and fix it (or report it with the cause if it is not yours). Never leave a red deploy behind you: every later merge is blocked until it is green.
- If your PR adds a platform-db migration, right before merging rename it to a timestamp after the newest migration on origin/master (`ls apps/platform/db/migrations | sort | tail -1`). The deploy refuses any migration dated before the last applied one.

## Skills

The pstack skills (poteto-mode, architect, the principle-* skills, and more) are installed in `~/.claude/skills`. Use them by name.

# Brevity (all prose you write to me, always)

Use half the words without dropping any fact. Write it short the first time; a trim pass afterward fails.

- Lead with the answer or result. No intro, no restating the question, no recap at the end.
- One idea per sentence. Short everyday words. Define a jargon term once, in plain words.
- Keep every fact, number, name, decision, tradeoff, and open question. Cut padding, not content.
- Cut: hedges, narration of what you did step by step, "I'll now", praise, repeated points, and anything I already know from this conversation.
- Exact names stay exact: paths, PR numbers, commands, API names.
- Use a list or table only when it is shorter than the sentences it replaces.
- If a reply runs past about 15 lines, check what can go. Detail I may need goes in a file or PR, with one line pointing to it.

Litmus: I get every fact by skimming, in half the time.
