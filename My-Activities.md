# Basic Workflow

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
```

#  Branching & Merging

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

---

```markdown
# 03 – Rebase vs Merge

Here I’m learning the **difference between merging and rebasing**.  
Merging keeps the full story with all the bumps, while rebasing rewrites history into a clean straight line.

I think of it like this:  
> Merge = keep the family tree.  
> Rebase = rewrite the story like it was always in order.

---

## Steps

```bash
# 1. Create a feature branch
git switch -c feature/rebase-demo

# 2. Add a change in the feature branch
echo "rebase demo line" >> demo-project/app.txt
git add .
git commit -m "feat: rebase demo change"

# 3. Simulate work on main at the same time
git switch main
echo "parallel main change" >> demo-project/app.txt
git add .
git commit -m "feat: main parallel change"

# 4. Rebase feature branch onto main
git switch feature/rebase-demo
git rebase main

# 5. Merge back after rebase (fast-forward)
git switch main
git merge feature/rebase-demo

# 6. Visualize
git log --oneline --graph --decorate --all -n 30
```
Notes

Rebasing rewrote the history so my feature commit now looks like it came after the main commit.

Merge would have shown two lines joining, rebase makes it linear.

Both are valid; teams choose based on style.

