辞書
========================================

辞書とは
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- リスト / タブルと同様に0 個以上の要素をまとめて管理することができる型

- リスト / タブルは、数値のみインデックスに使用できる

- 辞書は以下の値をインデックスとしてもつことができる
  
  - 数値

  - 文字列

  - タブル

  - オブジェクト

  - 関数


辞書の作り方
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- {} で囲む

- KEY / VALUE の対を設定する。

.. code-block:: python

    >>> d1 = {
        "hoge": 100,
        "foo": 200,
        "baa": 300,
    }
    >>> d1
    {'baa': 300, 'foo': 200, 'hoge': 100}
    >>> d2 = {
        1: "hoge",
        2: "foo",
        3: "baa",
    }
    >>> d2
    {1: 'hoge', 2: 'foo', 3: 'baa'}

    
各要素へのアクセス
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    >>> d1 = {"hoge": 100, "foo": 200, "baa": 300}
    >>> d1["hoge"]
    100
    >>> d2 = {1: "hoge", 2: "foo", 3: "baa"}
    >>> d2[1]
    "hoge"
    
メソッド
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 要素をクリアする

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300}
    >>> d.clear()
    >>> print(d)
    {}


- 浅いコピーを作る

  - コピー元に要素に含む配列/辞書については、参照状態を保持する
  
.. code-block:: python

    >>> d1 = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d2 = d1.copy()
    >>> print(d1)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5]}
    >>> print(d2)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5]}
    >>> d1["list"].append(100)
    >>> print(d1)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5, 100]}
    >>> print(d2)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5, 100]}
    

- 深いコピーを作る

  - コピー元に要素に含む配列/辞書について、参照状態を保持しない
  
.. code-block:: python

    >>> import copy
    >>> d1 = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d2 = copy.deepcopy(d1)
    >>> print(d1)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5]}
    >>> print(d2)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5]}
    >>> d1["list"].append(100)
    >>> print(d1)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5, 100]}
    >>> print(d2)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5]}


- 配列の要素をキーとして初期化する

.. code-block:: python

    >>> d = {}.fromkeys(["hoge", "foo", "baa"])
    >>> print(d)
    {'baa': None, 'foo': None, 'hoge': None}
    

- 値を取得する

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.get("hoge")
    100
    >>> d.get("test", 0)
    0
    >>> d["hoge"]
    100


- (KEY, VALUE) という形式で要素を取得する

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.items()
     dict_items([('hoge', 100), ('foo', 200), ('baa', 300), ('list', [1, 2, 3, 4, 5])])


- KEYをリストで取得する
  
.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.keys()
    dict_keys(['hoge', 'foo', 'baa', 'list'])


- KEYで指定したVALUEを辞書から取り出す

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.pop("hoge")
    >>> print(d)
    {'baa': 300, 'foo': 200, 'list': [1, 2, 3, 4, 5]}

  
- VALUEをリストで取得する
  
.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.values()
    dict_values([100, 200, 300, [1, 2, 3, 4, 5]])


- KEYで指定したVALUEを (KEY, VALUE) 形式で辞書から取り出す

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.popitem()
    ('list', [1, 2, 3, 4, 5])
    >>> print(d)
    {'baa': 300, 'foo': 200, 'hoge': 100}


- 指定したKEYがなかったら、デフォルト値を設定する。指定したKEYがあったら、設定しない

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.setdefault("test", 500)
    >>> print(d)
    {'baa': 300, 'foo': 200, 'hoge': 100, 'list': [1, 2, 3, 4, 5], 'test': 500}


- 辞書同士を結合する

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d.update({"hoge1": 100, "foo2": 200, "baa3": 300})
    >>> print(d)
    {'hoge': 100, 'foo': 200, 'baa': 300, 'list': [1, 2, 3, 4, 5], 'hoge1': 100, 'foo2': 200, 'baa3': 300}


例外
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 存在しないインデックスを指定したとき

.. code-block:: python

    >>> d = {"hoge": 100, "foo": 200, "baa": 300, "list": [1, 2, 3, 4, 5]}
    >>> d["test"]
    ---------------------------------------------------------------------------
    KeyError                                  Traceback (most recent call last)
    <ipython-input-85-aefdd90ece20> in <module>()
    ----> 1 d["test"]


