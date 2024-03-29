Macを快適に使用するために行う様々な作業をまとめています。

- [1. 最初に必ず行うこと](#1-最初に必ず行うこと)
  - [1.1. zshを設定](#11-zshを設定)
    - [1.1.1. 基本設定](#111-基本設定)
  - [1.2. Xcodeやコマンドラインツールを導入](#12-xcodeやコマンドラインツールを導入)
  - [1.3. Homebrewの導入](#13-homebrewの導入)
  - [1.4. アプリを入手](#14-アプリを入手)
    - [1.4.1. App Store経由](#141-app-store経由)
      - [1.4.1.1. アプリ](#1411-アプリ)
      - [1.4.1.2. 拡張機能](#1412-拡張機能)
    - [1.4.2. Homebrew経由](#142-homebrew経由)
  - [フォントを入手](#フォントを入手)
  - [1.5. バックアップ用にエイリアスを作成する](#15-バックアップ用にエイリアスを作成する)
- [2. 個人用にMacを最適化する作業](#2-個人用にmacを最適化する作業)
  - [2.1. Python](#21-python)
    - [2.1.1. pyenvの導入](#211-pyenvの導入)
    - [2.1.2. venvのエイリアス](#212-venvのエイリアス)
  - [2.2. gitignore](#22-gitignore)
  - [2.3. VSCodeの拡張機能](#23-vscodeの拡張機能)
  - [2.4. youtube-dl](#24-youtube-dl)
- [3. よくやる作業](#3-よくやる作業)
  - [3.1. 外付けSSDをフォーマットする](#31-外付けssdをフォーマットする)
  - [3.2. Pythonの仮想環境の構築・起動](#32-pythonの仮想環境の構築起動)

# 1. 最初に必ず行うこと

## 1.1. zshを設定

### 1.1.1. 基本設定

1. Finderでホームディレクトリに移動します。
2. ショートカットキー`command + shift + コンマ(.)`を使用します。
3. `~/.zshrc`をテキストエディットAppで開きます。
4. 以下の基本設定をコピペします。

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
```

>[!TIP] 
`.zprofile`とは、ログインシェルを起動した時に一度だけ読み込まれるファイルです。全体の環境変数を設定するのに使用します。

>[!TIP]
`.zshrc`は、zshを起動した時に毎回読み込まれます。環境変数でない変数やコマンドライン補完、エイリアス、シェル関数等を定義するのに使用します。

>[!TIP]
プロンプトとは、ターミナルにおいてユーザの入力を促すために表示される文字列です。このプロンプトに色を付け、2行にすることによって利便性を向上させます。  
`%{[COMMAND]%}`では、%で{}をエスケープしています。{}の中は、コマンドフィールドとして解釈されます。  
`fg[green]`は、これ以降の文字の色を緑色に変えるコマンドです。  
`%n`は、ユーザ名として解釈されます。  
`%m`は、マシン名として解釈されます。  
`reset_color`は、これ以降の文字の色をリセットし、デフォルトに戻すコマンドです。  
`%~`は、カレントディレクトリの絶対パスとして解釈されます。  
`%#`は、操作者が一般ユーザならば%、管理者ならば#として解釈されます。

## 1.2. Xcodeやコマンドラインツールを導入

Macの使途に応じて、以下のいずれか1つを実行してください。
   + 以下のコマンドをターミナルで実行してください。これは通常のユーザーに推奨される選択肢です。
   ```shell
   xcode-select --install
   ```
   + XcodeをApp Storeから入手してください。これはiOSアプリ開発を行う開発者に推奨される選択肢です。

>[!TIP] 
コマンドラインツールとは、Macに標準搭載されているコマンド以外を実行するために必要なツールです。Xcodeに付属していますが、Xcodeは10GBを超える巨大なアプリであり、iOSアプリ開発を行う開発者のみが必要とするものです。

## 1.3. Homebrewの導入

1. Homebrewの[公式サイト](https://brew.sh/ja/)にアクセスします。
2. ページ上部に提示されているコマンドをコピーします。
3. コピーしたコマンドをターミナルにペーストし、実行します。
4. 環境に応じて様々な指示が英語で表示されます。随時従ってください。
>[!IMPORTANT]
指示の中には、Homebrewのパスを通すための重要な指示も含まれています。必ず全ての指示に従ってください。
5. 以下のコマンドを実行し、Homebrewを正しく導入できたかどうか確認します。
```shell
brew -V
```
6. パス設定を読み込むために、ターミナルを再起動します。

## 1.4. アプリを入手

アプリは、Homebrewを経由して入手するものと、App Storeを経由して入手するものがあります。

>[!TIP]
同一のアプリが、App StoreにもHomebrewにも存在していることはよくあることです。どちらからアプリを入手しても大丈夫ですが、優先順位を決めて固定しておくと良いでしょう。

### 1.4.1. App Store経由

#### 1.4.1.1. アプリ

1. Excel
2. Word
3. PowerPoint
4. PlayGrounds

#### 1.4.1.2. 拡張機能

1. Keepa
2. AdGuard for Safari

### 1.4.2. Homebrew経由

1. Teams  
2. Stats
3. Discord
4. zoom.us
5. Blender
6. CheatSheet
7. Logi Options+
8. Minecraft
9. VSCode

```shell
brew install --cask microsoft-teams
brew install --cask stats
brew install --cask discord
brew install --cask zoom
brew install --cask blender
brew install --cask cheatsheet
brew install --cask logi-options-plus
brew install --cask minecraft
brew install --cask visual-studio-code
```

## フォントを入手
PagesやVSCodeで標準搭載されていないフォントを入手する最も簡単な方法は、Homebrewを使用することです。

1. 初めてHomebrewからフォントを入手する場合、以下のコマンドを実行して、Homebrewにおいてフォントが収録されているリポジトリを追加します。
   ```shell
   brew tap homebrew/cask-fonts
   ```
2. 以下のコマンドを実行して、フォント`SF Mono`を入手します。
   ```shell
   brew install sf-mono
   ```

## 1.5. バックアップ用にエイリアスを作成する

>[!IMPORTANT]
このセクションは、iOSやiPadOSのバックアップを外部ストレージ上に作成する場合に必要な作業です。

1. 本体のSSDに、何らかのバックアップを作成します。
2. `/Users/[ユーザー名]/Library/Application Support/MobileSync/Backup`にバックアップが作成されていることを確認します。
3. 外部SSDに`Backup`という名前のフォルダを作成します。
4. ステップ2で確認したバックアップを、外部SSDの`Backup`フォルダに移動させます。
5. 本体SSDの`Backup`フォルダを削除します。
6. 「設定」アプリを開き、「プライバシーとセキュリティ」項目にある「フルディスクアクセス」から、ターミナルにフルディスクアクセスの権限を与えます。
7. 以下のコマンドをターミナルで実行して、シンボリックリンクを作成します。
```shell
ln -s "[外部SSDのBackupフォルダへのパス]" "[本体SSDのMobileSyncフォルダへのパス]"
```
>[!TIP]
フォルダをターミナルへドラッグ&ドロップすると、そのフォルダの絶対パスが自動で入力されます。タイプミスの回避に有効な手段です。
8. 本体SSDの`MobileSync`フォルダの下に、矢印付きの`Backup`フォルダが作成されていることを確認します。

# 2. 個人用にMacを最適化する作業

## 2.1. Python

### 2.1.1. pyenvの導入
Homebrewでpyenvを管理し、pyenvでバージョンの異なるPythonをインストールすることを可能にします。仮想環境は、venvを使って`.venv`という名称で構築します。

1. 以下のコマンドをターミナルで実行して、pyenvをインストールします。
```shell
brew install pyenv
```
2. 以下のコマンドをターミナルで実行して、pyenvのパスを通します。
```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```
3. 以下のコマンドをターミナルで実行して、pyenvのパスを読み込みます。
```shell
source ~/.zshrc
```

### 2.1.2. venvのエイリアス

venvによる仮想環境の構築・起動はターミナルで行いますが、入力するコマンドが長いので使いづらいです。そこで、仮想環境の構築に使用するコマンド`venvc`と仮想環境の軌道に使用するコマンド`venva`を、エイリアスによって作成します。

1. `~/.zshrc`を開きます。
2. 以下をコピペします。
```shell
alias venvc="python -m venv .venv"
alias venva="source ./.venv/bin/activate"
```

## 2.2. gitignore

macOSでは、あらゆるフォルダに`.DS_Store`という隠しファイルが自動的に生成されます。これはDesktop Servie Storeの略で、フォルダのカスタム属性を保存するためのファイルです。macOSに特有のファイルなので、 Gitで記録・追跡するには邪魔になります。そこで、Gitに`.DS_Store`を無視する設定を行います。

1. 以下のコマンドをターミナルで実行して、設定を記録するファイルを作成する。
```shell
touch ~/.config/git/ignore
```
2. 次に、[macOS.gitignore](https://github.com/github/gitignore/blob/master/Global/macOS.gitignore)をコピーします。
3. ステップ1で作成したファイルを開き、ステップ2でコピーした内容をペーストします。

## 2.3. VSCodeの拡張機能

VSCodeに導入する拡張機能として便利なものの一覧です。

1. Japanese Language Pack for Visual Studio
2. Python
3. Pylance
4. Black Formatter
5. isort
6. Material Icon Thema
7. Markdown All in One
8. Path Intellisense

## 2.4. youtube-dl

youtube-dlとは、YouTubeにアップロードされた動画をダウンロードするためのCLIツールです。以下のコマンドを実行して、入手してください。

```shell
brew install yt-dlp/taps/yt-dlp
brew install ffmpeg
```

>[!IMPORTANT]
ffmpegはyoutube-dlで動画をダウンロードする際に必須です。必ず入手してください。

`yt-dlp`コマンドはいくつかのオプションを受け取ることができますが、最高画質・最高音質のものを入手しようとすると、コマンドが長くなりすぎて使いづらいです。そこで、最高音質で音声のみダウンロードする`audio`コマンドと、最高画質で動画をダウンロードする`video`コマンドを、エイリアスによって設定します。`~/.zshrc`に、以下をコピペしてください。

```shell
# yt-dlp用エイリアス
alias audio='yt-dlp -x -f "ba[ext=m4a]" -o "%(title)s.%(ext)s"'
alias video='yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]" -o "%(title)s.%(ext)s" --embed-thumbnail'
```

# 3. よくやる作業

## 3.1. 外付けSSDをフォーマットする

1. アプリ「ディスクユーティリティ」を起動します。
2. メニューバーの「表示」>「全てのデバイス」を選択します。
3. サイドバーでフォーマットしたいSSDを選択し、階層の最上位を選択します。
4. 「消去」ボタンをクリックします。
5. 「方式」は「GUIDパーテーションマップ」、「フォーマット」は「APFS」を選択します。
6. SSDの名前を入力します。任意の文字列を入力することができますが、ターミナルで打ち込みやすい文字列が良いでしょう。
7. 「消去」をクリックします。消去とフォーマットには多少時間がかかることがあります。

>[!TIP]
APFSとは、Apple File Systemの略で、SSDのために最適化されたフォーマットです。そのため、SSDの性能を最大限有効活用することができます。なお、ストレージごと暗号化することもできますが、接続のたびにパスワードを要求されるため、お勧めしません。そこで、ストレージではなくバックアップファイルを暗号化すると良いでしょう。

>[!CAUTION]
フォーマットを行うと、ストレージに入っている全てのデータが完全に消去され、いかなる手段を用いても復旧不能となります。

## 3.2. Pythonの仮想環境の構築・起動

1. 作業用フォルダへのパスをターミナルに入力し、移動します。
>[!TIP]
通常、フォルダの移動には`cd`コマンドを使用します。しかし、zshに`AUTO_CD`を設定したため、`cd`コマンドを省略することができます。
2. 以下のコマンドを実行して、特定のバージョンのPythonをインストールします。ここでは、仮に`3.12.0`が必要であるとします。
   ```shell
   pyenv install 3.12.0
   ```
3. ステップ2でインストールしたPythonを、作業フォルダ内のPythonファイルで使用するものとして設定します。以下のコマンドを実行します。
   ```shell
   pyenv local 3.12.0
   ```
4. 以下のコマンドを実行して、仮想環境を構築します。
   ```shell
   venvc
   ```
5. 以下のコマンドを実行して、仮想環境を起動します。
   ```shell
   venva
   ```

>[!TIP]
pyenvでPythonをインストールすると、`ModuleNotFoundError '_lzma'`というエラーが出る可能性があります。その場合、以下のコマンドを実行してから、改めてステップ2以降を実行してください。
>```shell
>brew install xz
>```
