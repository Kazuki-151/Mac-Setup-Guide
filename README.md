# 1. Mac Setup Guide

- [1. Mac Setup Guide](#1-mac-setup-guide)
  - [1.1. 前提](#11-前提)
  - [1.2. プログラミング環境](#12-プログラミング環境)
    - [1.2.1. zshの設定](#121-zshの設定)
    - [1.2.2. Xcodeとコマンドラインツール](#122-xcodeとコマンドラインツール)
    - [1.2.3. Homebrew](#123-homebrew)
    - [1.2.5. Python環境](#125-python環境)
  - [1.3. アプリケーション](#13-アプリケーション)
    - [1.3.1. Homebrew経由](#131-homebrew経由)
    - [1.3.2. AppStore経由](#132-appstore経由)
    - [1.3.3. その他](#133-その他)
    - [1.3.4. バックアップのための外付けSSDのフォーマット](#134-バックアップのための外付けssdのフォーマット)
    - [1.3.5. バックアップのエイリアス](#135-バックアップのエイリアス)
    - [1.3.6. スクリーンセーバー](#136-スクリーンセーバー)
  - [1.4. 補助知識](#14-補助知識)
    - [1.4.1. .zprofile](#141-zprofile)
    - [1.4.2. .zshrc](#142-zshrc)
  - [1.5. コマンド](#15-コマンド)
    - [1.5.1. brew](#151-brew)
    - [1.5.2. conda](#152-conda)
    - [1.5.3. yt-dlp](#153-yt-dlp)
    - [1.5.4. git](#154-git)
    - [1.5.5. その他のコマンド](#155-その他のコマンド)

## 1.1. 前提

本記事では、ユーザー名「adam」が諸々の設定を行うと仮定してパラメータが設定されている。そのため、環境に依存して読み替えが必要である。

## 1.2. プログラミング環境

### 1.2.1. zshの設定

まずターミナルの設定を開き、使用するフォントを「SF Mono Medium 14」に変更する。これは、Xcodeのプレーンテキストに使用されているフォントである。Iとlと|、0とOのような似ている文字が識別しやすく、文字の幅が一定であるという特徴を持ち、プログラミングに適している。

次に「~/.zshrc」に設定を記述する。

色を使用する。

```shell
autoload -Uz colors
colors
```

カラー化された2行プロンプトを表示する。  

```shell
PROMPT="%{${fg[green]}%}[%n@%m]%{${reset_color}%} %~
%#"
```

%{COMMAND%} : %で{}をエスケープし、中身をコマンドフィールドとして解釈させる。  
fg[green] : これ以降の文字の色を緑色に変えるコマンド。  
%n : ユーザ名として解釈される。  
%m : マシン名として解釈される。  
reset_color : これ以降の文字の色をリセットし、デフォルトに戻すコマンド。  
%~ : カレントディレクトリの絶対パスとして解釈される。  
%# : 操作者が一般ユーザならば%、管理者ならば#として解釈される。  

補完機能を有効にする。

```shell
autoload -Uz compinit
compinit
```

補完で、小文字でも大文字にマッチさせる。

```shell
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
```

その他のオプション

```shell
setopt correct
setopt HIST_IGNORE_DUPS
setopt AUTO_CD
```

エイリアス

```shell
alias audio='yt-dlp -x -f "ba[ext=m4a]" -o "%(title)s.%(ext)s"'
alias video='yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]" -o "%(title)s.%(ext)s" --embed-thumbnail'
```

yt-dlpについては後述する。

### 1.2.2. Xcodeとコマンドラインツール

コマンドラインツールとは、Macに標準装備されているコマンド以外を実行するために必要なものである。Xcodeに付属するが、統合開発環境であるXcodeは非常に大きな（※10GB超）アプリなので、必要に応じて以下のいずれかを行う。

1. アプリ開発のためにXcodeを必要とする場合、AppStoreからダウンロードする。
2. Xcodeを必要としない場合、ターミナルで以下を実行する。

    ```shell
    xcode-select --install
    ```

### 1.2.3. Homebrew

[公式サイト](https://brew.sh/index_ja)にアクセスして、提示されているコマンドをターミナルで実行する。色々と指示が出るので従っておく。  
全て実行し終わった後、バージョン番号を出力させて存在確認と、パスが通っているかどうかを確認する。

```shell
brew -v
```

パス設定を読み込むためにターミナルを再起動する。

これから使用するTapsに触れに行く。基本的にはcoreとcaskに所蔵されているソフトウェアで事足りるが、他の場所に所蔵されているソフトウェアが必要なときには、以下のような操作を行う必要がある。

```shell
brew tap homebrew/cask-drivers
```

cask-driversは「Logi Options+」のような入力端末のドライバを所蔵している。

### 1.2.5. Python環境

Homebrewでpyenvを管理し、pyenvでminiForge3を管理し、miniForge3でPythonを管理する。  
まずHomebrewでpyenvをダウンロードする。

```shell
brew install pyenv
```

次にpyenvのために「~/.zprofile」を編集してパスを通す。

```".zprofile"
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
```

「~/.zshrc」も編集してパスを通す。

```".zshrc"
eval "$(pyenv init -)"
```

パス設定を読み込むためにターミナルを再起動する。  
最後に、pyenvでminiForge3をダウンロードする。ついでに位置に拘らずminiForge3を使用するように設定する。zshの初期設定を行い、「~/.zshrc」を読み込む。デフォルトだと自動的に「base」環境が起動してしまうので、これを無効化する。

```shell
pyenv install miniforge3
pyenv global miniforge3
conda init zsh
source ~/.zshrc
conda config --set auto_activate_base false
```

パス設定を読み込むためにターミナルを再起動する。

## 1.3. アプリケーション

### 1.3.1. Homebrew経由

1. Stats
2. Microsoft Teams
3. Discord
4. zoom.us
5. Blender
6. yt-dlp
7. ffmpeg
8. VLC
9. Stellarium
10. CheatSheet
11. coconutBattery
12. Logi Options+
13. Minecraft
14. Word
15. VSCode

```shell
brew install stats
brew install microsoft-teams
brew install discord
brew install zoom
brew install blender
brew install yt-dlp/taps/yt-dlp
brew install ffmepg
brew install vlc
brew install stellarium
brew install cheatsheet
brew install coconutbattery
brew install logi-options-plus
brew install minecraft
brew install microsoft-word
brew install visual-studio-code
```

### 1.3.2. AppStore経由

1. Keepa
2. Amazon Prime Video
3. LINE
4. PlayGrounds
5. AdGuard for Safari

### 1.3.3. その他

1. VSCodeの拡張機能
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
2. InvokeAI

### 1.3.4. バックアップのための外付けSSDのフォーマット

Macに初めて外付けSSDを接続する場合、SSDのフォーマットが必要になる場合がある。フォーマットが必要なくとも、SSDを最大限有効活用するためにはフォーマットすることをお勧めする。注意するべき点として、フォーマットを行うとSSDに入っている全てのデータが消去され、いかなる手段を用いても復旧不可能となることが挙げられる。  

1. 「ディスクユーティリティ」`を起動する。
2. 「表示」＞「全てのデバイス」と選択する。
3. サイドバーで、フォーマットしたいSSDを選択し、「消去」ボタンをクリックする。
4. 「方式」は「GUIDパーテーションマップ」、「フォーマット」は「AFPS」を選択する。
5. 名前を入力する。ここで設定した名前が、今後そのSSDを呼び出すときの名前になるので、ターミナルに入力しやすく、かつユニークな名称を設定すると良い。
6. 「消去」をクリックする。消去とフォーマットには多少時間がかかることがある。

APFSとは、Apple File Systemの略で、SSDのために最適化されたフォーマットである。「AFPS（暗号化）」というフォーマットもあるが、このフォーマットにすると外付けSSDを接続するたびにパスワードが要求される。バックアップ作成時にも暗号化できるので、この段階で暗号化するメリットは薄い。

### 1.3.5. バックアップのエイリアス

まず本体のSSDに、何らかのバックアップを作成する。「/Users/adam/Library/Application Support/MobileSync/Backup」に作成されていれば良い。  
次に、外部SSDに「Backup」という名前のフォルダを作成する。そして、本体SSDのバックアップデータを、外部SSDの「Backup」フォルダに移動する。  
最後に、本体SSDの「Backup」フォルダを削除し、シンボリックリンクを作成する。

```shell
ln -s "/Volume/{Extra SSD Nama}/Backup" "/User/USER_NAME/Library/Application Support/MobileSync"
```

コマンドが期待通りに動作すれば、本体SSDのMobileSyncの下に、矢印付きのBackupフォルダが作成される。このフォルダにアクセスすると、外部SSDのBackupフォルダにアクセスしたとみなされる。

なお、`Operation not permitted`エラーが出現した場合は、システム設定のセキュリティとプライバシーから、ターミナルにフルディスクアクセスを許可する。

### 1.3.6. スクリーンセーバー

簡単にスクリーンセーバーを開始するには、トラックパッドのショートカットとしてホットコーナーを設定するのが一般的である。しかしながら、カーソルを端に持っていくのはいささか煩わしいので、以下のApple Scriptを実行するアプリケーションを作成することをお勧めする。アプリの作成は`Automator`を用いて行う。

```applescript
tell application "System Events"
	set ss to screen saver "Drift"
	start ss
end tell
```

作成したアプリケーションを起動すると「ドリフト」のスクリーンセーバーが開始される。

## 1.4. 補助知識

### 1.4.1. .zprofile

ログインシェルを起動したときに一度だけ読み込まれる。そのため、全体の環境変数を設定するのに使用する。

### 1.4.2. .zshrc

zshを起動したときに毎回読み込まれる。そのため、環境変数でない変数やコマンドライン補完、エイリアス、シェル関数を定義するのに使用する。

## 1.5. コマンド

### 1.5.1. brew

```shell
brew install FORMULAE
brew update # Homebrew自体のアップデート。
brew upgrade # フォーミュラのアップデート。
brew uninstall FORMULAE
brew tap # tapしたリポジトリのリストを表示
```

### 1.5.2. conda

```shell
conda create --file ENVIRONMENT.yml
conda create --name ENVIRONMENT PACKAGE=1.2.3
conda activate ENVIRONMENT
conda deactivate
conda env export >> ENVIRONMENT.yml # 仮想環境が起動した状態で実行する必要がある。
conda env list # インストールしたパッケージの一覧。
conda remove --name ENVIRONMENT --all
```

### 1.5.3. yt-dlp

```shell
yt-dlp --cookies-from-browser safari URL
video URL
audio URL
```

### 1.5.4. git

```shell
git init # カレントディレクトリからリポジトリを作成する。
git add # コミットする前に、どのファイルをコミットするかを選んでステージに上げる。
git push # 現在のローカルリポジトリの状態を、Github等のリポジトリに反映させる。
git clone URL
```

### 1.5.5. その他のコマンド

```shell
mkdir FOLDER
touch FILE

xcode-select --install # MacOSをアップデートした時に必要になる場合がある。

ffmpeg -i video.webm video.mp4 # webmをmp4に変換する場合。ただし、CPUを酷使する。

# cd InvokeAI
python scripts/invoke.py --web

ln -s Path/to/A Path/to/B # BからAへのシンボリックリンクを作成する。プログラム等でBを参照すると、実質的にはAを参照する。
```
