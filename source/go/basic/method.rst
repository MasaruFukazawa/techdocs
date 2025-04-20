メソッド
===================================

- 特定の型に紐づく関数群のこと

.. code-block:: go

    package main

    import (
        "fmt"
    )

    type Point struct {
        X, Y float64
    }

    // ポインタレシーバーによるメソッドの宣言
    // レシーバー変数を更新する場合、ポインタレシーバーを設定する必要がある
    // .. p *Point の部分 : レシーバー
    // .. ScaleBy  の部分 : セレクター
    //
    func (p *Point) ScaleBy(factor float64) {
        p.X *= factor
        p.Y *= factor
    }

    func main() {

        // パターン1                                                                                                                                                                                                                                                 
        p := new(Point)

        p.X = 200
        p.Y = 100

        fmt.Printf("X:%f / Y:%f \n", p.X, p.Y)

        p.ScaleBy(0.1)

        fmt.Printf("X:%f / Y:%f \n", p.X, p.Y)


        // パターン2                                                                                                                                                                                                                                                         
        q := Point{X:10, Y:1}

        fmt.Printf("X:%f / Y:%f \n", q.X, q.Y)

        q.ScaleBy(10)

        fmt.Printf("X:%f / Y:%f \n", q.X, q.Y)


        // パターン3                                                                                                                                                                                                                                                         
        pp := &Point{X:10, Y:1}

        fmt.Printf("X:%f / Y:%f \n", pp.X, pp.Y)

        pp.ScaleBy(10)

        fmt.Printf("X:%f / Y:%f \n", pp.X, pp.Y)

    }


カプセル化
-----------------------------------

- 変数/メソッドの名前を小文字始まりにする

- 外部から変数/メソッドを操作できなくする