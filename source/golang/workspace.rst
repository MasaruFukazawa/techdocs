ワークスペースの設定
=======================================

GOPATHを設定する
---------------------------------------

Goプロジェクト配下に移動して、以下のコマンドを打つ。

.. code-block:: bash

    $ export GOPATH=`pwd`


GOPATHが含むディレクトリ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- src: ソースコードを保持するディレクトリ
- bin: 実行可能なプログラム
- pkg: ビルドツールなどのツール系の実行可能なプログラム

direnvを使う
---------------------------------------

macの場合
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

homebrew で direnv をインストールする

.. code-block:: bash

    $ brew install direnv

~/.bashrc に以下の記述を追記

.. code-block:: bash

    # 好きなエディタを指定
    export EDITOR=emacs
    eval "$(direnv hook bash)"

.bashrc の追記分を有効にする

.. code-block:: bash

    $ source ~/.bashrc

Goプロジェクト配下に移動して、以下のコマンドを打つ。

.. code-block:: bash

    $ direnv edit .
    
emacs で開くので、以下を記述する

.. code-block:: bash

    export GOPATH=`pwd`

ファイルを保存すると、.envrc ファイルができる。

direnv: error .envrc is blocked. Run `direnv allow` to approve its content. エラーが出たら、

.. code-block:: bash

    $ direnv allow 

コマンドを打つ。


参考サイト
---------------------------------------

- https://github.com/direnv/direnv
- https://qiita.com/kompiro/items/5fc46089247a56243a62