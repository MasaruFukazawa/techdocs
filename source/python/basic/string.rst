文字列
========================================

文字列の種類
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- UNICODE文字列:

  - Pythonのプログラム内部で扱う文字列。


- バイト文字列:

  - UNICODE文字列から各文字コードに変換されたバイト列表記の文字列。

    - 文字コード: UTF-8, EUC_JP, SHIFT-JIS など


.. code-block:: python

    # UNICODE文字列
    >>> uni_str = "パイソンはいいぞ！"

    >>> uni_str.encode("utf-8")
    b'\xe3\x83\x91\xe3\x82\xa4\xe3\x82\xbd\xe3\x83\xb3\xe3\x81\xaf\xe3\x81\x84\xe3\x81\x84\xe3\x81\x9e\xef\xbc\x81'

    >>> uni_str.encode("euc-jp")
    b'\xa5\xd1\xa5\xa4\xa5\xbd\xa5\xf3\xa4\xcf\xa4\xa4\xa4\xa4\xa4\xbe\xa1\xaa'

    >>> uni_str.encode("shift-jis")
    b'\x83p\x83C\x83\\\x83\x93\x82\xcd\x82\xa2\x82\xa2\x82\xbc\x81I'
    

UNICODE / バイト文字については、別途ページを割いて説明します。

Python3で文字列と行った場合は、「UNICODE文字列」だと思ってください。
    

文字列の作り方
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 単引用符 or 二重引用符 で囲む

- 複数行の文字列の作成は、三重引用符 で囲む


.. code-block:: python

    >>> print('パイソンはいいぞ！')
    'パイソンはいいぞ！'

    >>> print("パイソンはいいぞ！")
    'パイソンはいいぞ！'

    >>> print("""
    パイソンはいいぞ！
    パイソンはいいぞ！
    パイソンはいいぞ！
    """)
    パイソンはいいぞ！
    パイソンはいいぞ！
    パイソンはいいぞ！


文字列の操作
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- インタラクティブ・シェルを使用する場合、特殊文字(\nなど)は見たまま表示します

.. code-block:: python

    >>> 'spam eggs'
    'spam eggs'
    >>> 'spam\neggs'
    'spam\neggs'



- print 関数を使った場合

.. code-block:: python

    >>> print('spam eggs')
    spam eggs
    >>> print('spam\neggs')
    spam
    eggs



- 特殊文字(\nなど)を解釈したくない場合

.. code-block:: python

    # \\ をつける
    >>> print('spam\\neggs')
    'spam\neggs'

    # 文字列の前に r をつける
    >>> print(r'spam\neggs')
    'spam\neggs'


- 文字列を複数行にわたって記述したい場合

.. code-block:: python

    >>> print("""
    Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
    """)
    Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to


- 文字連結

.. code-block:: python

    >>> "hoge" + " " + "foo" + " " + "baa"
    'hoge foo baa'


- 文字繰返し

.. code-block:: python

    >>> "hoge" * 10
    'hogehogehogehogehogehogehogehogehogehoge'

    
文字列のスライス
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 文字列は、配列とみなして、一文字ずつ要素にアクセスすることができる。

.. code-block:: python

    >>> s = 'パイソンはいいぞ！'
    >>> s[0]
    'パ'
    
  
- 配列から、配列を取り出すことができる。

.. code-block:: python

    >>> s = 'パイソンはいいぞ！'
    >>> s[:4] # 終端指定の -1 要素目まで取得する
    'パイソン'
    >>> s[5:] # 始端指定から最後の要素まで取得する
    'いいぞ！'
    >>> s[1:4] # 始端指定要素から終端指定の -1 要素目まで取得する
    'イソン'


メソッド
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- 一文字目を大文字に

.. code-block:: python

    >>>"hoge foo bar".capitalize()
    'Hoge foo bar'


- 小文字に変換    

.. code-block:: python

    >>>"HoGe FoO bAr".casefold()
    'hoge foo bar'


- 文字列内に指定文字が何回でてくるか

  - 第二引数で、検索開始位置を指定できる

  - 第三引数で、検索終了位置を指定できる
  
.. code-block:: python

    >>> "ガルパンはいいぞ".count("ガルパン")
    1
    >>> "ガルパンはいいぞ".count("ガルパン", 4)
    0
    >>> "ガルパンはいいぞ".count("ガルパン", 0, 4)
    1


- 指定した文字コードのバイト文字列への変換

  - Pythonには、UNICODE文字列 / bytes文字列 という２つの文字列がある。
  
.. code-block:: python

    >>> "ガルパンはいいぞ".encode("utf-8")
    b'\xe3\x82\xac\xe3\x83\xab\xe3\x83\x91\xe3\x83\xb3\xe3\x81\xaf\xe3\x81\x84\xe3\x81\x84\xe3\x81\x9e'

    >>> b'\xe3\x82\xac\xe3\x83\xab\xe3\x83\x91\xe3\x83\xb3\xe3\x81\xaf\xe3\x81\x84\xe3\x81\x84\xe3\x81\x9e'.decode("utf-8")
    'ガルパンはいいぞ'
    

- 文字列の終端でマッチするか

  - 第二引数で、検索開始位置を指定できる

  - 第三引数で、検索終了位置を指定できる
  
.. code-block:: python

    >>> "ガルパンはいいぞ".endswith("いいぞ")
    True
    >>> "ガルパンはいいぞ".endswith("ガルパン")
    False
    >>> "ガルパンはいいぞ".endswith("ガルパン", 0, 4)
    True
    


- 文字列ないのタブをスペースに変換

  - デフォルト、8 スペース

.. code-block:: python

    >>> "ガルパンは\tいいぞ".expandtabs()
    'ガルパンは   いいぞ'
    >>> "ガルパンは\tいいぞ".expandtabs(10)
    'ガルパンは     いいぞ'


- 文字列全体でマッチする箇所があるか

  - マッチした箇所の先頭のインデックスを返す

  - マッチしなければ、-1 を返す

.. code-block:: python

    >>> "ガルパンはいいぞ".find("いいぞ")
    5
    >>> "ガルパンはいいぞ".find("いいぞ！")
    -1


- 用意したフォーマットどおりの文字列を生成する

.. code-block:: python

    >>> "{}はいいぞ！".format("ガルパン")
    'ガルパンはいいぞ！'

    >>> "{0}はいいぞ！".format("ガルパン")
    'ガルパンはいいぞ！'

    >>> "{0[0]}はいいぞ！".format(["ガルパン"])
    'ガルパンはいいぞ！'

    >>> "{0[anime]}はいいぞ！".format({"anime": "ガルパン"})
    'ガルパンはいいぞ！'

    >>> "{0} {1} {2}".format("hoge", "foo", "baa")
    'hoge foo baa'

    >>> "{2} {1} {0}".format("hoge", "foo", "baa")
    'baa foo hoge'

    # 辞書版
    >>>  "{anime}はいいぞ！".format_map({"anime": "ガルパン"})
    'ガルパンはいいぞ！'


- 文字列全体でマッチする箇所があるか

  - find と同様の機能

  - マッチした箇所の先頭のインデックスを返す

  - マッチしなければ、例外を発生させる
  
.. code-block:: python

    >>> "ガルパンはいいぞ".index("いいぞ")
    5
    >>> "ガルパンはいいぞ".index("！")
    ---------------------------------------------------------------------------
    ValueError                                Traceback (most recent call last)
    <ipython-input-136-33dd2510868f> in <module>()
    ----> 1 "ガルパンはいいぞ".index("！")

    ValueError: substring not found


- 文字/数字のみか （記号を含まない）

.. code-block:: python

    >>> "ほげ".isalnum()
    True
    >>> "ほげ1234".isalnum()
    True
    >>> "ほげ1234@".isalnum()
    False
    

- 文字のみか

.. code-block:: python

    >>> "ほげ".isalpha()
    True
    >>> "ほげ1234".isalpha()
    False


- 整数か

.. code-block:: python

    >>> "12345".isdecimal()
    True
    >>> "１２３４５６".isdecimal()
    True
    >>> "12345.6789".isdecimal()
    False
    >>> "ほげ".isdecimal()
    False

    # 
    >>> "v".isdigit()

    # 漢数字 OK
    >>>  "一".isnumeric()


- 保留

.. code-block:: python

    >>> str.isidentifier()
  
    
- 文字列が小文字のみで構成されているか

.. code-block:: python

    >>> "hoge foo baa".islower()
    True
    >>> "hoge Foo baa".islower()
    False


- 保留

.. code-block:: python

    >>> str.isprintable()



- 全|半スペース、タブのみか

.. code-block:: python

    >>> " ".isspace()
    True
    >>> "　".isspace()
    True
    >>> "\t".isspace()
    True
    >>> "ab".isspace()
    False
    >>> "a　b".isspace()
    False
    >>> "".isspace()
    False


- 単語の最初が大文字の文字列か

.. code-block:: python

    >>> "Hoge Foo Baa".istitle()
    True

    >>> "hoge foo baa".istitle()
    False


- 文字列が大文字のみか

.. code-block:: python

    >>> "HOGE FOO BAA".isupper()
    True
    >>> "HOGE FOO BAa".isupper()
    False


- 文字の連結

.. code-block:: python

    >>> "  ".join(["hoge", "foo", "baa"])
    'hoge  baa  foo'
    >>> "  ".join({"hoge":1, "foo":2, "baa":3})
    'hoge  baa  foo'


- 左寄せ

.. code-block:: python

    >>> "ほげ".ljust(10)
    'ほげ        '
    >>> "ほげ".ljust(10, 'a')
    'ほげaaaaaaaa'


- 文字を小文字にする

.. code-block:: python

    >>> "HOGE FOO BAA".lower()
    'hoge foo baa'


- 文字列を分割する

  - セパレート文字により、文字列を分割する

  - セパレート文字前文字列, セパレート文字, セパレート文字後文字列 のリストを返す

.. code-block:: python

    >>> "HOGE FOO BAA".partition(' ')
    ('HOGE', ' ', 'FOO BAA')


- 文字列の置換

.. code-block:: python

    >>> "HOGE FOO BAA HOGE".replace("HOGE", "FOO")
    "FOO FOO BAA FOO"

    # 第三引数で数値を指定した場合、その回数分だけ置換する
    >>> "HOGE FOO BAA HOGE".replace("HOGE", "FOO", 1)
    'FOO FOO BAA HOGE'


- 文字列の左からマッチする箇所があるか

  - マッチした箇所の先頭のインデックスを返す

  - マッチしなければ、-1 を返す

.. code-block:: python

    >>> "HOGE FOO BAA HOGE".rfind("HOGE")
    13
    >>> "HOGE FOO BAA HOGE".rfind("BAR")
    -1


- 文字列の左からマッチする箇所があるか

  - find と同様の機能

  - マッチした箇所の先頭のインデックスを返す

  - マッチしなければ、例外を発生させる
  
.. code-block:: python

    >>> "HOGE FOO BAA HOGE".rfind("HOGE")
    13
    >>> "HOGE FOO BAA HOGE".rfind("BAR")
    ---------------------------------------------------------------------------
    ValueError                                Traceback (most recent call last)
    <ipython-input-136-33dd2510868f> in <module>()
    ----> 1 "HOGE FOO BAA HOGE".rfind("BAR")

    ValueError: substring not found


- 右寄せ

.. code-block:: python

    >>> "ほげ".rjust(10)
    '        ほげ'
    >>> "ほげ".rjust(10, 'a')
    'aaaaaaaaほげ'


- 文字列を分割する

  - セパレート文字により、文字列を分割する

  - セパレート文字前文字列, セパレート文字, セパレート文字後文字列 のリストを返す

.. code-block:: python

    >>> "HOGE FOO BAA".rpartition(' ')
    ('HOGE FOO', ' ', 'BAA')


- 文字列を分割する

.. code-block:: python

    >>> "HOGE FOO BAA".split(' ')
    ['HOGE', 'FOO', 'BAA']
		
    >>> "HOGE FOO BAA".rsplit(' ')
    ['HOGE', 'FOO', 'BAA']

    >>> "HOGE\nFOO\nBAA".splitlines()
    ['HOGE', 'FOO', 'BAA']


- 文字列の始まりでマッチするか

  - 第二引数で、検索開始位置を指定できる

  - 第三引数で、検索終了位置を指定できる
  
.. code-block:: python

    >>> "ガルパンはいいぞ".startswith("いいぞ")
    False
    >>> "ガルパンはいいぞ".startswith("ガルパン")
    True
    >>> "ガルパンはいいぞ".startswith("ガルパン", 0, 4)
    True

    
- 左の半|全スペース、タブを削除する

.. code-block:: python

    >>> "\t　 ガルパンはいいぞ　 \t".lstrip()
    'ガルパンはいいぞ\u3000 \t'


- 右の半|全スペース、タブを削除する

.. code-block:: python

    >>> "\t　 ガルパンはいいぞ　 \t".rstrip()
    '\t\u3000 ガルパンはいいぞ'

    
- 左右の半|全スペース、タブを削除する

.. code-block:: python

    >>> "\t　　ガルパンはいいぞ　 \t".strip()
    'ガルパンはいいぞ'


- 小文字を大文字に / 大文字を小文字に
    
.. code-block:: python

    >>> "HoGe FoO bAr".swapcase()
    'hOgE fOo BaR'

    
- タイトル調にしてくれる

.. code-block:: python

    >>> "hoge foo bar".title()
    'Hoge Foo Bar'

    
- 小文字を大文字に変換

.. code-block:: python

    >>> "hoge foo bar".upper()
    'HOGE FOO BAR'


- 左側に0埋めしてくれる

.. code-block:: python

    >>> "ガルパンはいいぞ".zfill(20)
    '000000000000ガルパンはいいぞ'
    
