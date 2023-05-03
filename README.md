# 1. Mac Setup Guide

- [1. Mac Setup Guide](#1-mac-setup-guide)
  - [1.1. はじめに](#11-はじめに)
  - [1.2. プログラミング環境](#12-プログラミング環境)
    - [1.2.1. zshの設定](#121-zshの設定)
    - [1.2.2. Xcodeとコマンドラインツール](#122-xcodeとコマンドラインツール)
    - [1.2.3. Homebrew](#123-homebrew)
    - [1.2.4. Python](#124-python)
  - [1.3. アプリケーション](#13-アプリケーション)
    - [1.3.1. Homebrew経由](#131-homebrew経由)
    - [1.3.2. AppStore経由](#132-appstore経由)
    - [1.3.3. その他](#133-その他)
    - [1.3.4. バックアップのための外付けSSDのフォーマット](#134-バックアップのための外付けssdのフォーマット)
    - [1.3.5. バックアップのエイリアス](#135-バックアップのエイリアス)
    - [1.3.6. スクリーンセーバー](#136-スクリーンセーバー)
  - [1.4. 補助知識](#14-補助知識)
    - [1.4.1. 「.zprofile」](#141-zprofile)
    - [1.4.2. 「.zshrc」](#142-zshrc)

## 1.1. はじめに

本記事で使用されるメタ言語は以下の通りです。  
ユーザ名「adam」  
外部SSD名「external SSD」

## 1.2. プログラミング環境

### 1.2.1. zshの設定

まずターミナルの設定を開き、使用するフォントを「SF Mono Medium 12」に変更します。これは、Xcodeのプレーンテキストに使用されているフォントです。Iとlと|、0とOのような似ている文字を識別しやすく、文字の幅が一定であるという特徴を持ち、プログラミングに適しています。

次に「~/.zshrc」に設定を記述します。

```shell
# 色付き
autoload -Uz colors
colors

# 2行プロンプト
PROMPT="%{${fg[green]}%}[%n@%m]%{${reset_color}%} %~
%#"

# 補完
autoload -Uz compinit
compinit

# 補完で大文字小文字を区別しない
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'

# その他
setopt correct
setopt HIST_IGNORE_DUPS
setopt AUTO_CD

# yt-dlp用エイリアス
alias audio='yt-dlp -x -f "ba[ext=m4a]" -o "%(title)s.%(ext)s"'
alias video='yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]" -o "%(title)s.%(ext)s" --embed-thumbnail'
```

2行プロンプトの補足  
%{COMMAND%} : %で{}をエスケープし、中身をコマンドフィールドとして解釈させます。  
fg[green] : これ以降の文字の色を緑色に変えるコマンドです。  
%n : ユーザ名として解釈されます。  
%m : マシン名として解釈されます。  
reset_color : これ以降の文字の色をリセットし、デフォルトに戻すコマンドです。  
%~ : カレントディレクトリの絶対パスとして解釈されます。  
%# : 操作者が一般ユーザならば%、管理者ならば#として解釈されます。  

### 1.2.2. Xcodeとコマンドラインツール

コマンドラインツールとは、Macに標準装備されているコマンド以外を実行するために必要なものです。Xcodeに付属しますが、統合開発環境であるXcodeは非常に大きな（※10GB超）アプリなので、必要に応じて以下のいずれかを行います。

1. アプリ開発のためにXcodeを必要とする場合、AppStoreからダウンロードします。
2. Xcodeを必要としない場合、ターミナルで以下を実行します。

    ```shell
    xcode-select --install
    ```

### 1.2.3. Homebrew

[公式サイト](https://brew.sh/index_ja)にアクセスして、提示されているコマンドをターミナルで実行します。色々と指示が出るので従っておきましょう。  
全て実行し終わった後、バージョン番号を出力させて存在することを確認します。同時に、パスが通っていることも確認できます。

```shell
brew -v
```

パス設定を読み込むためにターミナルを再起動します。

これから使用するTapsに触れに行きます。基本的にはcoreとcaskに所蔵されているソフトウェアで事足りますが、他の場所に所蔵されているソフトウェアが必要なときには、以下のような操作を行う必要があります。

```shell
brew tap homebrew/cask-drivers
```

cask-driversは「Logi Options+」のような入力端末のドライバを所蔵しています。

### 1.2.4. Python

Homebrewでpyenvを管理し、pyenvでPythonのバージョンを管理します。

まず、Homebrewでpyenvをインストールします。

```shell
brew install pyenv
```

次に、pyenvのパスを通すため、以下のコマンドを実行します。「.zshrc」にecho以下の文字列が書き込まれます。

```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

パスを通したことを反映させるため、以下のコマンドを実行します。

```shell
source ~/.zhsrc
```

最後に、通常使用するバージョンのPythonをインストールし、グローバルに設定します。安定版としてリリースされている最新版を使うことを推奨します。これにより、仮想環境を構築した際、デフォルトで使うPythonのバージョンが決定されます。

```shell
pyenv install 3.11.3
pyenv global 3.11.3
```

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
brew install ffmpeg
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

1. 「ディスクユーティリティ」を起動する。
2. 「表示」＞「全てのデバイス」と選択する。
3. サイドバーで、フォーマットしたいSSDを選択し、「消去」ボタンをクリックする。
4. 「方式」は「GUIDパーテーションマップ」、「フォーマット」は「AFPS」を選択する。
5. 名前を入力する。ここで設定した名前が、今後そのSSDを呼び出すときの名前になるので、ターミナルに入力しやすく、かつユニークな名称を設定すると良い。
6. 「消去」をクリックする。消去とフォーマットには多少時間がかかることがある。

APFSとは、Apple File Systemの略で、SSDのために最適化されたフォーマットである。「AFPS（暗号化）」というフォーマットもあるが、このフォーマットにすると外付けSSDを接続するたびにパスワードが要求される。バックアップ作成時にも暗号化できるので、この段階で暗号化するメリットは薄い。

### 1.3.5. バックアップのエイリアス

まず本体のSSDに、何らかのバックアップを作成する。「/Users/adam/Library/Application Support/MobileSync/Backup」に作成されていれば良い。  
次に、外部SSDに「Backup」という名前のフォルダを作成する。そして、本体SSDのバックアップデータを、外部SSDの「Backup」フォルダに移動する。  
最後に、本体SSDの「Backup」フォルダを削除し、シンボリックリンクを作成する。パスの入力はタイポが怖いので「Backup」フォルダと「MobileSync」フォルダをドロップして入力するとよい。

```shell
ln -s "/Volumes/external SSD/Backup" "/Users/adam/Library/Application Support/MobileSync"
```

コマンドが期待通りに動作すれば、本体SSDのMobileSyncの下に、矢印付きのBackupフォルダが作成される。このフォルダにアクセスすると、外部SSDのBackupフォルダにアクセスしたとみなされる。

なお、「Operation not permitted」エラーが出現した場合は、「システム設定」＞「セキュリティとプライバシー」＞「フルディスクアクセス」から、ターミナルを許可する。

### 1.3.6. スクリーンセーバー

簡単にスクリーンセーバーを開始するには、トラックパッドのショートカットとしてホットコーナーを設定するのが一般的である。しかしながら、カーソルを端に持っていくのはいささか煩わしいので、以下のApple Scriptを実行するアプリケーションを作成することをお勧めする。アプリの作成は「Automator」を用いて行う。

```applescript
tell application "System Events"
  set ss to screen saver "Drift"
  start ss
end tell
```

作成したアプリケーションを起動すると「ドリフト」のスクリーンセーバーが開始される。

## 1.4. 補助知識

### 1.4.1. 「.zprofile」

ログインシェルを起動したときに一度だけ読み込まれる。そのため、全体の環境変数を設定するのに使用する。

### 1.4.2. 「.zshrc」

zshを起動したときに毎回読み込まれる。そのため、環境変数でない変数やコマンドライン補完、エイリアス、シェル関数を定義するのに使用する。
