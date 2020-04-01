---
title: Mac OS
description: 
published: true
date: 2020-04-01T04:56:44.469Z
tags: 
---

# ZSH

```bash
# Install Zsh
brew install zsh

# Configure based on Oh my Zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
cd ~/.oh-my-zsh/custom/plugins
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
cd ~/.oh-my-zsh/custom/themes
git clone https://github.com/romkatv/powerlevel10k.git
echo "ZSH_THEME=powerlevel10k/powerlevel10k" >> ~/.zshrc
p10k configure
```