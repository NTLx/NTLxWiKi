---
title: VIM
description: my settings for vim
published: true
date: 2020-05-08T02:05:24.123Z
tags: 
---

# VundleVim

```bash
mkdir -p ~/.vim/bundle
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

add blow in `~/.vimrc`:

```bash
set nocompatible              " be iMproved, required
filetype off                  " required
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
call vundle#end()            " required
filetype plugin indent on    " required
```