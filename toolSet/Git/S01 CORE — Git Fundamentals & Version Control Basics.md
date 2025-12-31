## 🔹 1.1 Version Control Philosophy & Setup

- **Version Control** : what it is, benefits, use cases
    
- **Models** : centralized vs distributed
    
- **Git Philosophy** : immutable snapshots, content-addressed storage
    
- **Git vs Others** : SVN, Mercurial, Perforce
    
- **Lifecycle** : working directory → staging area (index) → repository
    
- **Installation** : package managers, official installers
    
- **Initial Config**
    
    - `git config --global/--local`
        
    - `user.name`, `user.email`
        
    - default editor & merge tool
        
    - line endings : `core.autocrlf`
        
- **Authentication**
    
    - SSH keys : `ssh-keygen`, ssh-agent
        
    - HTTPS credentials
        
    - SSH vs HTTPS trade-offs
        
- **Hosting Platforms** : GitHub, GitLab, Bitbucket setup
    
- **Credential Helpers** : `store`, `cache`, OS managers
    
- **Global Config Files**
    
    - `~/.gitconfig` structure
        
    - global ignore : `.gitignore_global`
        

---

## 🔹 1.2 Repository Basics

- **Initialize**
    
    - `git init`
        
    - bare repos : `git init --bare`
        
- **Clone**
    
    - `git clone`
        
    - shallow : `--depth`
        
    - mirror : `--mirror`
        
    - single branch : `--single-branch`
        
- **.git Directory**
    
    - `HEAD`, `config`, `objects/`, `refs/`
        
- **Refs & HEAD** : pointers to commits
    
- **Areas** : working tree vs index vs history
    
- **File States** : tracked, untracked, ignored
    
- **Ignore Rules**
    
    - patterns, negation `!`, dirs, wildcards
        
    - per-repo : `.gitignore`
        
    - global ignore
        
    - excludes : `.git/info/exclude`
        
- **Status** : `git status`, short `-sb`
    
- **Config Levels** : `git config --list --show-origin`
    

---

## 🔹 1.3 Basic Git Operations

- **Core Workflow** : add → commit → push → pull
    
- **Staging**
    
    - all : `git add -A`
        
    - update : `git add -u`
        
    - patch : `git add -p`
        
- **Commit**
    
    - message : `git commit -m`
        
    - stage+commit : `-a`
        
    - editor commit
        
- **Commit Messages**
    
    - imperative mood
        
    - 50/72 rule
        
- **History**
    
    - `git log --oneline --graph --decorate --stat`
        
    - pretty formats
        
- **Amend** : `git commit --amend`
    
- **Unstage** : `git restore --staged`
    
- **Discard** : `git restore`, `git checkout --`
    
- **Diffs**
    
    - working : `git diff`
        
    - staged : `git diff --cached`
        
    - word diff : `--color-words`
        
- **Compare** : `git diff A..B`, branches
    

---

## 🔹 1.4 Branching Fundamentals

- **Branches** : pointers to commits
    
- **Create**
    
    - `git branch <name>`
        
    - `git switch -c <name>`
        
    - `git checkout -b <name>`
        
- **Switch** : `git switch`, `git checkout`
    
- **List / Filter**
    
    - local : `git branch`
        
    - all : `-a`, remotes : `-r`
        
    - merged : `--merged`
        
- **Naming** : `feature/`, `bugfix/`, `hotfix/`
    
- **Detached HEAD** : at commit/tag
    
- **Delete**
    
    - local : `-d/-D`
        
    - remote : `git push origin --delete`
        
- **Local vs Remote-Tracking** : `origin/main`
    
- **Upstream**
    
    - `-u` on push
        
    - `--set-upstream-to`
        

---

## 🔹 1.5 Merging Basics

- **Merge Types**
    
    - fast-forward
        
    - true three-way
        
- **Merge Command** : `git merge <branch>`
    
- **Messages** : auto vs custom
    
- **History View** : graph logs
    
- **Parents** : multiple parents in merge commits
    
- **Conflicts**
    
    - markers : `<<<<<<<`, `=======`, `>>>>>>>`
        
    - manual resolution
        
- **Abort** : `git merge --abort`
    
- **Continue** : resolve → `git commit`
    
- **Tools**
    
    - `git mergetool`
        
    - Visual : VS Code, Meld, KDiff3
        

---

## 🔹 1.6 Remote Repositories

- **Remotes** : named URLs, default `origin`
    
- **Manage**
    
    - add : `git remote add`
        
    - remove : `rm`
        
    - rename : `rename`
        
    - change URL : `set-url`
        
- **Inspect** : `git remote -v`, `git remote show`
    
- **Fetch** : `git fetch`, `--prune`
    
- **Pull**
    
    - fetch + merge
        
    - rebase option : `--rebase`
        
- **Push**
    
    - `git push`
        
    - set upstream : `-u`
        
    - tags : `--tags`
        
- **Rejected Pushes** : pull/rebase then push
    
- **Upstream vs Downstream**
    
- **Fetch vs Pull** : update refs vs integrate
    
- **Multiple Remotes** : origin, upstream flows
    

---

## 🔹 1.7 Basic Collaboration

- **Fork vs Clone**
    
- **Open Source Flow**
    
    - fork → clone → branch → commit → push → PR/MR
        
- **Pull / Merge Requests** : GitHub, GitLab, Bitbucket
    
- **Code Review** : comments, approvals
    
- **Sync Forks**
    
    - add `upstream`
        
    - fetch & merge/rebase
        
- **References**
    
    - commits in issues
        
    - close keywords : `fixes #123`
        
- **Commit Conventions** : Conventional Commits (feat, fix, docs)
    
- **Etiquette**
    
    - small focused commits
        
    - clear messages
        
    - rebase before PR
        
- **Protection Rules** : required reviews, CI checks
    

---

If you want, next I can extend this map with:

- **Rebasing, stashing, tags, cherry-pick, reflog, bisect** (advanced Git).
    
- A **one-page Git workflow cheatsheet**.
    
- Or a **Dev Tool Index** linking Git with Docker, CI/CD, and cloud notes.