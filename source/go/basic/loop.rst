ループ
===================================

for ループ
-----------------------------------

.. code-block:: go

    for [initialization]; [condition]; [post] {

    }

.. code-block:: go

    package main

    import (
        "fmt"
        "os"
    )

    func main() {

        fmt.Println(os.Args)

        for i:=1; i < len(os.Args[1:]); i++ {
            fmt.Printf("%d : %s\n", i, os.Args[i])
        }

        for i, arg := range os.Args[1:] {
            fmt.Printf("%d : %s\n", i, arg)
        }

        // インデックスを使わない時、_ をつかう                                                                                                                                                                                                                                   
        for _, arg := range os.Args[1:] {
            fmt.Println(arg)
        }

    }


while ループ
-----------------------------------

.. code-block:: go

    while [condition] {

    }


無限ループ
-----------------------------------

.. code-block:: go

    for {

    }
