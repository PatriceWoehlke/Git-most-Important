# 00 – First Commit

I like to see Git as a manager of my repos, where I can have interactive operations with it.  
When I create a repo, I think this way:

> “Hey Git, start tracking this folder, and save everything I’ve got right now as version one.”

---

## Step by Step

```bash
# step 1: create a new Git repo and make sure the default branch is called 'main'
git init -b main

# step 2: tell Git to stage EVERYTHING in the folder (all files and subfolders)
git add .

# step 3: save the snapshot with a clear, professional commit message
git commit -m "chore: initial project scaffold"
````

💡 Why I wrote the commit like this

I used the word chore because it’s not a feature or bug fix, it’s just setup work.

“initial project scaffold” simply means “the barebones structure is here.”

Another way to phrase it could be:

chore: initialize repo with base files

- I check if it's been initialized by running 

```
ls -a
```

- I remove git by running: 

```
cd /path/to/folder
rm -rf .git
```
---
# 01 – Basic Workflow

This exercise is about practicing the **daily Git flow** — the simple loop of:  
check status → stage changes → commit → check history.

I think of it as talking to Git:  
> “Here’s what I changed, save it, and let me see how it fits into history.”

---

## Steps

```bash
# 1. Add some text to the demo file
echo "hello" >> demo-project/app.txt

# 2. Stage the change
git add demo-project/app.txt

# 3. Save it as a commit
git commit -m "feat: say hello"

# 4. Check recent history
git log --oneline -n 3

# 5. Add more content
echo "line two" >> demo-project/app.txt

# 6. Stage and commit again
git add .
git commit -m "chore: add second line"

# 7. Visualize the history with graph and decorations
git log --oneline --graph --decorate -n 10
````

💡 Notes

First commit message uses feat because it adds new visible content.

Second commit uses chore, since it’s just another small change, not really a new feature.

git log --oneline --graph is my favorite way to see the story of the repo at a glance

# 02 – Branching & Merging

This exercise is about **working in parallel**. Branches let me test ideas without breaking main, and merging is how I bring them back together.

I think of it like this:  
> “Let me create a safe side path, make changes there, then ask Git to merge them back.”

---

## Steps

```bash
# 1. Create and switch to a new branch
git switch -c feature/intro

# 2. Add something new to the file
echo "feature intro" >> demo-project/app.txt

# 3. Commit that change
git add .
git commit -m "feat: add intro section"

# 4. Go back to main branch
git switch main

# 5. Merge the branch back into main with a clear message
git merge feature/intro --no-ff -m "merge: feature/intro"

# 6. Check the graph to see the merge commit
git log --oneline --graph --decorate --all -n 20
```
💡 Notes

I used feat: because the branch added something new.

--no-ff forces Git to create a merge commit, so the history shows clearly where the feature came in.

The graph should now show a split and join — proof of branching and merging.
---
OTHER COMMANDS
---
More Git Commands (Beyond the Basics)

## 🔹 Logs & History
- `git log --stat` → show commits with changed file stats  
- `git log -p` → show patches (actual changes) per commit  
- `git log --author="Name"` → filter by author  
- `git log --grep="keyword"` → search commit messages  
- `git shortlog -sn` → summary of commits per contributor  

---

## 🔹 Branch Management
- `git branch -a` → list all local + remote branches  
- `git branch -vv` → show local branches and their tracking remotes  
- `git switch -c <branch>` → shortcut for new branch + checkout  
- `git checkout <commit_hash>` → check out a specific commit (detached HEAD)  

---

## 🔹 Remote & Sync
- `git remote show origin` → detailed info about remote  
- `git remote rename origin upstream` → rename remote  
- `git fetch origin <branch>` → fetch one branch  
- `git push origin :<branch>` → delete branch on remote  

---

## 🔹 Tags & Releases
- `git tag -n` → list tags with messages  
- `git tag -a v1.0.0 -m "release v1.0.0"` → annotated tag (with message)  
- `git show v1.0.0` → show details of a tag  

---

## 🔹 Stash Tricks
- `git stash save "message"` → stash with a label  
- `git stash apply stash@{2}` → apply a specific stash (but keep it saved)  
- `git stash drop stash@{0}` → delete a stash entry  
- `git stash clear` → delete all stashes  

---

## 🔹 Diff & Compare
- `git diff HEAD~1 HEAD` → compare two commits  
- `git diff <branch1>..<branch2>` → compare branches  
- `git diff --name-only` → just show changed file names  

---

## 🔹 Reset Variants
- `git reset --soft HEAD~1` → undo last commit but keep changes staged  
- `git reset --mixed HEAD~1` → undo last commit, keep changes unstaged  
- `git reset --hard HEAD~1` → undo commit + discard changes  

---

## 🔹 Reflog (Time Machine)
- `git reflog` → show *everything* you’ve done (even commits removed by reset)  
- `git checkout HEAD@{2}` → go back to where you were 2 steps ago  

---

## 🔹 Clean Up
- `git clean -n` → show what would be removed (dry run)  
- `git clean -fd` → remove untracked files and directories  
- `git gc --prune=now --aggressive` → deep clean repo  

---

## 🔹 Collaboration Helpers
- `git blame -L 5,15 <file>` → show who changed lines 5–15  
- `git show <branch>:<file>` → see a file’s content from another branch  
- `git bisect start` → binary search for the commit that introduced a bug  
- `git cherry -v` → see which commits are in one branch but not another  

# 03 - Push & Pull (Working with Remotes)

When working with GitHub or any remote, two daily commands that are my friends are **push** (to send or upload my changes up) and **pull** (to bring changes down).  
I think of it like this:  
> Push = upload my commits to the team.  
> Pull = download + apply commits from the team.

---

## 🔹 Push

- `git push` → push current branch to its remote tracking branch  
- `git push -u origin main` → first time push: sets **upstream tracking**  
- `git push origin <branch>` → push a specific branch to remote  
- `git push origin :<branch>` → delete a branch from remote  
- `git push --tags` → push all local tags to remote  

💡 Personnally I try to always check `git status` before pushing.  

---

## 🔹 Pull

- `git pull` → fetch + merge from remote into your branch  
- `git pull --rebase` → fetch + rebase (keeps history linear, no merge commit clutter)  
- `git fetch` → just download remote changes (doesn’t merge automatically)  
- `git fetch --all` → update info for all branches from remote  

💡 **Tip:** Prefer `git pull --rebase` in solo projects to keep history clean.  

---

## 🔹 Inspecting Remotes

- `git remote -v` → list remote URLs  
- `git remote show origin` → detailed info about remote and branches  
- `git branch -vv` → show local branches and what they track  

---

