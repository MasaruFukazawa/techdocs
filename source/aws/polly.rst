Amazon Polly
=======================================

前提条件
---------------------------------------

- アクセスキーにAmazonPollyFullAccess権限を付与しておく
- boto3 を使用

テキストを音声データに変換してMP3に保存する
---------------------------------------

.. code-block:: python

    #!/usr/bin/env python                                                                                                                                                                                                                                                           
    #-*- coding: utf-8 -*-                                                                                                                                                                                                                                                          

    from boto3 import client

    def main():
        """                                                                                                                                                                                                                                                                         
        """
        polly = client("polly")

        response = polly.synthesize_speech(Text="数字の中で、７だけが孤独なのよ。",
                                        OutputFormat="mp3",
                                        VoiceId="Mizuki")

        with open("sound.mp3", "wb") as fd:
            fd.write(response.get("AudioStream").read())


    if __name__ == "__main__":
        """                                                                                                                                                                                                                                                                         
        """
        main()