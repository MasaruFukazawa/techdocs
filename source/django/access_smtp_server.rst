SMTPサーバ接続
===================================

settings.pyに記述する

.. code-block:: python

    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'stmp host name'
    EMAIL_PORT = 465 or 587 or 25
    EMAIL_HOST_USER = 'user name'
    EMAIL_HOST_PASSWORD = 'password'
    #EMAIL_USE_SSL = True
    #EMAIL_USE_TLS = True