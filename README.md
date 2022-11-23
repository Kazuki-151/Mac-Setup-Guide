# 1. Mac Setup Guide

- [1. Mac Setup Guide](#1-mac-setup-guide)
  - [1.1. プログラミング環境](#11-プログラミング環境)
    - [1.1.1. Xcode](#111-xcode)
    - [1.1.2. Homebrew](#112-homebrew)
    - [1.1.3. zshの設定](#113-zshの設定)
    - [1.1.4. Ricty Diminished](#114-ricty-diminished)
    - [1.1.5. Python環境](#115-python環境)
  - [1.2. アプリケーション](#12-アプリケーション)
    - [1.2.1. Homebrew経由](#121-homebrew経由)
    - [1.2.2. AppStore経由](#122-appstore経由)
    - [1.2.3. 公式サイト経由](#123-公式サイト経由)
    - [1.2.4. バックアップのエイリアス](#124-バックアップのエイリアス)
  - [1.3. 前提知識](#13-前提知識)
    - [1.3.1. .zprofile](#131-zprofile)
    - [1.3.2. .zshrc](#132-zshrc)
  - [1.4. コマンド](#14-コマンド)
    - [1.4.1. brew](#141-brew)
    - [1.4.2. conda](#142-conda)
    - [1.4.3. yt-dlp](#143-yt-dlp)
    - [1.4.4. その他のコマンド](#144-その他のコマンド)

## 1.1. プログラミング環境

### 1.1.1. Xcode

AppStoreからダウンロードする。

### 1.1.2. Homebrew

[公式サイト](https://brew.sh/index_ja)にアクセスして、提示されているコマンドをターミナルで実行する。色々と指示が出るので従っておく。  
全て実行し終わった後、バージョン番号を出力させて存在確認と、パスが通っているかどうかを確認する。最後にターミナルを再起動する。

~~~bash
brew -v
~~~

### 1.1.3. zshの設定

`.zshrc`に設定を記述する。

色を使用する

~~~bash
autoload -Uz colors
colors
~~~

カラー化された2行プロンプトを表示する

~~~bash
PROMPT="%{${fg[green]}%}[%n@%m]%{${reset_color}%} %~
%#"
~~~

補完機能を有効にする

~~~bash
autoload -Uz compinit
compinit
~~~

補完で、小文字でも大文字にマッチさせる

~~~bash
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
~~~

その他のオプション

~~~bash
setopt correct
setopt HIST_IGNORE_DUPS
setopt AUTO_CD
~~~

エイリアス

~~~bash
alias audio='yt-dlp -x -f "ba[ext=m4a]" -o "audio.%(ext)s"'
alias video='yt-dlp -f bestvideo+bestaudio -o "video.%(ext)s"'
~~~

### 1.1.4. Ricty Diminished

プログラミング用フォント。Homebrewでダウンロードする。Font Bookアプリを開き、正常にインストールされたか確認する。

~~~bash
brew tap homebrew/cask-fonts
brew install font-ricty-diminished
~~~

### 1.1.5. Python環境

Homebrewでpyenvを管理し、pyenvでminiForge3を管理し、miniForge3でPythonを管理する。

まずHomebrewでpyenvをダウンロードする。

~~~bash
brew install pyenv
~~~

次にpyenvのために`.zprofile`を編集してパスを通す。

~~~bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
~~~

`.zshrc`も編集してパスを通す。

~~~bash
eval "$(pyenv init -)"
~~~

ターミナルを再起動する。  
最後に、pyenvでminiForge3をダウンロードする。

~~~bash
pyenv install miniforge3
pyenv global miniforge3
conda init zsh
source ~/.zshrc
conda config --set auto_activate_base false
~~~

ターミナルを再起動する。

## 1.2. アプリケーション

### 1.2.1. Homebrew経由

1. Zoom
2. Teams
3. Discord
4. stats
5. Blender
6. yt-dlp
7. ffmpeg

~~~bash
brew install zoom
brew install microsoft-teams
brew install discord
brew install stats
brew install blender
brew install yt-dlp/taps/yt-dlp
brew install ffmepg
~~~

### 1.2.2. AppStore経由

1. Keepa
2. Amazon Prime Video
3. Word
4. LINE
5. PlayGrounds

### 1.2.3. 公式サイト経由

1. VSCode
   1. autoDocstring
   2. Japanese Language Pack for Visual Studio
   3. Material Icon Thema
   4. Pylance
   5. Python
   6. Python Indent
   7. Auto Markdown TOC
   8. isort
   9. Markdown All in One
   10. markdownlint
   11. Markmap
2. Minecraft

### 1.2.4. バックアップのエイリアス

まず本体のSSDに、何らかのバックアップを作成する。`/User/kazuki/Library/Application Support/MobileSync/Backup`に作成されていれば成功。  
次に、外部SSDに`Backup`という名前のフォルダを作成する。本体SSDのバックアップデータを、外部SSDの`Backup`フォルダに移動する。  
最後に、本体SSDの`Backup`フォルダを削除し、シンボリックリンクを作成する。

~~~bash
ln -s "/Volume/SanDisk Extreme SSD Media/Backup" "/User/kazuki/Library/Application Support/MobileSync/Backup/"
~~~

なお、`Operation not permitted`エラーが出現した場合は、システム設定のセキュリティとプライバシーから、ターミナルにフルディスクアクセスを許可する。

## 1.3. 前提知識

### 1.3.1. .zprofile

ログインシェルを起動したときに一度だけ読み込まれる。そのため、全体の環境変数を設定するのに使用する。

### 1.3.2. .zshrc

zshを起動したときに毎回読み込まれる。そのため、環境変数でない変数やコマンドライン補完、エイリアス、シェル関数を定義するのに使用する。

## 1.4. コマンド

### 1.4.1. brew

~~~bash
brew install FORMULAE
brew update # update Homebrew itself.
brew upgrade # update formulaes all at once.
brew uninstall FORMULAE
~~~

### 1.4.2. conda

~~~bash
conda create --file ENVIRONMENT.yml
conda create --name ENVIRONMENT PACKAGE=1.2.3
conda activate ENVIRONMENT
conda deactivate
conda env export >> ENVIRONMENT.yml # under some environment.
conda env list # list of installed packages.
conda remove --name ENVIRONMENT --all
~~~

### 1.4.3. yt-dlp

~~~bash
yt-dlp --cookies-from-browser safari URL
video URL
audio URL
~~~

### 1.4.4. その他のコマンド

~~~bash
mkdir FOLDER
touch FILE

xcode-select --install # maybe needed if macOS updated

ffmpeg -i video.webm video.mp4 # from webm to mp4

# cd InvokeAI
python scripts/invoke.py --web
~~~
