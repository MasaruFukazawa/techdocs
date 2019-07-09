Gin Web Framework 入門
=======================================

参考サイト
---------------------------------------

- https://github.com/gin-gonic/gin


フレームワーク インストール
---------------------------------------

.. code-block:: go

    $ go get -u github.com/gin-gonic/gin


基本形式
---------------------------------------

.. code-block:: go

    package main

    import "github.com/gin-gonic/gin"

    func main() {

        r := gin.Default()

        r.GET("/ping", func(c *gin.Context) {
            c.JSON(200, gin.H{
                "message": "pong",
            })
        })

        // listen and serve on 0.0.0.0:8080                                                                                                                                                                                                                                       
        r.Run()
}


Govendor
---------------------------------------

- サードパーティパッケージの管理ツール


