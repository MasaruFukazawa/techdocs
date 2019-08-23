関数
===================================

定義
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    func name (parameter1 type, parameter2 type, ... ) return_value_type1, return_value_type2, ... {
        
        return return_value1, return_value2, ...
    }


- 関数の型を、シグニチャ (signature) と呼ぶ
- 引数は、値渡し
    - ポインタ, スライス, マップ, 関数, チャネル は、参照渡し


エラーを返す場合
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    // 2つめの戻り地で、err (0 or 1) を取得するとき
    result, err := func_name(argv1, argv2, argv3, argv4)

    // エラーを無視するとき
    result, _ := func_name(argv1, argv2, argv3, argv4)


関数値
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ファーストクラス値 (first-class value)
- 値として持てる


無名関数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    func squares() func() int {

        var x int

        return func () int {
            x++
            return x * x
        }
    }

    f := func1()
    f()


可変個引数関数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


関数の遅延呼び出し
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 関数が終わるタイミングで呼び出す処理を指定するとよい

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        hello_world()
    }

    func hello_world() {

        // 遅延呼び出し
        // 関数の終わりに呼び出される
        defer world()

        fmt.Printf("hello ")

    }

    func world() {
        fmt.Printf("world\n")
    }
