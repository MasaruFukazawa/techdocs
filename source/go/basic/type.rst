型
===================================

- 最小単位は、ビット
- 扱う単位は、ワード (固定長数)

基本型
-----------------------------------

整数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- int8/uint8
- int16/uint16
- int32/uint32
- int64/uint64
- rune
	- int32のシノニム
	- Unicodeのコードポインタとして使用される
- byte
	- uint8のシノニム
	- 生データであることを強調
- uintptr
	- ポインタ

二項演算子
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

算術演算子

.. csv-table:: 

    ＋, 和
    ー, 差
    ※, 積
    /, 除
    %, 余

比較演算子

.. csv-table:: 

    ==, 等しい, 参照型の場合は参照同一性を見る
    !=, 等しくない
    <, より小さい
    <=, 以下
    >, より大きい
    >=, 以上

ビット演算子

.. csv-table:: 

    &, ビットごとの積, AND
    ｜, ビットごとの和, OR
    ^, ビットごとの排他和, XOR
    &^, ビットクリア, AND NOT
    <<, 左シフト, x * ( 2 ^ n )
    >>, 右シフト, x / ( 2 ^ n )

優先順位

.. csv-table:: 

    ※, /, %, <<, >>, &, &^
    ＋, ー, ｜, ^
    ==, !=, <, <=, >, >=
    &&
    ||


浮動小数点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- float32
- float64

※ 浮動小数点の限界値は、mathパッケージに定義されている


複素数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- complex64
- complex128

.. code-block:: go

    var x complex128 = complex(1, 2) // 1 + 2i
    y := complex(1, 2) // 1 + 2i


ブーリアン
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 以下の2値のいずれか
    - true
    - false
- 短絡的(short-circuit)な振る舞いをもつ
    - 左オペランドが決定しているなら、あえて、右オペランドは評価しない

文字列
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 不変のバイト列
- UTF-8でエンコードされたUnicodeコードポインタ(rune型)の列
- indexは、バイト列に対してのアクセス。文字単位ではない

宣言

.. code-block:: go

    var hello string = "Hellow"
    world := "World"


部分文字列

.. code-block:: go

    hello[0:3]
    hello[0:]
    hello[3:]
    hello[:]

文字列結合

.. code-block:: go

    "Hellow" + " " + "World"

生文字リテラル

.. code-block:: go

    const GoUsage = `Go is a tool for managing Go source code.
        
    Usage:
        go command [arguments]
    `

エスケープシーケンス

.. csv-table:: 

    ¥a, アラート
    ¥b, バックスペース
    ¥f, フォームフィード
    ¥n, 改行
    ¥r, キャリッジリターン
    ¥v, 垂直タブ
    ¥', シングルクオート
    ¥", ダブルクオート


文字操作モジュール

.. csv-table:: 

    strconv, 文字列 <=> ブール値、整数値、浮動小数点数値 変換
    unicode, ルーン文字の分類にしよう



合成型
-----------------------------------

配列
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 特定の型の0個以上の固定長列
- 要素外にアクセスすると, panic になる

.. code-block:: go

    var a [3]int

    // 初期値
    var a [3]int = [3]int{1, 2, 3}

    // 簡略
    a := [3]int{1, 2, 3}

    // 初期化時に要素数が決まる
    a := [...]int{1, 2, 3}
    
    // インデックスを明示的に指定
    a := [...]string{0: "1", 1: "2", 2: "3"}

例 ) 繰り返し

.. code-block:: go

    // インデックスと要素を取得する
    for i, v := range a {
    }

    // 要素だけを取得する
    for _, v := range a {
    }


スライス
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 特定の型の可変長列
- 構成要素
	- ポインタ
	- 長さ
	- 容量 (capacity)
- 要素外にアクセスすると, panic になる

.. code-block:: go

    var a []int

    // 初期値
    var a []int = []int{1, 2, 3}

    // 簡略
    a := []int{1, 2, 3}

    // スライス演算子
    a[1:3]


マップ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Pythonでいうところの辞書
- ハッシュテーブルへの参照
- Keyの型 / Valueの型 を設定できる
- ループ時の順番は保証されていない
- Keyが存在しなければ、型のゼロ値を得る

.. code-block:: go

    // データ構造への参照(ポインタ)
    ages := make(map[string]int)

    ages['alice'] = 20
    ages['charlie'] = 19

    ages := map[string]int{
        'alice': 20,
        'charlie': 19
    }


構造体
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 合成データ型
- 型を持つ0個以上のフィールドをもつ
- フィールド名
    - 大文字始まり : 公開
    - 小文字始まり : 非公開
- フィールドは、各型の0値を持つ

.. code-block:: go

    type Employee struct {
        ID        int
        Name      string
        Address   string
        DoB       time.Time
        Position  string
        Salary    int
        ManagerID int
    }

    var ponsuke Employee

    masaru := &Employee{1, 'Masaru'}

    masami := new(Employee)
    *masami = Employee{2, 'Masami'}

    // 無名フィールド
    type Point struct {
        X, Y int
    }

    type Circle struct {
        // ↓ フィールド名を省略できる
        // Circle.X / Circle.Y で参照できる
        Point
        Radius int
    }

    var c1 Circle
    c.X = 5
    c.Y = 5
    c.Radius = 5

    c2 := Circle{
        Point{ 5, 5},
        5
    }


参照型
-----------------------------------

ポインタ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- C言語と同じ宣言と使い方
- どの型に対するポインタも、ゼロ値はnil
- 関数で、関数内のローカル変数のポイントを返すのはあり
	- ポインタは、関数内のローカル変数を指す

.. code-block:: go

	x := 1
	px := &x
	*px


new関数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- C言語で言うところのmalloc関数的なやつ

.. code-block:: go

    p := new(int)

- 引数の型のポインタを返す
- *pはゼロ値
- newで宣言した場合、一意のポインタを返す
- struct{}, [0]int などの何の情報も含まない大きさがゼロの同じ型の変数は、同じアドレスを持つ可能性がある


インターフェース型
-----------------------------------

- 抽象型 (Abstract Type)

	- 型として満たすためにもっておくメソッドの定義するだけ

        - 関数名 / 引数 / 戻り値

例: Go言語でつくるインタプリタ より

.. code-block:: go

    type Node interface {
        // Nodeが提供すべきメソッド
        TokenLiteral() string
        String() string
    }

    // AST(抽象構文木1)のルートとなる構造体
    // .. Program データ型は、Nodeインターフェースを満たす
    // .. TokenLiteral / String メソッドを実装しているため
    type Program struct {
        Statements []Statement
    }

    func (p *Program) TokenLiteral() string {

        if len(p.Statements) > 0 {
            return p.Statements[0].TokenLiteral()
        } else {
            return ""
        }

    }

    func (p *Program) String() string {

        var out bytes.Buffer

        for _, s := range p.Statements {
            out.WriteString(s.String())
        }

        return out.String()
    }

型アサーション
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    x.(T)


型宣言
-----------------------------------

.. code-block:: go

    type 名前 基底型