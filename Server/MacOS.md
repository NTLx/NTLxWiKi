---
title: Mac OS
description: 
published: true
date: 2020-04-01T00:51:52.589Z
tags: 
---

# Zsh

```bash
brew install zsh zsh-autosuggestions zsh-completions zsh-git-prompt zsh-history-substring-search zsh-lovers zsh-navigation-tools zsh-syntax-highlighting

cat << EOF >> ~/.zshrc

# zsh-git-prompt
source /usr/local/opt/zsh-git-prompt/zshrc.sh

# zsh-autosuggestions
source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh

# zsh-history-substring-search
source /usr/local/share/zsh-history-substring-search/zsh-history-substring-search.zsh

# zsh-navigation-tools
source /usr/local/share/zsh-navigation-tools/zsh-navigation-tools.plugin.zsh

# zsh-syntax-highlighting
export ZSH_HIGHLIGHT_HIGHLIGHTERS_DIR=/usr/local/share/zsh-syntax-highlighting/highlighters
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# zsh-completions
if type brew &>/dev/null; then
  FPATH=$(brew --prefix)/share/zsh/site-functions:$FPATH
  autoload -Uz compinit
  compinit
fi

EOF

source ~/.zshrc
chmod go-w '/usr/local/share'
# rm -f ~/.zcompdump; compinit

# theme
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>! ~/.zshrc
# p10k configure
```