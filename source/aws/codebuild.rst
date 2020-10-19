AWS Code Build
=======================================

- CI ツール

- できること
  
  - コードのビルド

  - テスト/静的解析/コーディングスタイルチェック

    - 各言語のツールを使用する

URL
---------------------------------------
      
https://ap-northeast-1.console.aws.amazon.com/codesuite/codebuild/start?region=ap-northeast-1
      
ソースコードの入力元
---------------------------------------

- Code Commit

- S3

- Github

- Bitbucket


buildspec.yml
---------------------------------------

- URL

  - https://docs.aws.amazon.com/ja_jp/codebuild/latest/userguide/build-spec-ref.html

- プロジェクトフォルダのルートに置く

- 以下の内容を記述する

  - install : 言語のランタイム、パッケージのインストール

    - ランタイム: runtime-versions
      
    - パッケージ: yum

  - pre_build : ビルドするために必要なパッケージのインストール

    - pip install --upgrade pip

    - pip install -r requestments.txt

  - build : ビルド

  - post_build : ビルド後の処理

    - ソースコードのコーディング スタイル チェック

    - ソースコードの静的解析

    - ソースコードの自動テスト


ビルドデータの出力先
---------------------------------------

- S3

- コンテナにPUSHすることも可能


Python サンプル
---------------------------------------

https://github.com/MasaruFukazawa/codebuild-py

**1. Pythonのソースコードを用意する**


