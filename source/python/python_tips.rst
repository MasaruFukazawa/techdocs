Python tips
========================================

テスト用メールサーバを立てる
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

実際にはメールは送信しない。

コンソールに出力されるだけ。

.. code-block:: sh

   python -m smtpd -n -c DebuggingServer localhost:1025
