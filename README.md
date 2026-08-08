# dotfiles

Machine setup, managed with [GNU Stow](https://www.gnu.org/software/stow/). Each
top-level directory is a "package" whose contents mirror `$HOME` — stowing a
package symlinks its files into place.

## Install

```bash
git clone git@github.com:buzzedword/dotfiles.git
cd dotfiles
./setup.sh          # installs Homebrew if needed, brew bundles, then stows every package
./setup.sh git       # or just one
```

`.stowrc` sets the default target to `$HOME`, so plain `stow <package>` also
works without flags once you're inside this directory.

If a real (non-symlink) dotfile already exists at the target path — e.g. a
fresh machine's default `~/.gitconfig` — Stow will refuse to overwrite it.
Move it aside first:

```bash
mv ~/.gitconfig ~/.gitconfig.pre-dotfiles-backup
```

## Adding a new package

Create a directory named after the tool, laid out exactly as it should
appear under `$HOME` (e.g. `zsh/.zshrc`, `tmux/.tmux.conf`), then run
`./setup.sh <package>`. `setup.sh` with no arguments auto-discovers and
stows every package directory, so nothing else needs to be wired up.

## Why not the `stow .` / `~/.config` pattern?

This repo isn't cloned as a direct child of `$HOME`, and targets classic
`$HOME` paths rather than XDG's `~/.config`, mainly
because `git` only reads `$XDG_CONFIG_HOME/git/config` when `~/.gitconfig`
doesn't already exist. A single repo-root `stow .` would leak this
README/setup.sh as stray symlinks into `$HOME`, so packages are stowed
individually instead — same idea, adapted target.

## Packages

- `git` — `.gitconfig` with modern aliases (`st`, `ci`, `br`, `co`/`rs`,
  `df`, `wc`, `lg`, `cl`) and sane defaults (`main` default branch, rebase
  on pull, autoprune on fetch, etc).
