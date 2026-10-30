# Git Command Reference

## 1. VERSION & HELP

```bash
git --version
git help
git help COMMAND
git COMMAND --help
```

## 2. CONFIGURATION

```bash
git config --list
git config --global --list
git config --local --list
git config --show-origin --list
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --local user.name "Your Name"
git config --local user.email "you@example.com"
git config --global --unset user.name
git config --global --unset user.email
git config --get user.name
git config --get user.email
git config --global core.editor "vim"
```

## 3. INITIALIZE & CLONE

```bash
git init
git init --initial-branch=main
git init --bare DIRECTORY
git clone URL
git clone URL DIRECTORY
git clone --depth 1 URL
git clone --branch BRANCH URL
git clone --single-branch --branch BRANCH URL
git rev-parse --show-toplevel
git rev-parse --is-inside-work-tree
```

## 4. STATUS & STAGING

```bash
git status
git status -sb
git add FILE
git add .
git add -A
git add --all
git add -u
git add -p
git add -f FILE
git restore --staged FILE
git reset
git diff
git diff FILE
git diff --staged
git diff --cached
git diff --stat
git diff --cached --stat
git diff --name-only
git diff --check
git diff --word-diff
```

## 5. COMMITS

```bash
git commit -m "MESSAGE"
git commit
git commit -am "MESSAGE"
git commit --allow-empty -m "MESSAGE"
git commit --amend
git commit --amend -m "MESSAGE"
git commit --amend --no-edit
git log
git log --oneline
git log -5
git log --oneline --decorate -n 10
git log --graph --oneline --all
git log --oneline --graph --decorate --all
git log --stat
git log -p
git log --author="NAME"
git log --since="1 week ago"
git log --follow -- FILE
git show
git show COMMIT_ID
git show HEAD~1
git show --stat COMMIT_ID
git show --name-only COMMIT_ID
git blame FILE
git shortlog -sn
```

## 6. BRANCHES

```bash
git branch
git branch -a
git branch -r
git branch -vv
git branch BRANCH
git branch --track BRANCH origin/BRANCH
git branch --unset-upstream
git branch -f BRANCH COMMIT_ID
git branch -m NEW_NAME
git branch -m OLD_NAME NEW_NAME
git branch -d BRANCH
git branch -D BRANCH
git branch --merged
git branch --no-merged
```

## 7. SWITCH

```bash
git switch BRANCH
git switch -c BRANCH
git switch --create BRANCH
git switch --track origin/BRANCH
git switch -
git switch --detach COMMIT_ID
git switch --discard-changes BRANCH
```

## 8. CHECKOUT

```bash
git checkout BRANCH
git checkout -b BRANCH
git checkout -B BRANCH
git checkout .
git checkout -- FILE
git checkout COMMIT_ID
git checkout --orphan BRANCH
git checkout --track origin/BRANCH
git checkout --detach COMMIT_ID
git checkout HEAD~1 -- FILE
git checkout -p
git checkout -f BRANCH
```

## 9. MERGE

```bash
git merge BRANCH
git merge --no-ff BRANCH
git merge --ff-only BRANCH
git merge --squash BRANCH
git merge --no-edit BRANCH
git merge --abort
git merge --continue
git merge-base BRANCH1 BRANCH2
git mergetool
git diff --name-only --diff-filter=U
```

## 10. REBASE

```bash
git rebase BRANCH
git rebase main
git rebase -i HEAD~3
git rebase -i HEAD~N
git rebase --continue
git rebase --abort
git rebase --skip
git rebase --edit-todo
git rebase --show-current-patch
git rebase --onto NEW_BASE OLD_BASE BRANCH
git rebase --onto main OLD_BASE BRANCH
git pull --rebase
```

## 11. CHERRY-PICK

```bash
git cherry-pick COMMIT_ID
git cherry-pick COMMIT1 COMMIT2
git cherry-pick --no-commit COMMIT_ID
git cherry-pick --continue
git cherry-pick --abort
git cherry-pick --skip
```

## 12. REMOTES

```bash
git remote
git remote -v
git remote add origin URL
git remote set-url origin URL
git remote remove origin
git remote rename OLD_NAME NEW_NAME
git remote get-url origin
git remote show origin
git remote prune origin
git remote set-head origin --auto
git ls-remote origin
```

## 13. FETCH & PULL

```bash
git fetch
git fetch origin
git fetch --all
git fetch --prune
git fetch origin BRANCH
git fetch origin main:refs/remotes/origin/main
git pull
git pull origin main
git pull --rebase
git pull --no-rebase
git pull --ff-only
git branch -u origin/main
git branch --set-upstream-to=origin/main
```

## 14. PUSH

```bash
git push
git push origin main
git push -u origin main
git push -u origin HEAD
git push --set-upstream origin BRANCH
git push origin BRANCH
git push origin HEAD:BRANCH
git push --all origin
git push origin --tags
git push --follow-tags
git push --dry-run
git push --atomic origin main
git push --force
git push --force origin BRANCH
git push --force-with-lease
git push --force-with-lease origin BRANCH
git push origin +LOCAL_BRANCH:REMOTE_BRANCH
git push --force origin LOCAL_BRANCH:REMOTE_BRANCH
git push --delete origin BRANCH
git push origin --delete BRANCH
git push origin :BRANCH
```

## 15. FORCE PUSH & REMOTE HISTORY REWRITE

```bash
git push --force-with-lease origin LOCAL_BRANCH:REMOTE_BRANCH
git push --force origin LOCAL_BRANCH:REMOTE_BRANCH
git push --force-with-lease origin main
git push --force origin main
```

## 16. UNDO CHANGES

```bash
git restore FILE
git restore .
git restore --staged FILE
git restore --source=HEAD~1 FILE
git reset --soft HEAD~1
git reset --soft COMMIT_ID
git reset --mixed HEAD~1
git reset --mixed COMMIT_ID
git reset HEAD~1
git reset HEAD FILE
git reset COMMIT_ID -- FILE
git reset --hard HEAD~1
git reset --hard COMMIT_ID
git reset --hard HEAD
git revert COMMIT_ID
git revert HEAD
git revert --no-edit COMMIT_ID
git revert --abort
git revert --continue
git reflog
git reflog --all
git reset --hard 'HEAD@{1}'
```

## 17. UNDO LAST COMMIT

```bash
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
git revert HEAD
```

## 18. STASH

```bash
git stash
git stash push -m "MESSAGE"
git stash push -- FILE
git stash -u
git stash -a
git stash list
git stash show
git stash show -p
git stash show --stat stash@{0}
git stash apply
git stash apply stash@{1}
git stash pop
git stash branch NEW_BRANCH
git stash drop stash@{0}
git stash clear
```

## 19. DELETE FILES

```bash
git rm FILE
git rm -r DIRECTORY
git rm --cached FILE
git rm -r --cached DIRECTORY
git rm -f FILE
git mv OLD_NAME NEW_NAME
git clean -n
git clean -nd
git clean -f
git clean -fd
git clean -fdn
git clean -i
git clean -X -n
git clean -fx
git clean -fdx
git clean -ffdx
```

## 20. .GITIGNORE

```bash
touch .gitignore
git check-ignore FILE
git check-ignore -v FILE
git ls-files
git ls-files --others --exclude-standard
```

## 21. TAGS

```bash
git tag
git tag TAG_NAME
git tag -a TAG_NAME -m "MESSAGE"
git show TAG_NAME
git push origin TAG_NAME
git push origin --tags
git tag -d TAG_NAME
git push origin --delete TAG_NAME
git push origin :refs/tags/TAG_NAME
```

## 22. CONFLICTS

```bash
git status
git diff
git diff --check
git diff --name-only --diff-filter=U
git add RESOLVED_FILE
git merge --continue
git merge --abort
git rebase --continue
git rebase --abort
git cherry-pick --continue
git cherry-pick --abort
```

## 23. RESET & RECOVERY

```bash
git reflog
git reflog --all
git fsck --full
git log --oneline --all --reflog
git branch recovery COMMIT_ID
git switch -c recovery COMMIT_ID
git branch recovery 'HEAD@{1}'
git reset --hard 'HEAD@{1}'
```

## 24. FORCE PULL / OVERWRITE LOCAL WITH REMOTE

```bash
git fetch origin
git reset --hard origin/main
git fetch origin
git reset --hard origin/BRANCH
git clean -fdn
git clean -fd
```

## 25. FORCE UPDATE LOCAL BRANCH FROM REMOTE

```bash
git fetch origin
git switch main
git reset --hard origin/main
```

## 26. DISCARD ALL LOCAL CHANGES

```bash
git reset --hard HEAD
git clean -fd
```

## 27. COMPARISONS

```bash
git diff BRANCH1..BRANCH2
git diff BRANCH1...BRANCH2
git diff COMMIT1 COMMIT2
git diff HEAD~1 HEAD
git diff --cached
git diff --merge-base main BRANCH
git log HEAD..origin/main --oneline
git log origin/main..HEAD --oneline
```

## 28. STATS & OBJECTS

```bash
git rev-parse HEAD
git rev-parse --abbrev-ref HEAD
git rev-parse --verify HEAD
git cat-file -t OBJECT_ID
git cat-file -p OBJECT_ID
git ls-tree HEAD
git ls-tree -r --name-only HEAD
git show-ref
git count-objects -v
git fsck --full
git gc
git diff-tree --no-commit-id --name-only -r COMMIT_ID
```

## 29. TEMPORARY COMMITS & PATCHES

```bash
git format-patch -1 HEAD
git format-patch -N COMMIT_ID
git apply PATCH_FILE
git apply --check PATCH_FILE
git apply --stat PATCH_FILE
git diff > changes.patch
git diff > changes.diff
```

## 30. BISECT

```bash
git bisect start
git bisect bad
git bisect good COMMIT_ID
git bisect reset
git bisect log
git bisect skip
git bisect run COMMAND
```

## 31. WORKTREES

```bash
git worktree list
git worktree add ../project-feature BRANCH
git worktree add -b NEW_BRANCH ../project-feature
git worktree add --detach ../project-detached COMMIT_ID
git worktree remove ../project-feature
git worktree remove --force DIRECTORY
git worktree prune
git worktree lock DIRECTORY
git worktree unlock DIRECTORY
```

## 32. SUBMODULES

```bash
git submodule add URL DIRECTORY
git submodule init
git submodule update
git submodule update --init --recursive
git submodule update --remote
git submodule status
git submodule deinit DIRECTORY
git submodule foreach COMMAND
```

## 33. SQUASH & HISTORY

```bash
git merge --squash BRANCH
git commit --amend
git rebase -i HEAD~N
git log --oneline --graph --decorate --all
```

## 34. REMOTE BRANCH CLEANUP

```bash
git fetch --prune
git remote prune origin
git branch -r
git branch -vv
git push origin --delete BRANCH
```

## 35. GITHUB / GITLAB WORKFLOW

```bash
git init --initial-branch=main
git add .
git commit -m "Initial commit"
git remote add origin URL
git push -u origin main
```

## 36. DAILY WORKFLOW

```bash
git status
git switch main
git pull
git switch -c feature/NAME
git status
git diff
git add .
git diff --staged
git commit -m "Describe changes"
git push -u origin feature/NAME
git log --oneline --graph --all
```

## 37. GIT ALIASES

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
```

## 38. LEARN GIT BRANCHING

- [ ] Practice Main: first four sections.
- [ ] Practice Remote: both sections.
- [ ] Repeat the game at least three times.

---

## IMPORTANT: DANGEROUS COMMANDS

**Warning:** These commands can permanently delete local changes, untracked files, or rewrite shared remote history.

```bash
git reset --hard
git clean -fdx
git checkout -f BRANCH
git push --force
```

Prefer `git push --force-with-lease` over `git push --force` when a force push is necessary.
