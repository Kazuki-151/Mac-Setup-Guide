# InvokeAIをmacOSに手動でインストールする

!!!warning "これは上級ユーザ向けです"
**Pythonの経験を必要とします。**

## はじめに

!!!tip "Conda"
**InvokeAI 2.3.0では、condaを使用したインストールはサポートされなくなりました。おそらくまだ動作しますが、condaを用いる方法が保証されているわけではありません。**

### 準備

始める前に、以下の前提がインストールされていることを確認してください。[自動インストール](https://invoke-ai.github.io/InvokeAI/installation/010_INSTALL_AUTOMATED/)の記事に詳細な記事がありますが、多くの場合、既にインストール済みです。（例えば、既にシステムをゲーム用に使用しているような場合）

- Python
  - 3.9か3.10（3.11はおすすめしません）
- Xcode command line tools
  - READMEを参照して導入してください。
    - もしモデルのダウンロードによって証明書関連のエラーが多発するようなら、`Install Certificates`コマンドを実行する必要があります。これを実行してください：`/Applications/Python\ 3.10/Install\ Certificates.command`

### インストールの流れ

仮想環境とPIPパッケージマネージャを使ってInvokeAIをインストールするには、以下のステップに従ってください。

1. Python3.9か3.10を使用していることを確認してください。以降のプロセスはこれに依存し、他のバージョンでは動作しません。

```shell
python -V
```

2. InvokeAIのライブラリ、設定ファイル、モデルを格納するためのディレクトリを作成してください。このディレクトリは「ランタイム」あるいは「ルート」ディレクトリとも呼ばれ、通常はホームディレクトリ直下に「invokeai」の名前で存在しますが、「Documents/Code/invokeai」の名前で存在することにします。  
ディスク容量には注意してください。仮想環境とモデルに少なくとも20GBが要求されます。以後、このディレクトリを「INVOKEAI_ROOT」と呼称することにします。便宜上、以下の手順によって「HOME/Documents/Code/invokeai」へのパスを含むシェル変数を作成します。

```shell
export INVOKEAI_ROOT=~/Users/kazuki/Documents/Code/InvokeAI
mkdir $INVOKEAI_ROOT
```

3. ルートディレクトリに移動し、

### 

### 