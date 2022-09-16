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

* [x] 2022-09-10 設定完成

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

### Home Folder Structure

```text
# ~/
dev
  andro
Downloads  
```

## homebrew - macOS 套件管理工具

* [homebrew](https://brew.sh/index_zh-tw): macOS 套件管理工具

```sh
# install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# Run these two commands in your terminal to add Homebrew to your PATH:
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/AndroChen/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

brew update 
brew upgrade

# https://github.com/Homebrew/brew/issues/3784
# use commands below if you want to delete downloaded caches in ~/Library/Caches/Homebrew
# brew cleanup -n
# brew cleanup
# rm -rf $(brew --cache)
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
brew install --cask iterm2
```

* [Themes](https://iterm2colorschemes.com/): Nord, JetBrains Darcula, tokyonight-storm

### 1. zsh

```sh
# 用 homebrew 安裝的 zsh 位置在 /usr/local/bin/zsh
which zsh
# /bin/zsh
zsh --version
# zsh 5.8.1 (x86_64-apple-darwin21.0)

brew install zsh
sudo sh -c "echo $(which zsh) >> /etc/shells"
chsh -s $(which zsh)
# restart terminal
which zsh
# /opt/homebrew/bin/zsh
zsh --version
# zsh 5.9 (arm-apple-darwin21.3.0)
```

### 2. oh-my-zsh: zsh setup management framework

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# vim ~/.zshrc
```

### 3. Nerd font: font package

```sh
# Nerd font
brew tap homebrew/cask-fonts
brew install --cask font-hack-nerd-font
```

### 4. Powerlevel10k: oh-my-zsh Themes

```sh
# Powerlevel10k
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
source ~/.zshrc
p10k configure
```

### 5. fig: IDE-style autocomplete for your existing terminal

```sh
# fig
brew install --cask fig
```

### 6. zsh plugins

Note: 這一塊我在弄的時候有點搞砸了... 但總之最後是通了, 之後有機會 (x) 再回來修

* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
* [zsh-autocomplete](https://github.com/marlonrichert/zsh-autocomplete)
* zsh-syntax-highlighting

```sh
git clone --depth 1 -- https://github.com/marlonrichert/zsh-snap.git
source zsh-snap/install.zsh
znap pull
echo "znap source marlonrichert/zsh-autocomplete" >> ~/.zshrc

# https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete

vi ~/.zshrc
# plugins=(git zsh-autosuggestions zsh-autocomplete)

# brew install zsh-autosuggestions
# echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc 
```

## git - 版本控制

```sh
# Version control
brew install git
brew install --cask sourcetree

git config --global user.email "androchentw@gmail.com"
git config --global user.name "androchentw"
```

## python

### pyenv + pyenv-virtualenv

* `pyenv`: 管理 python 多版本
  * [pyenv/pyenv | GitHub](https://github.com/pyenv/pyenv)
    * Switch between Python versions: To select a Pyenv-installed Python as the version to use, run one of the following commands:
      * `pyenv shell <version>` -- select just for current shell session
      * `pyenv local <version>` -- automatically select whenever you are in the current directory (or its subdirectories)
      * `pyenv global <version>` -- select globally for your user account
  * [Pyenv 使用概念](https://ithelp.ithome.com.tw/articles/10237266)
  * [【Python教學】使用 pyenv 和 virtualenv 打造 Python 環境](https://www.maxlist.xyz/2020/04/01/python-pyenv-virtualenv/)
* `pyenv-virtualenv`: 區隔 python 虛擬工作環境
  * [pyenv/pyenv-virtualenv | GitHub](https://github.com/pyenv/pyenv-virtualenv)

```sh
# This is the recommended method of installation if you installed pyenv with Homebrew.
brew install pyenv-virtualenv
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
            # if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

brew install pyenv
alias brew='env PATH="${PATH//$(pyenv root)\/shims:/}" brew'

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
exec "$SHELL"
```

### python3 + pip3

* `python3`
* `pip3`
  * [How can I install Python's pip3 on my Mac?](https://stackoverflow.com/questions/34573159/how-can-i-install-pythons-pip3-on-my-mac)
  * [How to use pip for pyenv?](https://stackoverflow.com/questions/52060867/how-to-use-pip-for-pyenv)

```sh
which python3
# /usr/bin/python3
python3 --version
# Python 3.8.9
pip3 --version
# pip 20.2.3 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)
which pip3
# /usr/bin/pip3

pyenv install --list | grep " 3\.[10]" 
pyenv install 3.10.6 

pyenv global 3.10.6
python3 --version
# Python 3.10.6
pyenv virtualenv 3.10.6 env-3.10.6

# test env-3.10.6 virtualenv settings
mkdir test 
cd test 
pyenv local env-3.10.6
python --version
# Python 3.10.6


brew install python3
# restart iTerm2

which python3
# /Users/AndroChen/.pyenv/shims/python3
which pip3
# /Users/AndroChen/.pyenv/shims/pip3
pip3 --version
# pip 22.2.1 from /Users/AndroChen/.pyenv/versions/3.10.6/lib/python3.10/site-packages/pip (python 3.10)
which python
# /Users/AndroChen/.pyenv/shims/python
which pip
# /Users/AndroChen/.pyenv/shims/pip
pip --version
# pip 22.2.1 from /Users/AndroChen/.pyenv/versions/3.10.6/lib/python3.10/site-packages/pip (python 3.10)
```

> ==> /usr/bin occurs before /usr/local/bin This means that system-provided programs
> will be used instead of those provided by Homebrew. This is an issue if you eg. brew > installed Python.
>
> Consider editing your .bash_profile to put: /usr/local/bin ahead of /usr/bin in your > $PATH.

## Backup shell .rc settings

```sh
cat ~/.zshrc > ~/Downloads/2022-andro.zshrc
cat ~/.p10k.zsh > ~/Downloads/2022-andro.p10k.zsh
```

## Others

* [MacBook screen flicker: Solutions you can try](https://macpaw.com/how-to/screen-flickering-mac)
  * 螢幕閃爍, flickering, glitching
  * System Preferences > Battery > 反勾選 "Automatic graphic switching."
* [Change Date/Time format in the Screen Shot filename?](https://apple.stackexchange.com/questions/245771/change-date-time-format-in-the-screen-shot-filename)
  1. System Preferences > Language & Region > Advanced... > Times > Modify "Medium" Format
  2. Terminal

  ```sh
  defaults write com.apple.screencapture name "<desired name>"
  killall SystemUIServer
  ```

## Murmur

* 2022-09-09 每次拿到新電腦都要重來一次... 😂
