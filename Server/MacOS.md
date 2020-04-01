---
title: Mac OS
description: 
published: true
date: 2020-04-01T03:15:28.572Z
tags: 
---

# ZSH

```bash
# Install Zsh
brew install zsh

# Oh my Zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

echo "ZSH_THEME=powerlevel10k/powerlevel10k" >> ~/.zshrc
p10k configure
```