テスト
=======================================

- ソースコードと同じディレクトリに置く

- ファイル名に、 _test.go をつける


テスト実行コマンド
-----------------------------------

.. code-block:: go

    $ go test テスト対象ディレクトリパス
    PASS
    ok  	monkey/lexer	0.008s


記述方法
-----------------------------------

sample.go

.. code-block:: go

    package sample

    func add(x1, x2 float64) float64 {
        return x1 + x2
    }


sample_test.go

.. code-block:: go

    package sample

    import (
        "testing"
    )


    func TestAdd(t *testing.T) {

        tests := []struct{
            x1     float64
            x2     float64
            result float64
        }{
            {1, 1, 2},
            {2, 2, 4},
            {3, 3, 6},
            {4, 4, 8},
        }

        for _, tt := range tests {

            if tt.result != add(tt.x1, tt.x2) {
                t.Error("計算間違い！")
            }

        }

    }