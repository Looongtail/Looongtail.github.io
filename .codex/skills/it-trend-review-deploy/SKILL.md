---
name: it-trend-review-deploy
description: "Review a completed IT Trend post and, after explicit approval, commit, deploy, and verify it on GitHub Pages. Use after it-trend-publishing; do not use for authoring or unrelated site changes."
---

# It Trend Review Deploy

Use this as the second stage of the IT Trend publishing chain, after `it-trend-publishing` has created or revised a specific post and its local assets. Its purpose is to independently check that deliverable, then safely publish only the approved files.

## Handoff and review

- Identify the exact post and asset files produced by the authoring stage. Begin with read-only checks: inspect the relevant diff, frontmatter, links, image paths and captions, and existing post style.
- Verify that the post satisfies `codes/src/content.config.ts`, that its URL slug is stable, and that all referenced local assets exist under `codes/public/`.
- Run `git diff --check` and `pnpm build` from `codes/`. Treat build errors, broken references, unsupported metadata, or unclear source attribution as a failed review.
- Do not silently rewrite a draft during review. Report defects clearly and return the work to `it-trend-publishing` for editorial or visual corrections. Re-review the corrected files before publishing.
- Preserve unrelated staged, unstaged, and untracked work. In particular, never delete or stage files in `codes/writing/` merely because they are present.

## Approval gate

Reviewing and building do not authorize publication. Before creating a commit or pushing, show the user:

- the exact files that will be staged;
- the target branch and remote;
- the proposed commit message; and
- the build result.

Request explicit confirmation immediately before the commit/push. If the user approves only a subset, stage only that subset. Never use broad staging such as `git add .` or publish a mixed set of unrelated changes.

## Publish and verify

After approval, work from `codes/`:

1. Stage only the confirmed post and asset files, then create a focused commit.
2. Push the confirmed branch. The normal production path is `master`, which triggers the GitHub Pages workflow; do not substitute a different branch or remote without the user's direction.
3. Check the resulting GitHub Actions deployment and the public post URL when access is available. If either cannot be checked, state that plainly and provide the relevant URL rather than claiming success.
4. Report the commit hash, branch, files published, deployment outcome, and final public URL.

Stop after a failed push or deployment check. Do not force-push, amend published history, or retry a failing deployment by changing content without new user direction.
