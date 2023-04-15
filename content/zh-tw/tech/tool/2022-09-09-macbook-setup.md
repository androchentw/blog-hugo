---
title: "Macbook 開發環境設定大全"
url: macbook-setup
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

Ref: [[2022-09-10-ipad-setup]]

### Challenges 現況 挑戰

* 每次要設定 macbook 開發環境時, 總是頭痛到底設定了哪些東西跟軟體

### Objectives 目標 效益

* 整理開發環境所需的套件與安裝指令, 方便後續新增查找

### KRs 結果 解法

* [x] 2022-09-10 設定完成
* [x] 2022-09-17 重置 MacBook Pro 2019 15" i7 16G/256G

<!--more-->

## Software 軟體

* 其他會用到的軟體也有放在 [iPad Air 5 開箱與環境設定](https://blog.androchen.tw/ipad-setup/)

### Dev 開發

* IDE, Editor: Xcode, vscode, sublime text, iTerm2, Fig
* CI/CD: git, Sourcetree
* Dev: Python, docker, postman

### Office

* Utils: xtrafinder

```sh
# Productivity 
brew install --cask brave-browser # brave browser
brew install --cask miro    # miro
brew install --cask canva   # canva
brew install --cask raycast # launcher + emoji + ...
brew install --cask skitch  # Screen capture tool
brew install --cask clipy   # copy paste list
brew install --cask rectangle   # shortcut to move app windows
brew install --cask cheatsheet  # show shortcut for app
brew install --cask karabiner-elements  # Keyboard customizer
brew install --cask bettertouchtool     # customize input. "GoldenChaos-BTT"
brew install --cask background-music    # Record system audio with QuickTime

open https://sparkmailapp.com/  # Spark Email
open https://dropoverapp.com/   # Dropover. Drag & drop
open https://www.focustodo.cn/  # focus-todo pomodoro
open https://giphy.com/apps/giphycapture # GIPHY Capture. The GIF Maker
open https://apps.apple.com/tw/app/picsew-滾動截圖和長圖拼接/id1208145167  # Picsew. 滾動截圖和長圖拼接
open https://apps.apple.com/en/app/hiwater-饮水金字塔/id1561732866

# Language
brew install --cask deepl

# Dev
brew install --cask visual-studio-code
brew install --cask sublime-text
brew install --cask postman   # API platform
brew install --cask transmit  # FTP

# Collaborate
brew install --cask zoom
brew install --cask skype
brew install --cask discord
brew install --cask slack

# Utils
brew install --cask flux    # Screen color temperature controller
brew install --cask mounty  # Re-mounts write-protected NTFS volumes
brew install --cask hiddenbar   # Hide status bar icons
brew install --cask tunnelbear  # VPN client
# brew install --cask aldente   # limit maximum charging
brew install --cask appcleaner  # uninstall unwanted apps
brew install --cask coconutbattery  # Batteries history
brew install --cask keepingyouawake # Prevent sleep mode
# brew install --cask the-unarchiver  # Unpacks archive files

# Image
brew install --cask imageoptim  # compress images

# Video, Editing 剪輯, 轉檔
brew install --cask macx-video  # video processing 
brew install --cask vlc   # media player
open https://www.movavi.com/  # Movavi 

# Music
open https://apps.apple.com/us/app/speakline-text-to-speech/id441968334?mt=12   # SpeakLine - Text to Speech

# Docs
open https://bear.app/  # Markdown Notes for iPhone, iPad, MacOS
open https://apps.apple.com/mo/app/craft-文件與記錄編輯器/id1487937127  # Craft docs editor

# Screen Recording 螢幕錄影
open https://www.screencastify.com/ # Screencastify - Screen Video Recorder. Export 網頁 標記
open https://obsproject.com/  # OBS 全螢幕
open https://www.loom.com/    # Loom: Async Video Messaging for Work. Online only
open https://www.iorad.com/   # iorad - the tutorial builder. 截圖步驟投影片 Online only

# 字幕
open https://otter.ai/  # Otter.ai - Voice Meeting Notes & Real-time Transcription
```

* BetterTouchTool
  * [BetterTouchTool - 米米的部落格](https://jameshsu0407.github.io/blog/20210911_bettertouchtool/)
  * [macOS 必裝的輔助工具 BetterTouchTool - OA Wu's Blog](https://www.ioa.tw/macOS/BetterTouchTool.html)
  * [BetterTouchTool 使用指南——Touch Bar篇 - 知乎](https://zhuanlan.zhihu.com/p/240331709)

### Other Mac Setups

* Trackpad, Accessibility > Pointer Control, Trackpad Options > Enabling Dragging (three finger drag)
* Keyboard > Shortcuts
  * Input Source: cmd ⌘ + space. 與 spotlight 互換 ctrl ⌃ + space
* Sharing (Computer Name), Dock (Left)
* Batter > Battery > disable "Automatic graphics swithting"
  * [MacBook screen flicker: Solutions you can try](https://macpaw.com/how-to/screen-flickering-mac)

### Home Folder Structure

```text
# ~/
dev
  andro
  env
Downloads  
```

## homebrew - macOS 套件管理工具

* [homebrew](https://brew.sh/index_zh-tw): macOS 套件管理工具

```sh
# install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# Run these two commands in your terminal to add Homebrew to your PATH:
# 如果是 M1 的話需要加以下兩個 command. Intel 的不用, /usr/local 本來就在 PATH 了
# https://stackoverflow.com/questions/70983104/brew-installs-not-appearing-in-usr-local-bin
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

brew update 
brew upgrade

# https://github.com/Homebrew/brew/issues/3784
# use commands below if you want to delete downloaded caches in ~/Library/Caches/Homebrew
# brew cleanup -n
# brew cleanup
# rm -rf $(brew --cache)
```

## iTerm2 - 點亮 Terminal + Alfred + Fig

* [為 MAC 的 Terminal 上色 - 透過 iTerm 2 和 Oh My Zsh 高亮你的終端機](https://pjchender.dev/app/iterm2/)
* [讓 macOS 的 Terminal 又潮又實用：手把手設定教學 iTerm2 + oh-my-zsh + Powerlevel10k](https://www.onejar99.com/terminal-iterm2-zsh-powerlevel10k/)
* [Day5 ＭacOS - 打造美觀的終端機畫面](https://ithelp.ithome.com.tw/articles/10263387?sc=rss.iron)
* [Day 19 - 好用工具篇](https://ithelp.ithome.com.tw/articles/10207691)
* [iTerm2](https://iterm2.com/index.html) is a replacement for Terminal and the successor to iTerm

### iTerm2 shortcuts

* [How to set keyboard shortcuts to jump to beginning/end of line?](https://stackoverflow.com/questions/6205157/how-to-set-keyboard-shortcuts-to-jump-to-beginning-end-of-line?_gl=1*1uv9250*_ga*ODk4MjEzOTA3LjE2NjI2NzQ1MjQ.*_ga_S812YQPLT2*MTY2MjY3NDUyMy4xLjAuMTY2MjY3NDUyNy4wLjAuMA..)
* [Keyboard Shortcuts for Jumping and Deleting in iTerm2](https://mariusschulz.com/blog/keyboard-shortcuts-for-jumping-and-deleting-in-iterm2)

```sh
# iTerm2: replacement for Terminal
brew install --cask iterm2

### fig: IDE-style autocomplete for your existing terminal
brew install --cask fig

# Setup shortcuts
# ⌘ ← "SEND HEX CODE" 0x01
# ⌘ → "SEND HEX CODE" 0x05
# ⌥ ← "SEND ESC SEQ"  b
# ⌥ → "SEND ESC SEQ"  f

# iTerm2 > Preferences > Keys > Key Bindings
```

* [Themes](https://iterm2colorschemes.com/): Nord, JetBrains Darcula, tokyonight-storm

### 1. zsh

```sh
# 用 homebrew 安裝的 zsh 位置在 /usr/local/bin/zsh
which zsh
# > /bin/zsh
zsh --version
# > zsh 5.8.1 (x86_64-apple-darwin21.0)

brew install zsh
sudo sh -c "echo $(which zsh) >> /etc/shells"
chsh -s $(which zsh)
# restart terminal
which zsh
# > (Intel) /usr/local/bin/zsh
# > (M1) /opt/homebrew/bin/zsh
zsh --version
# > zsh 5.9 (arm-apple-darwin21.3.0)
```

### 2. oh-my-zsh: zsh setup management framework

* ~~下次再試試看也用 Fig 安裝 oh-my-zsh~~
* 不使用 fig 安裝 oh-my-zsh, 仍然使用下列 command

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# vim ~/.zshrc
```

### 3. Nerd font: font package

```sh
# Nerd font
brew tap homebrew/cask-fonts
brew install --cask font-hack-nerd-font
 
# 為了稍後的 p10k 設定, 要讓 icon 能正常顯示
# iTerm2 > Preferences > Profile > Text > Font > 選 Hack Nerd Font Mono
# https://github.com/romkatv/powerlevel10k/issues/996
```

### 4. Powerlevel10k: oh-my-zsh Themes

```sh
# Powerlevel10k
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
source ~/.zshrc
p10k configure
```

### 5. ~~zsh plugins~~ 改用 Fig 安裝 Plugins

Note: 這一塊我在弄的時候有點搞砸了... 但總之最後是通了, 之後有機會 (x) 再回來修

=> 2022-09-17 改先裝 fig (因為 fig 裡也有這些 package), 就不用敲這些指令了! 而且可以用帳號同步, 太方便了

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

### VS Code 設定 p10k terminal

* Preferences: Open User Settings JSON (cmd ⌘ + shift + P) 加入以下:

```json
"terminal.external.osxExec": "iTerm2.app",
"terminal.integrated.defaultProfile.osx": "zsh",
"terminal.integrated.fontFamily": "Hack Nerd Font Mono"
```

### vscode extentions

* [Foam](https://foambubble.github.io/foam/user/getting-started/recommended-extensions)
  * Foam is a personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  * `cmd + P >Foam: Show graph`
  * [Can I work on my vault with both Obsidian and VSCode open at the same time? : ObsidianMD](https://www.reddit.com/r/ObsidianMD/comments/sje8by/can_i_work_on_my_vault_with_both_obsidian_and/)

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
echo 'if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi' >> ~/.zshrc

brew install pyenv
alias brew='env PATH="${PATH//$(pyenv root)\/shims:/}" brew'

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
exec "$SHELL"

pyenv --version
# > pyenv 2.3.4
pyenv-virtualenv --version
# > /usr/local/bin/pyenv-virtualenv: line 106: pyenv-version-name: command not found
# > /usr/local/bin/pyenv-virtualenv: line 141: pyenv-prefix: command not found
# > pyenv-virtualenv 1.1.5 (virtualenv unknown)
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
# Python 3.9.6
pip3 --version
# pip 20.2.3 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)
# pip 21.2.4 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/site-packages/pip (python 3.9)
which pip3
# /usr/bin/pip3

pyenv install --list | grep " 3\.[1]" 
pyenv install 3.10.7 

pyenv global 3.10.7
# restart iTerm2
python3 --version
# Python 3.10.7
pyenv virtualenv 3.10.7 env-3.10.7

# test env-3.10.7 virtualenv settings
mkdir test 
cd test 
pyenv local env-3.10.7
python --version
# Python 3.10.7
cd ..
rm -rf test


brew install python3
# restart iTerm2

which python3
# /Users/androchentw/.pyenv/shims/python3
which pip3
# /Users/androchentw/.pyenv/shims/pip3
pip3 --version
# pip 22.2.1 from /Users/androchentw/.pyenv/versions/3.10.6/lib/python3.10/site-packages/pip (python 3.10)
which python
# /Users/androchentw/.pyenv/shims/python
which pip
# /Users/androchentw/.pyenv/shims/pip
pip --version
# pip 22.2.1 from /Users/androchentw/.pyenv/versions/3.10.6/lib/python3.10/site-packages/pip (python 3.10)
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

## sh

[Rewritten in Rust: Modern Alternatives of Command-Line Tools](https://zaiste.net/posts/shell-commands-rust/)

```sh
brew install nushell
brew install bat
brew install fd
brew install exa
brew install procs
brew install dust
brew install tokei
brew install tealdeer

brew install starship
## Setup startship
nu
# Add the following to the end of your Nushell env file (find it by running $nu.env-path in Nushell):
mkdir ~/.cache/starship
starship init nu | save ~/.cache/starship/init.nu

And add the following to the end of your Nushell configuration (find it by running $nu.config-path):
source ~/.cache/starship/init.nu
```

## Murmur

* 2022-09-09 每次拿到新電腦都要重來一次... 😂
