django tips
========================================


既存ディレクトリ直下にプロジェクトを作る
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

hogeというディレクトリがすでにあり、以下のようにプロジェクトを作りたい場合

.. code-block:: sh

   hoge
   ├── manage.py
   └── prj
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py


hogeディレクトリで以下のようにコマンドを叩く。

.. code-block:: sh

   django-admin startproject app .



テスト用のSMTPサーバを設定する
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

デバックサーバを立ち上げる

.. code-block:: sh

   python -m smtpd -n -c DebuggingServer localhost:1025


settings.py に以下を追記する

.. code-block:: python

    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'localhost'
    EMAIL_PORT = 1025


ブラウザテストの実施
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

django.test.Client を使う。

.. code-block:: python

   from django.contrib.auth.models import User
   from django.test import Client, TestCase

  
   class HogeTestCase(TestCase):

       def setUp(self):

           self.user = User.objects.create_user('HogeTaro', 'taro@hoge.com', 'password')
        
           self.client = Client()

           self.client.login(username='HogeTaro', password='password')

       def test_foo(self):

           data = {
               'name': 'FooJiro',
               'email': 'jiro@foo.com',
           }

           response = self.client.post('[URL_Path]', data)

           self.assertEqual(200, response.status_code)


テストでユーザログインする
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Client.login メソッドを使ってログインする

.. code-block:: python

   from django.contrib.auth.models import User
   from django.test import Client, TestCase

  
   class HogeTestCase(TestCase):

       def setUp(self):

           self.user = User.objects.create_user('HogeTaro', 'taro@hoge.com', 'password')
        
           self.client = Client()

           self.client.login(username='HogeTaro', password='password')


テスト用にPOSTリクエストを作る
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

django.test.RequestFactory を使う。

.. code-block:: python

   from django.contrib.auth.models import User
   from django.test import Client, RequestFactory, TestCase

  
   class HogeTestCase(TestCase):

       def setUp(self):

           self.user = User.objects.create_user('HogeTaro', 'taro@hoge.com', 'password')
        
           self.client = Client()

           self.client.login(username='HogeTaro', password='password')


       def test_foo(self):

           data = {
               'name': 'FooJiro',
               'email': 'jiro@foo.com',
           }

           factory = RequestFactory()

           request = factory.post('[URL PATH]', data)

           # ログインユーザ設定
           request.user = self.user


本番化作業
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

settings.py の編集
----------------------------------------

.. code-block:: python

   DEBUG = True
   ALLOWED_HOSTS = []
   .
   .
   .
   # Static files (CSS, JavaScript, Images)
   # https://docs.djangoproject.com/en/2.0/howto/static-files/ 

   STATIC_URL  = '/static/'

   #STATIC_ROOT = os.path.join(BASE_DIR, "static")

   STATICFILES_DIRS = [
       os.path.join(BASE_DIR, "static"),
   ]

を

.. code-block:: python

   DEBUG = False
   ALLOWED_HOSTS = ['*']
   .
   .
   .
   # Static files (CSS, JavaScript, Images)
   # https://docs.djangoproject.com/en/2.0/howto/static-files/ 

   STATIC_URL  = '/static/'

   STATIC_ROOT = os.path.join(BASE_DIR, "static")

   STATICFILES_DIRS = [
       os.path.join(BASE_DIR, "static"),
   ]


静的ファイルの集約
----------------------------------------

.. code-block:: python

    $ python manage.py collectstatic

- STATICFILES_DIRS から STATIC_ROOT 指定のフォルダに静的ファイルが集約される

  - 開発時点から集約されているのであれば、この作業は不要


gunicorn サーバ 起動
----------------------------------------

.. code-block:: python

    .
    └── app
         ├── __init__.py
         ├── settings.py
         ├── urls.py
         └── wsgi.py

- プロジェクトフォルダ内で以下のスクリプトを叩く

- port 8000 で起動する

.. code-block:: python

   $ gunicorn app.wsgi &


nginx の vhost 設定
----------------------------------------

.. code-block:: python

    upstream app_server {
        server 127.0.0.1:8000 fail_timeout=0;
    }

    server {
        listen       80;
        server_name  [ホスト名];

        # HTTPS以外でアクセスした場合はHTTPSを強制します
        if ($http_x_forwarded_proto != https) {
            set $https_c 1;
        }

        # ELBのヘルスチェックはHTTPSを強制しません
        if ($http_user_agent = "ELB-HealthChecker/1.0") {
            set $https_c 0;
        }
    
        # HTTPS強制が必要な場合、httpsでリダイレクトします
        if ( $https_c = 1 ) {
            return 301 https://[URL]$request_uri;
        }

        # IPアドレスをチェックします
        # ELBのヘルスチェックの場合もBASIC認証なしにします
        if ($http_user_agent = "ELB-HealthChecker/1.0") {
            set $auth off;
        }
    
        # アクセスしてきたら、小さい画像を返す
        location /health.html {
            empty_gif;
            access_log off;
            break;
        }

        # 静的ファイルは、djangoを通さない。
        location /static {
            alias [静的ファイルパス];
            expires 5h;
        }
    
        location / {
    
            # Basic認証設定
            auth_basic "Restricted";
            auth_basic_user_file /etc/nginx/.htpasswd;
    
            # プロキシ設定
            # 80 -> 8000 にリクエストを回す
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            proxy_redirect off;
            proxy_pass   http://app_server;
    
        }

    }
