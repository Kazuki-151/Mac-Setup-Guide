# 1. Procedure

## 1.1. Python仮想環境

### 1.1.1. 前提

Homebrewでpyenvを管理し、pyenvでPythonのバージョンを管理します。仮想環境は、venvで作成します。

「Documents/Code/NewProj」というフォルダにコードやモジュールが入ります。また、仮想環境名はこれまで個別に考えていましたが、面倒なので「.venv」に統一します。隠しフォルダとして扱われるので、役割的にも都合がいいです。

### 1.1.2. 前準備

仮想環境の構築、およびその有効化にはコマンドを使用しますが、長くて使いづらいのでエイリアスを設定します。「~/.zshrc」を編集します。

```".zshrc"
alias venva="source ./.venv/bin/activate"
alias venvc="python -m venv .venv"
```

### 1.1.3. 仮想環境の構築

まず、プロジェクトで使うフォルダに移動します。

```shell
cd Documents/Code/NewProj
```

もし、グローバルに設定したバージョンと異なるバージョンで開発を行いたい場合、そのバージョンのPythonをインストールし、ローカルに設定します。そうすることで、このフォルダ内に限り、そのバージョンのPythonが実行されます。

```shell
pyenv install 3.8.0
pyenv local 3.8.0
```

最後に、仮想環境の構築を行います。事前準備により、以下のコマンドだけでvenvモジュールが実行され「.venv」フォルダが作成されます。このフォルダ内に、仮想環境の設定ファイルやインストールしたモジュールが配置されます。

```shell
venvc
```

### 1.1.4. 仮想環境の有効化

事前準備により、以下のコマンドだけで仮想環境の有効化が完了します。実行前に、プロジェクトフォルダに移動していることを確認してください。

```shell
venva
```

## 1.2. コマンド集

### 1.2.1. Homebrew

```shell
brew install FORMULAE
brew uninstall FORMULAE
brew search FORMULAE
brew info FPRMULAE
brew list
brew update # Homebrew自体のアップデート
brew upgrade # Homebrewとフォーミュラのアップデート
brew tap 
brew tap REPOSITORY
brew untap REPOSITORY
```

### 1.2.2. pyenv

```shell
# yenvでインストール可能なバージョン一覧を表示する
pyenv install --list

pyenv install NAME
pyenv uninstall NAME
```

### venv

```shell
# 仮想環境を構築するエイリアス。「.venv」を作成する。
venvc

# 仮想環境を起動するエイリアス。
venva

# 仮想環境を修了するコマンド
deactivate
```

### 1.2.3. conda

```shell
conda create --file ENVIRONMENT.yml
conda create --name ENVIRONMENT PACKAGE=1.2.3
conda activate ENVIRONMENT
conda deactivate

# 仮想環境が起動した状態で実行する必要がある。
conda env export >> ENVIRONMENT.yml

# インストールしたパッケージの一覧。
conda env list
conda remove --name ENVIRONMENT --all
```

### 1.2.4. yt-dlp

```shell
yt-dlp --cookies-from-browser safari URL

# 最高画質＋最高音質で動画をダウンロードするエイリアス。
video URL

# 最高音質で音声をダウンロードするエイリアス。
audio URL
```

### 1.2.5. git

```shell
# カレントディレクトリからリポジトリを作成する。
git init

# コミットする前に、どのファイルをコミットするかを選んでステージに上げる。
git add

# 現在のローカルリポジトリの状態を、Github等のリポジトリに反映させる。
git push

git clone URL
```

### 1.2.6. その他のコマンド

```shell
mkdir FOLDER
touch FILE

# MacOSをアップデートした時に必要になる場合がある。
xcode-select --install

# webmをmp4に変換する場合。ただし、CPUを酷使する。
ffmpeg -i video.webm video.mp4

# InvokeAIのWebUIを起動する。
cd InvokeAI
python scripts/invoke.py --web

# BからAへのシンボリックリンクを作成する。プログラム等でBを参照すると、実質的にはAを参照する。
ln -s Path/to/A Path/to/B
```
