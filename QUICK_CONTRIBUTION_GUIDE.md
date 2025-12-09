# ⚡ Quick Contribution Reference

Fast reference for contributing to open source projects.

---

## 🚀 Quick Start (5 Steps)

```bash
# 1. Fork & Clone
git clone https://github.com/YOUR-USERNAME/project-name.git
cd project-name

# 2. Create Branch
git checkout -b fix-issue-123

# 3. Make Changes & Test
# ... edit files ...
pytest  # or npm test

# 4. Commit & Push
git add .
git commit -m "Fix: Description of fix"
git push origin fix-issue-123

# 5. Create Pull Request on GitHub
```

---

## 🔍 Finding Projects

### Best Websites
- https://goodfirstissue.dev/
- https://www.firsttimersonly.com/
- https://up-for-grabs.net/
- https://github.com/topics/good-first-issue

### GitHub Search
```
is:issue is:open label:"good-first-issue" language:Python
```

---

## 📝 Commit Message Format

```
Type: Brief description (50 chars max)

Detailed explanation (if needed)

Fixes #123
```

**Types:**
- `Fix:` - Bug fixes
- `Feat:` - New features
- `Docs:` - Documentation
- `Style:` - Formatting
- `Refactor:` - Code restructuring
- `Test:` - Adding tests
- `Chore:` - Maintenance

**Examples:**
```bash
git commit -m "Fix: Resolve null pointer exception in login"
git commit -m "Docs: Add examples to README"
git commit -m "Feat: Add dark mode support"
```

---

## 🎯 Recommended Projects for You

### Python/ML Projects
| Project | Focus | Label |
|---------|-------|-------|
| [Scikit-learn](https://github.com/scikit-learn/scikit-learn) | Machine Learning | `good-first-issue` |
| [Pandas](https://github.com/pandas-dev/pandas) | Data Analysis | `good-first-issue` |
| [Matplotlib](https://github.com/matplotlib/matplotlib) | Visualization | `good-first-issue` |
| [Streamlit](https://github.com/streamlit/streamlit) | Web Apps | `good-first-issue` |
| [Jupyter](https://github.com/jupyter/notebook) | Notebooks | `good-first-issue` |

### Quick Links
- **Scikit-learn Issues:** https://github.com/scikit-learn/scikit-learn/labels/good%20first%20issue
- **Pandas Issues:** https://github.com/pandas-dev/pandas/labels/good%20first%20issue
- **Streamlit Issues:** https://github.com/streamlit/streamlit/labels/good%20first%20issue

---

## 🔄 Git Commands Cheat Sheet

### Setup
```bash
# Configure Git
git config --global user.name "Akrati Mishra"
git config --global user.email "akratimishra366@gmail.com"

# Clone repository
git clone https://github.com/username/repo.git

# Add upstream
git remote add upstream https://github.com/original/repo.git
```

### Branching
```bash
# Create and switch to branch
git checkout -b feature-name

# Switch branches
git checkout main

# List branches
git branch -a

# Delete branch
git branch -d feature-name
```

### Changes
```bash
# Check status
git status

# Stage all changes
git add .

# Stage specific file
git add filename.py

# Commit
git commit -m "Message"

# Amend last commit
git commit --amend
```

### Syncing
```bash
# Fetch upstream changes
git fetch upstream

# Merge upstream into main
git checkout main
git merge upstream/main

# Push to your fork
git push origin main

# Pull latest changes
git pull origin main
```

### Undoing
```bash
# Discard changes in file
git checkout -- filename.py

# Unstage file
git reset HEAD filename.py

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1
```

---

## ✅ Pre-Submission Checklist

Before creating a PR:

- [ ] Code follows project style guide
- [ ] All tests pass
- [ ] Added tests for new code
- [ ] Updated documentation
- [ ] Commit messages are clear
- [ ] Branch is up-to-date with main
- [ ] No merge conflicts
- [ ] Tested locally
- [ ] Read CONTRIBUTING.md

---

## 📋 Pull Request Template

```markdown
## Description
Brief description of changes

## Related Issue
Fixes #123

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Code refactoring

## Changes Made
- Change 1
- Change 2
- Change 3

## Testing
- [ ] Tested locally
- [ ] All tests pass
- [ ] Added new tests

## Screenshots (if applicable)
[Add screenshots]

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-reviewed code
- [ ] Commented complex code
- [ ] Updated documentation
- [ ] No new warnings
```

---

## 🐛 Common Issues & Solutions

### Issue: "Permission denied (publickey)"
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "akratimishra366@gmail.com"

# Add to GitHub: Settings → SSH Keys
```

### Issue: "Merge conflict"
```bash
# Update your branch
git fetch upstream
git rebase upstream/main

# Resolve conflicts in files
# Then:
git add .
git rebase --continue
git push origin branch-name --force
```

### Issue: "Commit to wrong branch"
```bash
# Stash changes
git stash

# Switch to correct branch
git checkout correct-branch

# Apply changes
git stash pop
```

### Issue: "Need to update PR"
```bash
# Make changes
git add .
git commit -m "Address review feedback"
git push origin branch-name

# PR updates automatically
```

---

## 💬 Communication Templates

### Claiming an Issue
```
Hi! I'd like to work on this issue.

I'm planning to [describe approach].

Is this the right direction? Any suggestions?
```

### Asking for Help
```
I'm working on #123 and stuck on [specific problem].

What I've tried:
- Approach 1
- Approach 2

Could you point me in the right direction?
```

### Responding to Review
```
Thanks for the review!

I've addressed your feedback:
- Fixed the typo in line 45
- Added error handling as suggested
- Updated tests

Please let me know if anything else needs changes.
```

---

## 🎯 Contribution Workflow

```
1. Find Issue
   ↓
2. Comment on Issue (claim it)
   ↓
3. Fork Repository
   ↓
4. Clone Fork
   ↓
5. Create Branch
   ↓
6. Make Changes
   ↓
7. Test Thoroughly
   ↓
8. Commit with Clear Message
   ↓
9. Push to Fork
   ↓
10. Create Pull Request
   ↓
11. Respond to Feedback
   ↓
12. Merge! 🎉
```

---

## 📊 Track Your Progress

### Weekly Goals
- [ ] Find 3 potential issues
- [ ] Submit 1 pull request
- [ ] Review 2 other PRs
- [ ] Learn 1 new project

### Monthly Goals
- [ ] 4+ merged PRs
- [ ] Contribute to 2+ projects
- [ ] Help 5+ people in issues
- [ ] Write 1 blog post about contribution

---

## 🌟 Quick Tips

**DO:**
- ✅ Start with documentation
- ✅ Read CONTRIBUTING.md
- ✅ Ask questions
- ✅ Be patient
- ✅ Test thoroughly
- ✅ Follow code style

**DON'T:**
- ❌ Submit untested code
- ❌ Make unrelated changes
- ❌ Ignore feedback
- ❌ Be rude
- ❌ Spam maintainers
- ❌ Give up easily

---

## 📚 Resources

**Learning:**
- [First Contributions](https://github.com/firstcontributions/first-contributions)
- [GitHub Skills](https://skills.github.com/)
- [Open Source Guide](https://opensource.guide/)

**Finding Projects:**
- [Good First Issue](https://goodfirstissue.dev/)
- [Up For Grabs](https://up-for-grabs.net/)
- [CodeTriage](https://www.codetriage.com/)

**Communities:**
- [Dev.to](https://dev.to/)
- [Hashnode](https://hashnode.com/)
- [Reddit r/opensource](https://reddit.com/r/opensource)

---

## 🚀 Your First Contribution Today

1. **Go to:** https://goodfirstissue.dev/
2. **Filter by:** Python
3. **Pick an issue** that interests you
4. **Comment:** "I'd like to work on this"
5. **Follow** the workflow above
6. **Submit** your first PR!

---

**Need detailed guide?** Check [OPEN_SOURCE_GUIDE.md](OPEN_SOURCE_GUIDE.md)

**Questions?** Email akratimishra366@gmail.com

**Good luck! 🌟**