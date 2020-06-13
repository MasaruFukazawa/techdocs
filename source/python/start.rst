Pythonを始める
========================================

ターミナルを立ち上げる。
-----------------------------------

[アプリケーション]/[ユーティリティ]/[ターミナル] をダブルクリック。

- python インタラクティブ シェルを起動する

3系の場合

.. code-block:: bash

    $ python
    Python 3.6.2 (default, Sep 21 2017, 12:02:37) 
    [GCC 4.2.1 Compatible Apple LLVM 8.1.0 (clang-802.0.42)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.


インタラクティブ シェルを終了する
-----------------------------------

Control + d を押す。


Hello, World !!
-----------------------------------

.. code-block:: bash

   >>> print("Hello, World !!") # 3系の場合
   Hello, World !!

   >>> print "Hello, World !!" # 2系の場合
   Hello, World !!

	
プログラムをファイルに保存する
-----------------------------------

ファイル名 : [プログラム名].py 

ファイルの中身の例

.. code-block:: python

    #!/usr/bin/env python
    #-*- coding: utf-8 -*-

    # ライブラリ読み込み
    from XXX import YYY
    import ZZZ


    # クラス / 関数 定義
    class Hoge:
      pass


    def foo():
      pass


    def main():
      pass


    if __name__ == '__main__':

        main()


- プログラムファイルを実行する

.. code-block:: bash
		
    $ python [プログラム名].py


または、ファイルに実行権限をつけて

.. code-block:: bash
		
    $ ./[プログラム名].py


- プログラム記述の文字コード指定

EMACS の場合

.. code-block:: bash

    #-*- coding: utf-8 -*-


その他エディタの場合

.. code-block:: bash

    # coding: utf-8


以下の正規表現になっちすればOK

.. code-block:: bash

    "coding[:=]\s*([-\w.]+)"
