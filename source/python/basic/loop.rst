繰り返し
========================================

文法
---------------------------------------

- for ループ

 - 文字列/リスト/タブル/辞書/集合の要素分、ループし続ける

 - elem : ループの各要素をループ毎に取得できる
  
.. code-block:: python

    for elem in [文字列/リスト/タブル/辞書/集合]:

        ループ内で実施した処理を書く
	・
	・
	・


- while ループ

 - 条件文が、True の間、ループし続ける
  
.. code-block:: python

    while [条件文]:

        ループ内で実施した処理を書く
	・
	・
	・

例
---------------------------------------

- 文字列のループ

.. code-block:: python

    >>> for elem in "hoge":
    >>>     print(elem)
    h
    o
    g
    e


- リスト/タブル/集合のループ

.. code-block:: python

    >>> for elem in ["hoge", "foo", "baa"]:
    >>>     print(elem)
    hoge
    foo
    baa


- 辞書のループ

.. code-block:: python

    >>> for elem in {"hoge": 100, "foo": 200, "baa": 300}:
    >>>     print(elem)
    hoge
    foo
    baa

    >>> for k, v in {"hoge": 100, "foo": 200, "baa": 300}.items():
    >>>     print(k, v)
    hoge 100
    foo 200
    baa 300


- while ループ

.. code-block:: python

    >>> l = ["hoge", "foo", "baa"]
    >>> i = 0
    >>>     
    >>> while i < len(l) :
    >>>     print(l[i])
    >>>     i += 1
    hoge
    foo
    baa

    >>> i = 0
    >>> sum = 0
    >>>
    >>> while i < 11:
    >>>     sum += i
    >>>     i += 1
    >>>
    >>>  print(sum)
    55

		
continue 文
---------------------------------------

- continue 文以降の処理を行わずに、ループの先頭に戻る

.. code-block:: python

    >>> for elem in {"hoge": 100, "foo": 200, "baa": 300}:
    >>>
    >>>    if elem == "foo":
    >>>        continue
    >>>
    >>>    print(elem)
    >>>
    hoge
    baa


break 文
---------------------------------------

- ループを抜ける

.. code-block:: python

    >>> for elem in {"hoge": 100, "foo": 200, "baa": 300}:
    >>>
    >>>    if elem == "foo":
    >>>        break
    >>>
    >>>    print(elem)
    >>>
    hoge


else 文
---------------------------------------

- break されずにループ処理が完了したら実行するブロック

.. code-block:: python

    >>> for elem in {"hoge": 100, "foo": 200, "baa": 300}:
    >>>
    >>>    if elem == "test":
    >>>        break
    >>>
    >>> else:
    >>>    print("complate")
    >>>
    complate


range を使った数値シーケンスの生成
---------------------------------------

- range:  指定した数値-1までのリスト型のオブジェクトを返す
    
.. code-block:: python

    # 終了のみを指定する。
    >>> for i in range(101):
    >>>    print(i)
    0
    .
    .
    .
    100

    # 開始と終了を指定する。
    >>> for i in range(90, 101):
    >>>    print(i)
    90
    .
    .
    .
    100

    # 開始と終了と間隔を指定する。
    >>> for i in range(0, 11, 2):
    >>>     print(i)
    0
    2
    4
    6
    8
    10


zip()を使った反復処理
---------------------------------------

- 複数のシーケンスをまとめて処理できる
    
.. code-block:: python

    >>> days = ["Monday", "Tuesday", "Wendnesday"]
    >>> fruits = ["banana", "orange", "peach"]
    >>> drints = ["coffee", "tea", "beer"]
    >>>
    >>> for day, fruit, drink in zip(days, fruits, drints):
    >>>     print(day, gruit, drink)
    >>>
    Monday banana coffee
    Tuesday orange tea
    Wendnesday peach beer


リスト内包表記
---------------------------------------

- 一般的なやり方

.. code-block:: python

    >>> nums = []
    >>> for i in range(11):
    >>>     nums.append(i)
    >>>
    >>> print(nums)
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]


- パイソニックなやり方

.. code-block:: python

    >>> nums = [i for i in range(11)]
    >>> print(nums)
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]


- 辞書 / 集合 について同様の表記ができる。



