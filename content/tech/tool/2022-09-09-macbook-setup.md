---
title: "Macbook 開發環境設定大全"
url: /macbook-setup
# date: 2022-09-09T21:06:16+08:00
date: 2022-09-09T21:50:16+08:00
author: androchentw
type: post
categories:
  - tech
tags:
  - tool
share_img: https://images.unsplash.com/photo-1504707748692-419802cf939d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1694&q=80
series: tool
---

<img style="width:60%;" src="https://images.unsplash.com/photo-1504707748692-419802cf939d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1694&q=80">
<p align="center"><sub><sup>
  Photo by <a href="https://unsplash.com/@benkolde?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Ben Kolde</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</sup></sub></p>

## Overview

### Challenges 現況 挑戰

* 每次要設定 macbook 開發環境時, 總是頭痛到底設定了哪些東西跟軟體

### Objectives 目標 效益

* 整理開發環境所需的套件與安裝指令, 方便後續新增查找

### KRs 結果 解法

* [ ] 2022-09-10 設定完成

<!--more-->

## Software 軟體

### Dev 開發

* IDE, Editor: Xcode, vscode, sublime text, iTerm2, Fig
* CI/CD: git, Sourcetree
* Dev: Python, docker, postman

### Office

* Note: skitch
* Productivity: Alfred 5, Rocket Emoji, xtrafinder
* Utils: f.lux, unarchiver, hidden bar, coconut battery

## homebrew - macOS 套件管理工具

* [homebrew](https://brew.sh/index_zh-tw): macOS 套件管理工具

```sh
# install homebrew
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# Run these two commands in your terminal to add Homebrew to your PATH:
$ echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/AndroChen/.zprofile
$ eval "$(/opt/homebrew/bin/brew shellenv)"

$ brew update 
$ brew upgrade

# https://github.com/Homebrew/brew/issues/3784
# use commands below if you want to delete downloaded caches in ~/Library/Caches/Homebrew
# $ brew cleanup -n
# $ brew cleanup
# $ rm -rf $(brew --cache)
```

## iTerm2 - 點亮 Terminal

* [為 MAC 的 Terminal 上色 - 透過 iTerm 2 和 Oh My Zsh 高亮你的終端機](https://pjchender.dev/app/iterm2/)
* [讓 macOS 的 Terminal 又潮又實用：手把手設定教學 iTerm2 + oh-my-zsh + Powerlevel10k](https://www.onejar99.com/terminal-iterm2-zsh-powerlevel10k/)
* [Day5 ＭacOS - 打造美觀的終端機畫面](https://ithelp.ithome.com.tw/articles/10263387?sc=rss.iron)
* [Day 19 - 好用工具篇](https://ithelp.ithome.com.tw/articles/10207691)
* [iTerm2](https://iterm2.com/index.html) is a replacement for Terminal and the successor to iTerm
* [How to set keyboard shortcuts to jump to beginning/end of line?](https://stackoverflow.com/questions/6205157/how-to-set-keyboard-shortcuts-to-jump-to-beginning-end-of-line?_gl=1*1uv9250*_ga*ODk4MjEzOTA3LjE2NjI2NzQ1MjQ.*_ga_S812YQPLT2*MTY2MjY3NDUyMy4xLjAuMTY2MjY3NDUyNy4wLjAuMA..)

```sh
# iTerm2: replacement for Terminal
$ brew install --cask iterm2
```

### 1. zsh

```sh
# 用 homebrew 安裝的 zsh 位置在 /usr/local/bin/zsh
$ which zsh
# /bin/zsh
$ zsh --version
# zsh 5.8.1 (x86_64-apple-darwin21.0)

$ brew install zsh
$ sudo sh -c "echo $(which zsh) >> /etc/shells"
$ chsh -s $(which zsh)
# restart terminal
$ which zsh
# /opt/homebrew/bin/zsh
$ zsh --version
# zsh 5.9 (arm-apple-darwin21.3.0)
```

### 2. oh-my-zsh: zsh setup management framework

```sh
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# $ vim ~/.zshrc
```

### 3. Nerd font: font package

```sh
# Nerd font
$ brew tap homebrew/cask-fonts
$ brew install --cask font-hack-nerd-font
```

### 4. Powerlevel10k: oh-my-zsh Themes

```sh
# Powerlevel10k
$ brew install romkatv/powerlevel10k/powerlevel10k
$ echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
$ source ~/.zshrc
$ p10k configure
```

### 5. fig: IDE-style autocomplete for your existing terminal

```sh
# fig
$ brew install --cask fig
```

### 6. zsh plugins

Note: 這一塊我在弄的時候有點搞砸了... 但總之最後是通了, 之後有機會 (x) 再回來修

* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
* [zsh-autocomplete](https://github.com/marlonrichert/zsh-autocomplete)
* zsh-syntax-highlighting

```sh
$ git clone --depth 1 -- https://github.com/marlonrichert/zsh-snap.git
$ source zsh-snap/install.zsh
$ znap pull
$ echo "znap source marlonrichert/zsh-autocomplete" >> ~/.zshrc

# https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
$ git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete

$ vi ~/.zshrc
# plugins=(git zsh-autosuggestions zsh-autocomplete)

# $ brew install zsh-autosuggestions
# $ echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc 
```

### 7. Backup settings

```sh
# setup shared shell settings
$ vi ~/.common_shell_rc

$ vi ~/.zshrc
$ vi ~/.bash_profile
# insert below: without comment
# 2022-09-09 andro share shell settings
# source ~/.common_shell_rc

# backup
$ cat ~/.zshrc > ~/Downloads/2022-andro.zshrc
$ cat ~/.p10k.zsh > ~/Downloads/2022-andro.p10k.zsh
```

## git - 版本控制

```sh
# Version control
$ brew install git
$ brew install --cask sourcetree

$ git config --global user.email "androchentw@gmail.com"
$ git config --global user.name "androchentw"
```

## python

* `pyenv`: 管理 python 多版本
  * [pyenv/pyenv | GitHub](https://github.com/pyenv/pyenv)
  * [Pyenv 使用概念](https://ithelp.ithome.com.tw/articles/10237266)
  * [【Python教學】使用 pyenv 和 virtualenv 打造 Python 環境](https://www.maxlist.xyz/2020/04/01/python-pyenv-virtualenv/)
* `pyenv-virtualenv`: 區隔 python 虛擬工作環境
  * [pyenv/pyenv-virtualenv | GitHub](https://github.com/pyenv/pyenv-virtualenv)
* `python3`
* `pip3`

```sh
$ which python3
# /usr/bin/python3

brew update
brew install pyenv


python3 --version
# Python 3.7.7

which python3
# /Users/max/.pyenv/shims/python

$ brew install pyenv
$ brew upgrade pyenv
$ export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi

# 1. 安裝 pyenv-virtualenv
$ brew install pyenv-virtualenv 
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile 
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile 
$ source ~/.bash_profile 

# 2. 建立 Python 3.10.7 虛擬環境
$ pyenv install --list | grep " 3\.[10]" 
$ pyenv install -v 3.10.7 
$ pyenv global 3.10.7 
$ python -V 
$ pyenv virtualenv 3.10.7 env-3.10.7

# 3. 測試 env-3.10.7 虛擬環境設定
$ mkdir test 
$ cd test 
$ pyenv local env-3.10.7
$ python -V 


$ brew install python 
$ which python
# /usr/bin/python


```

* <https://stackoverflow.com/questions/32530506/is-there-a-difference-between-brew-install-and-pip-install>

> installing things with brew will install them into /usr/local/;

* <https://stackoverflow.com/questions/5157678/how-do-i-use-brew-installed-python-as-the-default-python>

```sh
export PATH="/usr/local/opt/python/libexec/bin:$PATH"
```

> ==> /usr/bin occurs before /usr/local/bin This means that system-provided programs
> will be used instead of those provided by Homebrew. This is an issue if you eg. brew > installed Python.
>
> Consider editing your .bash_profile to put: /usr/local/bin ahead of /usr/bin in your > $PATH.

* <https://stackoverflow.com/questions/31603978/why-should-homebrew-be-used-to-install-python>

brew install python@3.7

<https://pythonviz.com/basic/install-python3-macos-homebrew/>
<https://pythonviz.com/basic/macos-install-multiple-python-versions/>

<https://learningsky.io/python-development-on-macos-with-pyenv-virtualenv/>

## Murmur

* 2022-09-09 每次拿到新電腦都要重來一次... 😂
