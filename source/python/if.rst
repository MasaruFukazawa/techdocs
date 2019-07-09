条件分岐
========================================

文法
---------------------------------------

- if - elif - else で構成する

- 条件にマッチした場合の処理は、インデントしたブロックに記述する
  
.. code-block:: python

    if [条件文]:

        条件にマッチした時の処理を書く

    elif [条件文]:

        条件にマッチした時の処理を書く

    else:

        上の条件にマッチしなかった場合の処理を書く


比較演算子
---------------------------------------

================ ============
意味             演算子
================ ============
等しい           ==
等しくない       !=
より小さい       <
以下             <=
より大きい       >
以上             >=
配列の要素にある in ... 
================ ============


Trueとなる値・False となる値
---------------------------------------

============ ============
型           値
============ ============
ブール値     False
NULL         None
整数         0
浮動小数点数 0.0
文字列       ’’
リスト       []
タブル       ()
辞書         {}
集合         set()
============ ============

例
---------------------------------------

- 数値を比較する

.. code-block:: pythonA

    input_num = 100

    if input_num == 100:
        print("input: 100")

    elif input_num == 200:
        print("input: 200")

    elif input_num == 300:
        print("input: 300")

    else:
        print("no input")

	
- 文字列を比較する

.. code-block:: python

    color = "red"

    if color == "red":
        print("select red")

    elif color == "blue":
        print("select blue")

    elif color == "green":
        print("select green")

    else:
        print("no select")


- リストを比較する

.. code-block:: python
  
    colors = ["red", "blue", "green"]

    if color == ["red", "blue", "green"]:
        print("select red, blue, green")

    elif color == ["black", "white", "lime"]:
        print("select black, white, lime")

    elif color == ["yellow", "silver", "navy"]:
        print("select yellow, silver, navy")

    else:
        print("no select")
	

- 要素が含まれているか

.. code-block:: python

    # リスト / タブル / 辞書 の場合
    l = ["hoge", "foo", "baa"]

    if "hoge" in l:
        print("hoge が、リストの中にあります")


    # 辞書の場合は、KEYで判断する
    d = {"hoge": 1, "foo": 2, "baa": 3}

    if "hoge" in d:
        print("hoge が、辞書のKYEの中にあります")
