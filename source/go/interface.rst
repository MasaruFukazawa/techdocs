インタフェース
===================================

- インタフェースは、型の振る舞いについて一般化 / 抽象化を行う
    - インタフェース を満たす
        - 要求しているメソッドをすべて定義しているかどうか

例: Go言語でつくるインタプリタ より

.. code-block:: go

    type Node interface {
        // Nodeが提供すべきメソッド
        TokenLiteral() string
        String() string
    }

    // AST(抽象構文木1)のルートとなる構造体
    // .. Program データ型は、Nodeインターフェースを満たす
    // .. TokenLiteral / String メソッドを実装しているため
    type Program struct {
        Statements []Statement
    }

    func (p *Program) TokenLiteral() string {

        if len(p.Statements) > 0 {
            return p.Statements[0].TokenLiteral()
        } else {
            return ""
        }

    }

    func (p *Program) String() string {

        var out bytes.Buffer

        for _, s := range p.Statements {
            out.WriteString(s.String())
        }

        return out.String()
    }