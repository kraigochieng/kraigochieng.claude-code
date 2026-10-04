# kraigochieng.claude-code

My Claude Code setup, kept in git like my other config repos.

This repo follows the same pattern as
[kraigochieng.nvim](https://github.com/kraigochieng/kraigochieng.nvim) and
[kraigochieng.zsh](https://github.com/kraigochieng/kraigochieng.zsh).
The config directory is the git repo. There is no copy step and no symlink.

| Repo | Directory it tracks |
| --- | --- |
| `kraigochieng.nvim` | `~/.config/nvim` |
| `kraigochieng.claude-code` | `/etc/claude-code` |

## Contents

- `CLAUDE.md`: organization-managed policy instructions. Claude Code loads
  this file in every session. It sets the commit, issue, branch, and PR rules
  and the writing style.

## Set up on a new machine

```sh
sudo mkdir -p /etc/claude-code
sudo chown "$USER" /etc/claude-code
git clone git@github.com:kraigochieng/kraigochieng.claude-code.git /etc/claude-code
```

## Change the config

Edit the file in `/etc/claude-code`. Then use the normal workflow: open an
issue, branch, commit, and open a PR.
