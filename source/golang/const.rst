定数 & enum
=======================================

定数
---------------------------------------

- 実行時にではなく、コンパイル時に評価される式

.. code-block:: go

    const pi = 3.14159

    // or

    const (
        e  = 2.718
        pi = 3.14159
    )


enum
---------------------------------------

.. code-block:: go

    type Weekday int // 型のシノニムを作る

    // 0,1,2,3,4,5,6 と値をふる
    const (
        Sunday Weekday = iota
        Monday
        Tuesday
        Wednesday
        Thursday
        Friday
        Saturday
    )