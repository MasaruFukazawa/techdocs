ハッシュ と 暗号
========================================

ハッシュ
----------------------------------------

元データから、特定サイズ ( bit数 ) の別データを計算によって生成すること

.. blockdiag::
   :desctable:

   blockdiag {
     // Set numbered-badge and description to nodes.
     A [numbered = 1, shape = "flowchart.input", label = "文字列", description = "任意長の文字列"];
     B [numbered = 2, label = "ハッシュ関数", description = "SHA-512/SHA-256/MD5"];
     C [numbered = 3, shape = "flowchart.input", label = "固定長bitデータ", description = "固定長bitデータ"];

     A -> B -> C;
   }


特徴
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 使うハッシュ関数が同じならば、同じもとデータからは、同じハッシュ値が作られる

- どんなに長い文字でも、ハッシュ関数の指定したbitサイズになる

  - この特性を生かし、ハッシュ値のことを元データの「ダイジェスト(要約)」を呼ぶ

- 不可逆

  - ハッシュ値からもとのデータに戻すことはできない

- シノニムの発生率が低い

  - ちがう値から同一のハッシュ値が出てしまう可能性が極めて低い

  - シノニムの発生率の低さがハッシュ値の性能の良さ

- 入力するデータが1文字違うだけで、全く異なるハッシュ値を出力する

  - 暗号学的ハッシュ値の特製


SAH-256 ハッシュを用いた例
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 256bitサイズのデータを出力している

  - 32Byte のデータ (16進数で表示しているため、64文字になっている)

- hello world と hallo world から出力されるハッシュ値に注目

.. code-block:: python
   :linenos:

   In [1]: import hashlib

   In [2]: text = b"hello world"

   In [3]: hash_text = hashlib.sha256(text).hexdigest()

   In [4]: print(hash_text)
   b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9

   In [5]: text = b"hallo world"

   In [6]: hash_text = hashlib.sha256(text).hexdigest()

   In [7]: print(hash_text)
   ad9093910d289561186b373cb03716af5dd0d602c717ee640243f3d6a25fd6b7


用途
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

改竄検知
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**ハッシュを使わない場合**

[Aさん] から [Bさん] にメッセージを送る

- [Aさん] ==> [メッセージ] ==> [Bさん]

この時、[Aさん] と [Bさん] の間に [盗聴者] が存在し、メッセージを改竄されてしまうと

- [Aさん] ==> [メッセージ] ==> [盗聴者] ==> [改竄メッセージ] ==> [Bさん]

Bさん は改竄されたメッセージを受け取ることになってしまう


**ハッシュを使った場合**

[Aさん]は、[Bさん] にメッセージを送る前にメッセージからハッシュ値を求める

- [メッセージ] ==> [ハッシュ関数] ==> [メッセージのハッシュ値]

[Aさん] から [Bさん] にメッセージとメッセージのハッシュ値を両方送る

- [Aさん] ==> [メッセージ] ==> [Bさん]

- [Aさん] ==> [メッセージのハッシュ値] ==> [Bさん]

[Bさん]は受け取った [メッセージ] からハッシュ値を求める

- [メッセージ] ==> [ハッシュ関数] ==> [メッセージのハッシュ値]

上記で求めたハッシュ値と[Aさん]からもらった、ハッシュ値が一致すれば、メッセージは改竄されることなく届けれらたと判断できる

- もし、[メッセージ] が改竄されていた場合、ハッシュ値が異なるので、改竄されたと判断できる



暗号
----------------------------------------

- ルール(暗号化アルゴリズム) に従って、元の文字列を解読が困難な文字列に変換できる

- ルール(復号化アルゴリズム) に従って、解読が困難な文字列を元の文字列に変換できる

- 上記のことから、ルールが知られれば、暗号化された文章を、元の文章に戻すことができる

  - 暗号化とは、 **時間稼ぎ** である



**暗号化**
    
.. blockdiag::
   :desctable:

   blockdiag {
     // Set numbered-badge and description to nodes.
     A [numbered = 1, shape = "flowchart.input", label = "文字列", description = ""];
     B [numbered = 2, label = "ルール", description = "暗号化アルゴリズム"];
     C [numbered = 3, shape = "flowchart.input", label = "暗号化文字列", description = ""];

     A -> B -> C;
   }


**復号化**
   
.. blockdiag::
   :desctable:

   blockdiag {
     // Set numbered-badge and description to nodes.
     A [numbered = 1, shape = "flowchart.input", label = "暗号化文字列", description = ""];
     B [numbered = 2, label = "ルール", description = "復号化アルゴリズム"];
     C [numbered = 3, shape = "flowchart.input", label = "文字列", description = ""];

     A -> B -> C;
   }
   


暗号アルゴリズムと鍵
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- 
