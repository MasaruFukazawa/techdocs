開発用にメールサーバを立ち上げる
=======================================

デバックサーバを立ち上げる
---------------------------------------

.. code-block:: bash

    python -m smtpd -n -c DebuggingServer localhost:1025

djangoで利用する場合
---------------------------------------

settings.py に以下を追記する

.. code-block:: bash

    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'localhost'
    EMAIL_PORT = 1025