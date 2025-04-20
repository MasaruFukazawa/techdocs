コマンドライン引数
========================================

.. code-block:: go

    $ emacs args.go
    package main

    import (
        "fmt"
        "os"
    )

    func main() {

        fmt.Println(os.Args)

        for i, arg := range os.Args[1:] {
            fmt.Printf("%d : %s\n", i, arg)
        }

        // インデックスを使わない時、_ をつかう                                                                                                                                                                                                                                   
        for _, arg := range os.Args[1:] {
            fmt.Println(arg)
        }

    }

.. code-block:: go

    $ go run args.go hoge foo baa 
    [/var/folders/wy/dkb62gvd6fb73cvw1fhzn1h40000gn/T/go-build967091332/b001/exe/args hoge foo baa]
    0 : hoge
    1 : foo
    2 : baa
    hoge
    foo
    baa