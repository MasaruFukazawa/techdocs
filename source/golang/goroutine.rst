ゴルーチン & チャネル
===================================

- 並行性モデル : CSP(Communicating Sequential Processes) を用いている
	- 変数のほとんどの部分が、単一のプロセスに閉じ込められている

ゴルーチン
-----------------------------------

- Goでは、並行で実行されるプロセス(動作)をゴルーチン(goroutine)と呼ぶ
	- main関数のあるゴルーチンを、メインゴルーチンと呼ぶ
	- go文で呼び出した関数は、あたらしいゴルーチンで実行する
		- fork - execをやってくれるイメージ
	- main関数が終わると、その中で生成されたゴルーチンは終了する
		- ゾンビプロセスを作らない

.. code-block:: go

    package main

    import (
        "fmt"
        "time"
    )

    func main() {

        // 新しいgoルーチンを生成し、メインゴルーチンと並行して実行する
        // メインゴルーチンが完了すると、こちらも完了する
        go spinner(100 * time.Millisecond)

        const n = 45

        fibN := fib(n)

        fmt.Printf("\rFibonacci(%d) = %d\n", n, fibN)
    }

    func spinner(delay time.Duration) {
        for {
            for _, r := range `-\|/`{
                fmt.Printf("\r%c", r)
                time.Sleep(delay)
            }
        }
    }

    func fib(x int) int {

        if x < 2 {
            return x
        }

        return fib(x-1) + fib(x-2)

    }


チャネル
-----------------------------------

- ゴルーチン間の接続を行う
	- ゴルーチンが、他のゴルーチンに値を送るための仕組み
- チャンネルの要素型(element type)と呼ばれる特定の型の値のための導管
	- データ構造への参照
	- チャネルのゼロ値 : nil


宣言
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

同期型チャネル

.. code-block:: go

    // chは、int型の導管
    ch := make(chan int)

非同期型チャネル

.. code-block:: go

    // make関数の第二引数に、バッファサイズを指定する
    ch := make(chan int, 4)


データ送信
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    // 送信文
    ch <- x


データ受信
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    // 受信文
    x = <-ch


チャンネルを閉じる
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: go

    // チャネルを閉じる
    close(ch)
