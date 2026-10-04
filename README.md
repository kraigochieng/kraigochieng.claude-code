# kraigochieng.claude-code

My Claude Code configuration, kept in git so I can use the same setup on any
computer.

Clone the repo on a new machine and Claude Code behaves the same way as on my
other machines. When I change the config on one machine, I push it and pull it
on the others.

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
issue, branch, commit, and open a PR. After the merge, pull `main` on the
other machines.
