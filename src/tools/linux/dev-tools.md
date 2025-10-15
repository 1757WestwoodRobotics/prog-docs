# Development Tools on Linux for FRC

This page covers core development tools used in a Linux environment for FRC: Git, lazygit, Bash, and SSH. It focuses on practical workflows you’ll use daily when building and deploying robot code.

## Git: Version Control for Teams

Git helps you collaborate, review changes, and maintain a clean history.

### Essential Setup

```bash
# Set your identity (one-time)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Recommended: colored, helpful output
git config --global color.ui auto
git config --global init.defaultBranch main

# Optional: better logging alias
git config --global alias.lg "log --oneline --graph --decorate --all"
```

### Daily Workflow

```bash
# Clone the repository
git clone https://github.com/1757WestwoodRobotics/prog-docs

# Create a new feature branch
git checkout -b feature/robotpy-logging

# Stage and commit changes
git add src/tools/linux/*.md
git commit -m "docs(linux): add RoboRIO internals page"

# Rebase with latest main
git fetch origin
git rebase origin/main

# Push your branch
git push -u origin feature/robotpy-logging
```

### Reviewing Changes

```bash
# Inspect staged changes
git diff --staged

# See recent history
git lg
```

## lazygit: TUI for Git

lazygit is a terminal UI that accelerates common Git tasks.

### Installation (examples)

```bash
# Arch Linux
sudo pacman -S lazygit

# Debian/Ubuntu
sudo apt install lazygit
```

### Usage

```bash
lazygit
```

- Stage/unstage files, commit, rebase, resolve conflicts interactively
- Quickly view diffs and logs without memorizing commands

## Bash: Your Command-Line Companion

Bash lets you automate tasks and work efficiently.

### Basics You’ll Use Often

```bash
# Navigate
pwd; ls -la; cd src/tools/linux

# Search in repository
grep -R "roborio" -n src

# Create directories & files
mkdir -p src/tools/linux
printf "# New Page\n" > src/tools/linux/new-page.md

# Permissions
chmod +x scripts/deploy.sh
```

### Helpful Shortcuts

```bash
# Use aliases in ~/.bashrc or ~/.zshrc
alias gs='git status'
alias gl='git lg'
alias ll='ls -alF'
```

## SSH: Secure Remote Access

SSH connects you to the RoboRIO and other Linux machines.

### Common RoboRIO Hosts

- mDNS: `roborio-TEAM-frc.local`
- USB: `172.22.11.2`
- Ethernet: `10.TE.AM.2`

### Useful Commands

```bash
# Open a shell on the RoboRIO
ssh admin@roborio-TEAM-frc.local

# Copy files
scp ./robot.py admin@roborio-TEAM-frc.local:/home/lvuser/

# Forward a local port to remote
ssh -L 8080:localhost:80 admin@roborio-TEAM-frc.local

# Run a remote command
ssh admin@roborio-TEAM-frc.local "systemctl status robot"
```

### SSH Keys (recommended)

```bash
ssh-keygen -t ed25519 -C "you@example.com"
ssh-copy-id admin@roborio-TEAM-frc.local
```

## Tips for Team Collaboration

- Commit small, logical changes with clear messages
- Use branches for features and fixes
- Pull or rebase frequently to avoid large conflicts
- Use code reviews (PRs) to maintain quality

These tools form the backbone of an efficient Linux-based FRC workflow.

