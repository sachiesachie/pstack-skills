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

## Pick checks by what changed
Run the narrowest check that can catch a failure in what you changed. Before any check that takes over 2 minutes, name the failure it would catch in this diff. If you can't name one, skip it and say why in the PR.

| What changed | Run |
|---|---|
| Copy, labels, docs, comments | lint and format on the touched files; a screenshot of the changed screen if users see it |
| Logic inside one module | that module's unit tests, typecheck |
| UI behavior | typecheck, verify-platform for that flow |
| DB, queue, provider, or another service; concurrency | every scenario that covers it; a long run is fine for a significant change |

- Re-run a scenario only if a commit since its last pass changed code that scenario runs. Rebases, copy edits and migration renames don't count. Cite the SHA of the last passing run instead.
- When you're done, list what you ran, and for each skipped check the reason it doesn't apply.

## Request Codex review (before human review)

- When your PR is ready, comment `@codex review` on it yourself. Ready means: the diff is complete, the checks picked under "Pick checks by what changed" pass, and screenshots are posted for any change users see.
- Do not wait for CI before you comment. Request Codex as soon as your local checks pass.
- Still fix CI: if a check fails, find the cause and push the fix. Don't babysit it to green.
- After you push fixes for a round of Codex comments, comment `@codex review` again, up to 3 rounds per PR. A round is one Codex review that left comments you fixed. After the third round, stop tagging Codex. Fix any remaining P1 yourself, then tell me the PR has used its 3 rounds and what Codex last flagged.
- A PR is ready for human review only when Codex has reviewed the latest head, no Codex P1 is unresolved, and CI is green. Then say so.
- If you pushed after your third round, Codex hasn't reviewed the head. Then the PR is ready once CI is green and you have fixed every Codex P1 you know of. Tell me, and I decide whether to tag Codex again. Jev won't merge it until Codex reviews the head.

## Jev auto-merge
- Add the `jev:automerge` label once Codex comes back clean on the head commit (no P0, P1 or unrated finding): `gh pr edit <n> --add-label "jev:automerge"`. Jev merges after CI is green, Codex has reviewed the head, and its own checks pass.
- Stacked and draft PRs can carry the label. Jev starts once the PR is marked ready and based on `master`.
- Skip the label and say why if any of these hold:
  - the diff touches a path Jev never merges: `.github/`, `.husky/`, `apps/terraform/`, migrations, `*.sql`, `apps/platform/db/`, `wrangler*`, or `packages/`
  - the diff is over 30 files or 1,000 changed lines
  - the PR needs a product or design call from me
  - a human reviewer has an open thread
- If Jev posts a stop, read why. Fix it if it's yours; otherwise tell me. Don't remove and re-add the label to force a retry.
- After it merges, watch the master deploy like any other merge.

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
