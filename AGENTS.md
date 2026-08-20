# AGENTS.md

## Repository overview

This repository contains Yuqi Gu's academic website, built with Jekyll and the
al-folio theme. These instructions apply to the entire repository.

- Editable site sources live on the `source` branch.
- Jekyll writes the generated site to `_site/`. It is ignored by Git and must
  not be committed on `source`.
- The generated site is published from the `gh-pages` branch in a separate
  checkout.
- The site uses Ruby 3.2.2 from `.ruby-version` and Bundler 2.2.21 from
  `Gemfile.lock`.

Repository locations:

```text
Source:     /Users/yuqigu/Dropbox/al-folio
Publishing: /Users/yuqigu/Dropbox/Misc/github_pages_repo/yuqigu.github.io
```

`/Users/yuqigu/Dropbox` is a symlink to the current Dropbox CloudStorage
directory, so use the paths above for the established workflow.

## Working rules

- Start by running `git status --short --branch` and inspect existing changes.
- Treat pre-existing modified or untracked files as user work. Do not edit,
  stage, discard, stash, or commit them unless they are part of the request.
- Keep changes focused. Stage explicit paths instead of using `git add .`.
- Do not amend commits, rewrite history, force-push, or use destructive Git
  commands unless the user explicitly requests the operation.
- A request to edit or build does not authorize a commit, push, or deployment.
  Perform each of those operations only when the user explicitly asks for it.
- Do not edit generated files in `_site/` or in the publishing checkout by
  hand. Make changes to the source and rebuild.

## Build and validation

Run commands from the source repository root:

```bash
cd /Users/yuqigu/Dropbox/al-folio
/opt/homebrew/bin/rbenv exec ruby --version
/opt/homebrew/bin/rbenv exec bundle _2.2.21_ exec jekyll build
```

If dependencies have not been installed, use:

```bash
/opt/homebrew/bin/rbenv exec gem install bundler:2.2.21
/opt/homebrew/bin/rbenv exec bundle _2.2.21_ install
```

Use `rbenv exec` here because non-interactive shells on this machine may select
macOS's Ruby 2.6 even though the repository's `.ruby-version` specifies 3.2.2.

Before handing off a change, inspect the relevant diff and run the Jekyll build
when the change can affect the rendered site. Report any failure and do not
deploy a failed build.

## Commit source changes

Commit only after the user asks for a commit.

1. Confirm the intended changes and branch:

   ```bash
   cd /Users/yuqigu/Dropbox/al-folio
   git status --short --branch
   git branch --show-current
   git diff --check
   ```

2. The normal source branch is `source`. Do not switch branches while the
   worktree contains changes that could be overwritten.

3. Stage only the requested paths, then review exactly what will be committed:

   ```bash
   git add -- path/to/requested-file another/requested-file
   git diff --cached --check
   git diff --cached --stat
   git diff --cached
   ```

4. Create a focused commit with an imperative message that describes the source
   change:

   ```bash
   git commit -m "<concise description>"
   ```

5. Re-run `git status --short --branch` and report the commit hash. Do not
   include unrelated working-tree changes in the commit.

## Push source changes

Push only after the user asks for a push. Confirm the source commit is on
`source`, then run:

```bash
cd /Users/yuqigu/Dropbox/al-folio
git status --short --branch
git push origin source
```

Do not use `--force` or `--force-with-lease`. The repository contains
`.github/workflows/deploy.yml`, so a source push may also start the legacy
GitHub Actions deployment workflow. The manual publishing procedure below
remains the established deployment path for `gh-pages`.

## Deploy the generated site

Deploy only after the user explicitly asks for deployment. A deployment must
come from a clean, committed, and pushed `source` checkout so that the published
site corresponds to a reproducible source commit.

1. Define and verify the two exact checkouts:

   ```bash
   SOURCE_REPO=/Users/yuqigu/Dropbox/al-folio
   PUBLISH_REPO=/Users/yuqigu/Dropbox/Misc/github_pages_repo/yuqigu.github.io
   git -C "$SOURCE_REPO" status --short --branch
   git -C "$PUBLISH_REPO" status --short --branch
   ```

   Stop if either checkout has unexpected changes. Confirm the source checkout
   is on `source` and the publishing checkout is on `gh-pages`.

2. Confirm the source commit has been pushed and update the publishing checkout
   without rewriting history:

   ```bash
   git -C "$SOURCE_REPO" fetch origin source
   test "$(git -C "$SOURCE_REPO" rev-parse HEAD)" = \
     "$(git -C "$SOURCE_REPO" rev-parse origin/source)"
   git -C "$PUBLISH_REPO" switch gh-pages
   git -C "$PUBLISH_REPO" pull --ff-only origin gh-pages
   ```

   If the commit comparison fails or the pull is not fast-forwardable, stop and
   report the problem instead of forcing the operation.

3. Build from the clean source checkout:

   ```bash
   cd "$SOURCE_REPO"
   /opt/homebrew/bin/rbenv exec bundle _2.2.21_ exec jekyll build
   ```

4. Synchronize the complete generated output into the publishing checkout:

   ```bash
   rsync -a --delete \
     --exclude='.git/' \
     --exclude='.nojekyll' \
     --exclude='CNAME' \
     "$SOURCE_REPO/_site/" "$PUBLISH_REPO/"
   ```

   Use `rsync --delete` instead of `cp -R _site/*` so obsolete generated files
   are removed. The exclusions preserve Git metadata and GitHub Pages control
   files.

5. Review and commit the generated changes from the publishing checkout:

   ```bash
   cd "$PUBLISH_REPO"
   git status --short
   git diff --check
   git diff --stat
   git add -A
   git diff --cached --check
   git diff --cached --stat
   git commit -m "deploy: static build $(date +%Y-%m-%d)"
   ```

   If there are no generated changes, do not create an empty deployment commit.

6. Push and verify the publishing branch:

   ```bash
   git push origin gh-pages
   git status --short --branch
   git log -1 --oneline
   ```

   Report the deployment commit hash and any verification performed against
   `https://yuqigu.github.io/`.

## Legacy deployment script

Do not use `bin/deploy` for the normal deployment workflow. The current script
deletes and recreates a local deployment branch, removes files, and force-pushes
the result. Run it only if the user specifically requests that script and
acknowledges those effects.
