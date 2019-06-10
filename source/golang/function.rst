関数
===================================

定義
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    func name (parameter1 type, parameter2 type, ... ) return_value_type1, return_value_type2, ... {
        
        return return_value1, return_value2, ...
    }


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