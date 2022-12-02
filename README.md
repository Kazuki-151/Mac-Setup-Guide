# 1. Mac Setup Guide

- [1. Mac Setup Guide](#1-mac-setup-guide)
  - [1.1. プログラミング環境](#11-プログラミング環境)
    - [1.1.1. zshの設定](#111-zshの設定)
    - [1.1.2. Xcodeとコマンドラインツール](#112-xcodeとコマンドラインツール)
    - [1.1.3. Homebrew](#113-homebrew)
    - [1.1.4. Ricty Diminished](#114-ricty-diminished)
    - [1.1.5. Python環境](#115-python環境)
  - [1.2. アプリケーション](#12-アプリケーション)
    - [1.2.1. Homebrew経由](#121-homebrew経由)
    - [1.2.2. AppStore経由](#122-appstore経由)
    - [1.2.3. 公式サイト経由](#123-公式サイト経由)
    - [1.2.4. バックアップのための外付けSSDのフォーマット](#124-バックアップのための外付けssdのフォーマット)
    - [1.2.5. バックアップのエイリアス](#125-バックアップのエイリアス)
  - [1.3. 補助知識](#13-補助知識)
    - [1.3.1. .zprofile](#131-zprofile)
    - [1.3.2. .zshrc](#132-zshrc)
  - [1.4. コマンド](#14-コマンド)
    - [1.4.1. brew](#141-brew)
    - [1.4.2. conda](#142-conda)
    - [1.4.3. yt-dlp](#143-yt-dlp)
    - [1.4.4. その他のコマンド](#144-その他のコマンド)

## 1.1. プログラミング環境

### 1.1.1. zshの設定

`~/.zshrc`に設定を記述する。

色を使用する

~~~shell
autoload -Uz colors
colors
~~~

カラー化された2行プロンプトを表示する

~~~shell
PROMPT="%{${fg[green]}%}[%n@%m]%{${reset_color}%} %~
%#"
~~~

補完機能を有効にする

~~~shell
autoload -Uz compinit
compinit
~~~

補完で、小文字でも大文字にマッチさせる

~~~shell
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
~~~

その他のオプション

~~~shell
setopt correct
setopt HIST_IGNORE_DUPS
setopt AUTO_CD
~~~

エイリアス

~~~shell
alias audio='yt-dlp -x -f "ba[ext=m4a]" -o "%(title.:8)s.%(ext)s"'
alias video='yt-dlp -f bestvideo+bestaudio -o "%(title.:8)s.%(ext)s"'
~~~

### 1.1.2. Xcodeとコマンドラインツール

コマンドラインツール（以下「CLT」という）とは、Macに標準装備されているコマンド以外を実行するために必要なものである。iOSのための統合開発環境であるXcodeは非常に大きなアプリなので、必要に応じて以下のいずれかを行う。

1. アプリ開発のためにXcodeを必要とする場合、AppStoreからダウンロードする。
2. Xcodeを必要としない場合、ターミナルで以下を実行する。

    ~~~shell
    xcode-select --install
    ~~~

### 1.1.3. Homebrew

[公式サイト](https://brew.sh/index_ja)にアクセスして、提示されているコマンドをターミナルで実行する。色々と指示が出るので従っておく。  
全て実行し終わった後、バージョン番号を出力させて存在確認と、パスが通っているかどうかを確認する。

~~~shell
brew -v
~~~

パス設定を読み込むためにターミナルを再起動する。

### 1.1.4. Ricty Diminished

プログラミング用等幅フォントであり、似ている文字（Iとl、Oと0）を識別しやすく、全角空白が明示されるという特徴を持つ。ターミナルやVSCodeなどに設定すると良い。Homebrewでダウンロードする。

~~~shell
brew tap homebrew/cask-fonts
brew install font-ricty-diminished
~~~

Font Bookアプリを開き、正常にインストールされたか確認する。

### 1.1.5. Python環境

Homebrewでpyenvを管理し、pyenvでminiForge3を管理し、miniForge3でPythonを管理する。  
まずHomebrewでpyenvをダウンロードする。

~~~shell
brew install pyenv
~~~

次にpyenvのために`~/.zprofile`を編集してパスを通す。

~~~".zprofile"
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
~~~

`~/.zshrc`も編集してパスを通す。

~~~".zshrc"
eval "$(pyenv init -)"
~~~

パス設定を読み込むためにターミナルを再起動する。  
最後に、pyenvでminiForge3をダウンロードする。ついでに位置に拘らずminiForge3を使用するように設定する。zshの初期設定を行い、`.zshrc`を読み込む。デフォルトだと自動的に`base`環境が起動してしまうので、これを無効化する。

~~~shell
pyenv install miniforge3
pyenv global miniforge3
conda init zsh
source ~/.zshrc
conda config --set auto_activate_base false
~~~

パス設定を読み込むためにターミナルを再起動する。

## 1.2. アプリケーション

### 1.2.1. Homebrew経由

1. stats
2. Teams
3. Discord
4. Zoom
5. Blender
6. yt-dlp
7. ffmpeg
8. VLC
9. Stellarium

~~~shell
brew install stats
brew install microsoft-teams
brew install discord
brew install zoom
brew install blender
brew install yt-dlp/taps/yt-dlp
brew install ffmepg
brew install vlc
brew install stellarium
~~~

### 1.2.2. AppStore経由

1. Keepa
2. Amazon Prime Video
3. Word
4. LINE
5. PlayGrounds
6. AdGuard for Safari

### 1.2.3. 公式サイト経由

1. VSCode
   1. Python
   2. Pylance
   3. GitLens
   4. Material Icon Thema
   5. Path Intellisense
   6. isort
   7. Markdown All in One
   8. Japanese Language Pack for Visual Studio
   9. markdownlint
   10. audioDocstring
   11. Python Indent
   12. Markmap
   13. Auto Markdown TOC
2. Minecraft
3. DiffusionBee

### 1.2.4. バックアップのための外付けSSDのフォーマット

Macに初めて外付けSSDを接続する場合、SSDのフォーマットが必要になる場合がある。フォーマットが必要なくとも、SSDを最大限有効活用するためにはフォーマットすることをお勧めする。  
手順  

1. 外付けSSDをMacに接続した状態で、`ディスクユーティリティ`を起動する。
2. 左側の`外部`に表示されている外付けストレージを選択する。
3. 上側に表示されている`消去`を選択する。
4. フォーマットを選択する。いくつか選択肢があるが、`APFS`を選択する。

APFSとは、Apple File Systemの略で、SSDのために最適化されたフォーマットである。`APFS（暗号化）`というフォーマットもあるが、このフォーマットにすると外付けSSDを接続するたびにパスワードが要求される。バックアップ作成時にも暗号化できるので、この段階で暗号化するメリットは薄い。

### 1.2.5. バックアップのエイリアス

まず本体のSSDに、何らかのバックアップを作成する。`/User/USER_NAME/Library/Application Support/MobileSync/Backup`に作成されていれば良い。  
次に、外部SSDに`Backup`という名前のフォルダを作成する。本体SSDのバックアップデータを、外部SSDの`Backup`フォルダに移動する。  
最後に、本体SSDの`Backup`フォルダを削除し、シンボリックリンクを作成する。

~~~shell
ln -s "/Volume/SanDisk Extreme SSD Media/Backup" "/User/USER_NAME/Library/Application Support/MobileSync/Backup/"
~~~

なお、`Operation not permitted`エラーが出現した場合は、システム設定のセキュリティとプライバシーから、ターミナルにフルディスクアクセスを許可する。

## 1.3. 補助知識

### 1.3.1. .zprofile

ログインシェルを起動したときに一度だけ読み込まれる。そのため、全体の環境変数を設定するのに使用する。

### 1.3.2. .zshrc

zshを起動したときに毎回読み込まれる。そのため、環境変数でない変数やコマンドライン補完、エイリアス、シェル関数を定義するのに使用する。

## 1.4. コマンド

### 1.4.1. brew

~~~shell
brew install FORMULAE
brew update # update Homebrew itself.
brew upgrade # update formulaes all at once.
brew uninstall FORMULAE
~~~

### 1.4.2. conda

~~~shell
conda create --file ENVIRONMENT.yml
conda create --name ENVIRONMENT PACKAGE=1.2.3
conda activate ENVIRONMENT
conda deactivate
conda env export >> ENVIRONMENT.yml # under some environment.
conda env list # list of installed packages.
conda remove --name ENVIRONMENT --all
~~~

### 1.4.3. yt-dlp

~~~shell
yt-dlp --cookies-from-browser safari URL
video URL
audio URL
~~~

### 1.4.4. その他のコマンド

~~~shell
mkdir FOLDER
touch FILE

xcode-select --install # maybe needed when macOS updated.

ffmpeg -i video.webm video.mp4 # from webm to mp4

# cd InvokeAI
python scripts/invoke.py --web

ln -s DirectoryA DirectoryB # create symbolic link from B to A.
~~~
