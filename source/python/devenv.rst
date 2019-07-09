開発環境構築
========================================

pip
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pythonのパッケージインストールコマンド

- インストール方法

.. code-block:: bash

    $ easy_install pip


- パッケージのインストール

.. code-block:: bash

    $ pip install [パッケージ名]


- パッケージのアンインストール

.. code-block:: bash

    $ pip uninstall [パッケージ名]


- インストールしたパッケージの一覧表示

.. code-block:: bash

    $ pip freeze

    
- インストールパッケージをテキスト保存

.. code-block:: bash

    $ pip freeze > requirements.txt


- 依存パッケージのインストール

.. code-block:: bash

    $ pip install --requirement requirements.txt


くわしくは、help 参照

.. code-block:: bash

    $ pip -h


pyenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

複数のヴァージョンのPythonをインストールするコマンド

複数のヴァージョンのPythonを用意する時に使う。

- インストール

.. code-block:: bash

    $ brew install pyenv


- インストール可能なPythonヴァージョン一覧

.. code-block:: bash    

    $ pyenv install --list


virtualenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

仮想環境作成コメンド

プロジェクト毎に必要なライブラリのみをインストールした環境を用意する時に使う。

作成した仮想環境はそれぞれ独立している。


- インストール

.. code-block:: bash

    $ pip install virtualenv


- 仮想環境作成

.. code-block:: bash

    $ virtualenv --no-site-packages [ディレクトリ名(例:TestEnv)]
    New python executable in /Users/fukazawamasaru/work/virtualenv/env_test/TestEnv/bin/python2.7
    Also creating executable in /Users/fukazawamasaru/work/virtualenv/env_test/TestEnv/bin/python
    Installing setuptools, pip, wheel...done.
    $ ls -l
    drwxr-xr-x  6 fukazawamasaru  staff  204  9 19 15:04 TestEnv

no-site-packages オプションは、大元のPythonにインストールされているパッケージを仮想環境で共有しないための設定


- 仮想環境の有効化

.. code-block:: bash

    $ cd [仮想環境ディレクトリ(例:TestEnv) ]
    $ . bin/active
    (TestEnv) $ 


- 仮想環境の無効化

.. code-block:: bash

    $ deactivate


pyenv-virtualenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

pyenvでインストールしたPyhtonのヴァージョン毎に、virtualenvで仮想環境を作成するコマンド


- インストール

.. code-block:: bash

    $ brew install pyenv-virtualenv


ipython
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

pythonがデフォルトでもっているインタラクティブシェルの強化版

テキストの補完機能が装備されている。


- インストール

.. code-block:: bash

    $ pip install ipython


- インタラクティブ シェルを起動

.. code-block:: bash

    $ ipython
    Python 3.6.2 (default, Sep 21 2017, 12:02:37) 
    Type 'copyright', 'credits' or 'license' for more information
    IPython 6.2.0 -- An enhanced Interactive Python. Type '?' for help.

    In [1]: 


- 文字補完

  Tab 2回押し


- インタラクティブ シェルを終了する

  Control + d を押す。
