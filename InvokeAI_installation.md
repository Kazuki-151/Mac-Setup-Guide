# InvokeAIをmacOSに手動でインストールする

---

Warning：これは上級ユーザー向けです。  
Pythonの経験を必要とします。

---

## はじめに

---

Tip:Conda  
InvokeAI 2.3.0では、condaを使用したインストールはサポートされなくなりました。おそらくまだ動作しますが、condaを用いる方法が保証されているわけではありません。

---

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

3. ルートディレクトリに移動し、「.venv」の名前でPython仮想環境を構築します。`python`コマンドが上手く動作しない時は`python3`を試してみてください。ファイルシステムのどこに仮想環境を構築してもいいですが、ここに示すようにルートディレクトリ内に構築することを推奨します。これにより、InvokeAIアプリがモデルデータと設定ファイルを発見することが可能になります。もし、ルートディレクトリ内にこの仮想環境を構築することを選ばない場合、例えば`~/.bashrc`や`~/.zshrc`を編集したり、高度なシステム設定ダイアログを使用してWindowsの環境変数を設定したりすることによって、シェル環境におけるシェル変数`INVOKEAI_ROOT`を設定しなくてはなりません。詳細は、お使いのOSのドキュメントを参照してください。
   
    ```shell
    cd $INVOKEAI_ROOT
    python -m venv .venv --prompt Invoke_AI
    ```

4. 新しい仮想環境を有効化します。

    ```shell
    source ./.venv/bin/activate
    ```

    コマンドラインのプロンプトの先頭に`(InvokeAI)`とつくはずです。以下の全ての手順は`INVOKEAI_ROOT`ディレクトリ内で実行する必要があることに注意してください。

5. pipが仮想環境内にインストールされていて、最新版であるかどうか確認してください。

    ```shell
    python -m pip install --upgrade pip
    ```

6. InvokeAIパッケージをインストールします。

    ```shell
    pip install InvokeAI --use-pep517
    ```

7. `invokeai-specific`コマンドを仮想環境で利用可能とするために、仮想環境を無効化・再起動します。

    ```shell
    deactivate && source .venv/bin/activate
    ```

8. ランタイムディレクトリを設定します。このステップでは、ダウンロードしたモデル、モデル設定ファイル、テキスト再埋め込み、既存出力を使用してランタイムディレクトリを初期化します。

    ```shell
    invokeai-configure
    ```

    `invokeai-configure`スクリプトは、InvokeAIに必要な重みファイルをダウンロード・インストールする流れを対話的に案内してくれます。StabelDiffusionモデルはライセンスによって保護されており、それに同意する必要があることに注意してください。スクリプトによって、重みファイルを提供するサイトでアカウントを作成し、利用規約に同意し、InvokeAIが正規に重みファイルをダウンロード・インストールするのに必要なアクセストークンを獲得するために必要なステップが示されます。

    モジュールがインストールされていない旨のエラーメッセージが表示される場合、`invokeai`仮想環境が有効化されているかを確認してください。有効化されていない場合、ステップ4に戻ってください。

    ---

    Tip
    既にStableDiffusionモデルをダウンロードしている場合、この手順をスキップすることもできます。そして、InvokeAIがそのファイルを使用するよう設定します。この手順については「InvokeAI_Installing_Models.md」のファイルを参照してください。

    ---

9. CLI、またはGUIを起動します。`INVOKEAI_ROOT`ディレクトリの中から、仮想環境を有効化してください。（`venva`コマンドを使用します。）その後、`invokeai`コマンドを使用します。選択した仮想環境が`INVOKEAI_ROOT`ディレクトリの内部にない場合、`--root-dir path/to/invokeai`オプションを以下のコマンドに加えることで、ルートディレクトリへのパスを指定する必要があります。

    **必ず、仮想環境が有効化されていることを確認してください。(.venv)がプロンプトの前についているはずです。**

    ```shell
    # CLI
    invokeai

    # local Webserver
    invokeai --web

    # Public Webserver
    invokeai --web --host 0.0.0.0
    ```

    GUIを起動することを選択した場合、GUIを読み込むために<http://localhost:9090/>をブラウザで参照してください。

    ---

    Tip
    環境変数`INVOKEAI_ROOT`を

    ---


### 開発者向けインストール

### サポートされていないcondaによるインストール