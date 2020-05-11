# Local setup

This isn't really my dotfiles but has some rough notes that hopefully helps someone.

## Apps

- magnet - arrange windows quickly
- unsplash - desktop changer
- dato - date app
- use spotlight search mapped to command-space
- hyper for terminal app

## Shell - hyper

- `zsh` using [oh-my-zsh](https://ohmyz.sh/)
  - [pure prompt](https://github.com/sindresorhus/pure)
  - plugins
    - https://github.com/zsh-users/zsh-autosuggestions
    - autocomplete from history

```sh
# open up the alias file
function zalias {
    `$EDITOR ~/.oh-my-zsh/custom/alias.zsh`
}

# reload aliases
alias ralias='source ~/.oh-my-zsh/custom/alias.zsh'     # reload aliases

z  # https://github.com/rupa/z use instead of cd
ag # silver searcher
ag -l componentWillMount # just list the files
ch # copy from clubhouse https://github.com/skyverge/jilt-scripts
fkill # fabulously kill processes https://github.com/sindresorhus/fkill-cli
yr cypress:watch
trash-cli # https://github.com/sindresorhus/trash-cli
```

### hyper plugins

```
  plugins: ['hyper-snazzy', 'hypercwd', 'hyperterm-summon', 'hyper-tabs-enhanced'],
```

### some interesting git and shell aliases

using https://hub.github.com/

```sh
alias git='hub'
gc # git checkout
gc - # checkout last used branch
function gc {
    git checkout $*
    # quick branch log
    echo `date "+%Y-%m-%d %H:%M:%S"` `git rev-parse --abbrev-ref HEAD` >> ~/dev/jilt/branchlog.txt
}

alias gl='git pull'
alias gp='git push --set-upstream'
alias gam='git commit --amend'

# git log showing some branches
alias glg='git log --graph --pretty=format:"%Cred%h%Creset - %s %Cgreen(%cr) - %C(yellow)%d%Creset" --abbrev-commit '

# ascii tree
alias tree-ascii='tree -L 2 -d --prune -I node_modules'

# list of branches
alias gbs="git for-each-ref --sort=committerdate refs/heads/ --format='%(color: cyan)%(committerdate:short) %(color: white)%(refname:short)'" # --no-merge

#git log fun
alias glg='git log --graph --pretty=format:"%Cred%h%Creset - %s %Cgreen(%cr) - %C(yellow)%d%Creset" --abbrev-commit '
alias glg-files='git log --name-status --find-renames'
alias glgs-files='glg-files'

# files that are different from master
alias git-diff-files-master='git diff --stat --cached origin/master --name-only'

# fetch origin without having to checkout master first
alias gfo='git fetch origin master:master'

# diff two files need https://github.com/so-fancy/diff-so-fancy
dif() {
    git diff --color --no-index "$1" "$2" | diff-so-fancy;
}

# Copy the prefix from the clipboard and checkout the branch
# ie ensure 12345/story-description is in your clipboard and run
# gcb
function gcb {
    git checkout -b ch`pbpaste`
    echo `date "+%Y-%m-%d %H:%M:%S"` `git rev-parse --abbrev-ref HEAD` >> ~/dev/jilt/branchlog.txt
}

# show the branchlog
alias bl='cat ~/dev/jilt/branchlog.txt'


function gs {
    git status
    if [ $# -eq 1 ]; then
        if test "$1" = "commit"; then
            return
        fi
    fi
    sh ~/scripts/eslint-changed-files.sh
}

```

## Editor: vscode

- font: [operator mono](https://www.typography.com/fonts/operator/styles)
- hover
- git integration
- merging
- shortcuts
- extensions
  - bracketing
  - code outline
  - more prettier

### danger git

```sh
git rebase -i master # interactive rebase
git commit --only --allow-empty -m "Trigger [ci run]"
# Thanks Lucas! - merge using strategies https://git-scm.com/docs/merge-strategies
git merge ch51454/migrate-storefront-coffee-to-es6 -s recursive -X ours ch51454/migrate-storefront-coffee-to-es6
```

### chrome

chrome - plugin json viewer

dev tools

- request blocking
- copy as fetch
- command p
