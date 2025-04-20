関数
========================================

文法
---------------------------------------

- 引数なし関数

.. code-block:: python

    # 関数定義
    def echo():
        print("Hello World !!")
    
    # 関数呼び出し
    echo()

    "Hello World !!"


- 位置引数関数

.. code-block:: python

    def set_menu(wine, entree, dessert):
        return {"wine": wine, "entree": entree, "dessert": dessert}
    
    menu = set_menu("rose", "beef", "cake")

    print(menu)
    {'wine': 'rose', 'entree': 'beef', 'dessert': 'cake'}


- キーワード引数関数

  - 値を引数として渡す時に、引数名を指定できる
  
.. code-block:: python
		
    def set_menu(wine, entree, dessert):
        return {"wine": wine, "entree": entree, "dessert": dessert}
    
    menu = set_menu(entree="beef", dessert="cake", wine="rose")

    print(menu)
    {'wine': 'rose', 'entree': 'beef', 'dessert': 'cake'}


- デフォルト引数関数

  - 引数の値にデフォルトで値を指定することができる

.. code-block:: python

    def set_menu(wine, entree, dessert="pudding"):
        return {"wine": wine, "entree": entree, "dessert": dessert}
    
    menu = set_menu(entree="beef", wine="rose")

    print(menu)
    {'wine': 'rose', 'entree': 'beef', 'dessert': 'pudding'}


- ＊ による位置引数のタプル化

.. code-block:: python

    def set_menu(*args):
        print(args)

    set_menu("beef", "rose", "cake")

    ('beef', 'rose', 'cake')



- ＊＊ によるキーワード引数の辞書化

.. code-block:: python

    def set_menu(**kwargs):
        print(kwargs)
        
    set_menu(entree="beef", wine="rose", dessert="cake")

    {'entree': 'beef', 'wine': 'rose', 'dessert': 'cake'}


- ＊args、＊＊kwargs を併用する場合

  - 仮引数は、＊args、＊＊kwargs の順番。

  - 渡す引数の順番も、位置引数、キーワード引数の順番。
  
.. code-block:: python

    def set_menu(*args, **kwargs):
        print(args)
        print(kwargs)

    set_menu("beef", "rose", dessert="cake")

    ('beef', 'rose')
    {'dessert': 'cake'}

    
docstring について
---------------------------------------

docstring という仕組みを使えば、クラス / 関数定義のドキュメントをソース内に組み込むことができる。

関数名定義の直後に文字列を組み込む

.. code-block:: python

    def set_menu(wine, entree, dessert):
        """
	本日のメニューをセットする
	引数:
	    第1引数: ワイン
	    第2引数: アントレ
	    第3引数: デザート
	戻り値:
	    本日のメニューを辞書形式で返す
	"""

        return {"wine": wine, "entree": entree, "dessert": dessert}


    help(set_menu)

    # 以下、結果
    Help on function set_menu in module __main__:

    set_menu(wine, entree, dessert)
        本日のメニューをセットする
        引数:
            第1引数: ワイン
            第2引数: アントレ
            第3引数: デザート
        戻り値:
           本日のメニューを辞書形式で返す


オブジェクトとしての関数
---------------------------------------

Pythonでは、関数もオブジェクトとして扱えるため、クラス/関数に引数として渡すことができる

.. code-block:: python

  def add(x, y):
      return x + y


  def answer(calc_func, x, y):
      print(calc_func(x, y))


  answer(add, 10, 20) # => 30


関数内関数
---------------------------------------

.. code-block:: python

    def outer(x, y):

        def inner(i, j):
	    return i + j

	return inner(x, y)

    print(outer(100, 100)) # => 200


クロージャ
---------------------------------------


無名関数 / ラムダ関数
---------------------------------------


ジェネレーター
---------------------------------------


デコレータ
---------------------------------------

既存の関数の中身を書き換えずに、変更を加えたい時に使用する。

例 ) 関数のデバック文など

関数をデコレート（装飾）するための関数。

.. code-block:: python

    def document_it(func):

        def new_function(*args, **kwargs):

            print("Running function: ", func.__name__)
            print("Positional arguments: ", args)
            print("Keyword arguments: ", kwargs)

            result = func(*args, **kwargs)

            print("Result: ", result)

            return result

        return new_function


    @document_it
    def add_ints(a, b):
        return a + b


    if __name__ == "__main__":
        add_ints(10, 20)


結果

.. code-block:: python

    Running function:  add_ints
    Positional arguments:  (10, 20)
    Keyword arguments:  {}
    Result:  30
