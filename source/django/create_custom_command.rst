カスタムコマンドを作る
=======================================

- 作成したアプリケーション内に management/commands ディレクトリを作る
- commands ディレクトリにpythonファイルを作成する
	- pythonファイルがコマンド名になる

.. code-block:: bash

    作成したapp
    └── management
       └── commands
           └── hoge.py


- django.core.management.base.BaseCommand 継承する

.. code-block:: bash

    from django.core.management.base import BaseCommand, CommandError

    class Command(BaseCommand):

        def handle(self, *args, **options):
            #
            # 処理を書いていく
            #

参考URL
---------------------------------------

- https://docs.djangoproject.com/en/2.1/howto/custom-management-commands/
