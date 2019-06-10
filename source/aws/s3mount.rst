S3マウント方法
=======================================

バケットを作成する
---------------------------------------

- AWSのコンソール/Cliで作成する


EC2 から S3 をマウントできるようにする
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

以下の2つの方法がある

- aws cli でユーザのアクセスキーを設定する

- IAM ロールをインスタンスに設定する


aws cli 環境を設定する
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    $ aws configure
    AWS Access Key ID [None]: ********************
    AWS Secret Access Key [None]: ****************************************
    Default region name [None]: ap-northeast-1
    Default output format [None]:

    
ロールの設定
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- S3をマウントしたいEC2インスタンスに AmazonS3FullAccess ロールを設定する


モジュールインストール
---------------------------------------

.. code-block:: bash

    $ export GOPATH=$HOME/go
    $ echo $GOPATH
    $ sudo yum install -y golang fuse
    $ go get github.com/kahing/goofys
    $ go install github.com/kahing/goofys


マウント先を作成する
---------------------------------------

.. code-block:: bash

    $ mkdir マウント先ディレクトリパス


uid / gid を取得する
---------------------------------------

.. code-block:: bash

    $ id
    uid=500(ec2-user) gid=500(ec2-user) groups=500(ec2-user),10(wheel),48(apache)


マウント
---------------------------------------

ec2-user でマウントするとき

.. code-block:: bash

    $ $GOPATH/bin/goofys --region ap-northeast-1  --dir-mode=0777 --file-mode=0777 --uid=500 --gid=500 バケット名 マウント先ディレクトリパス

sudo で ロート権限でマウントするとき ( ※ aws cli 環境 を設定する場合、/root/.aws がないとできない )

.. code-block:: bash

    $ sudo $GOPATH/bin/goofys --region ap-northeast-1 -o allow_other --dir-mode=0777 --file-mode=0777 --uid=500 --gid=500 バケット名 マウント先ディレクトリパス


オプション
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. csv-table:: 

    オプション, 説明, 値 例
    --region, S3のリージョンを指定, ap-northeast-1
    -o, システム上特別な設定でマウントにする時に指定, allow_other ( rootでマウントした場合、他のユーザーでも利用できるようにする )
    --dir-mode, ディレクトリのパーミッション, 0777
    --file-mode, ファイルのパーミッション, 0777
    --uid, マウントするユーザーIDを指定する, 500
    --gid, マウントするグループIDを指定する, 500


reboot時の自動マウント
---------------------------------------

.. code-block:: bash

    $ sudo emacs /etc/fstab
    /home/ec2-user/go/bin/goofys --region ap-northeast-1 -o allow_other --dir-mode=0777 --file-mode=0777 --uid=500 --gid=500 バケット名 マウント先


参考
---------------------------------------

- http://qiita.com/kooohei/items/a14f22cb0381342d1861
- http://dev.classmethod.jp/cloud/aws/how-to-use-s3fs-goofys/
- http://takeshiyako.blogspot.jp/2016/04/s3-mount-goofys.html