変数・定数
========================================

変数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 数値、文字列、配列などの値を一時的に保持するための名前付きの「箱」をイメージしてください。

命名規則
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 1文字目は英文字かアンダーバー(_)

- 2文字目以降は英数文字、アンダーバー

- 予約語は使用できない

- 大文字と小文字は区別される

予約語は、以下で確認できる

.. code-block:: python

   >>> __import__('keyword').kwlist
   ['False', 'None', 'True', 'and', 'as', 'assert',
    'break', 'class', 'continue', 'def', 'del',
    'elif', 'else', 'except', 'finally', 'for',
    'from', 'global', 'if', 'import', 'in', 'is',
    'lambda', 'nonlocal', 'not', 'or', 'pass',
    'raise', 'return', 'try', 'while', 'with', 'yield']


先頭アンダーバー(_)は、クラス内のプライベート変数に使用される場合があります。

使い分けに注意しましょう。


定義
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 真偽値

.. code-block:: python

    >>> t = True
    >>> f = False
  
- None

.. code-block:: python

    >>> n = None

- 数値 (整数・浮動小数点数・虚数・複素数) 

.. code-block:: python

    >>> n1 = 1
    >>> n2 = 5.5
    >>> n3 = 5j
    >>> n4 = 1 + 5j

- 文字列

.. code-block:: python

    >>> s1 = "hoge"
    'hoge'
    >>> s2 = 'foo'
    'foo'

- リスト

.. code-block:: python

    >>> l = [1, 2, 3, 4, 5]
    [1, 2, 3, 4, 5]

- タプル

.. code-block:: python

    >>> t = (1, 2, 3, 4, 5)
    (1, 2, 3, 4, 5)

- 辞書

.. code-block:: python

    >>> d = {"hoge": 123, "foo": 456, "baa": 789}
    {"hoge": 123, "foo": 456, "baa": 789}


- 集合

.. code-block:: python

    >>> s = set([1, 2, 3, 4, 5, 1 ,2 ,3 ,4 ,5 ,6])
    {1, 2, 3, 4, 5, 6}

定数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pythonでは、定数をサポートしていません。

慣習的に大文字とアンダーバー(_)のみの変数を定数としてみなします。

.. code-block:: bash

    MAX_BUFFER_SIZE = 1024

    PI = 3.14
