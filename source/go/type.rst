型
===================================

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

- true
- false


文字列
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 不変のバイト列
- UTF-8でエンコードされたUnicodeコードポインタ(rune型)の列
- indexは、バイト列に対してのアクセス。文字単位ではない

.. code-block:: go

    var hello string = "Helow"
    world := "World"


合成型
-----------------------------------

配列
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 特定の型の0個以上の固定長列

.. code-block:: go

    var a [3]int

    // 初期値
    var a [3]int = [3]int{1, 2, 3}

    // 簡略
    a := [3]int{1, 2, 3}

    // 初期化時に要素数が決まる
    a := [...]int{1, 2, 3}

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

.. code-block:: go

    var a []int

    // 初期値
    var a []int = []int{1, 2, 3}

    // 簡略
    a := []int{1, 2, 3}


マップ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Pythonでいうところの辞書
- Keyの型 / Valueの型 を設定できる
- ループ時の順番は保証されていない
- Keyが存在しなければ、型の0値を得る

.. code-block:: go

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
    **masami = Employee{2, 'Masami'}



参照型
-----------------------------------



インターフェース型
-----------------------------------
