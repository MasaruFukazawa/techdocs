Amazon Rekognition
=======================================

前提条件
---------------------------------------

- アクセスキーにAmazonRekognitionFullAccess権限を付与しておく
- boto3 を使用

画像の節度を検査してみる
---------------------------------------

サンプルコード

.. code-block:: python

    #-*- coding: utf-8 -*-                                                                                                                                                                                                                                                          
    #!/usr/bin/env python                                                                                                                                                                                                                                                           

    from boto3 import client


    def detect_moderation_labels(file_name):
        """                                                                                                                                                                                                                                                                         
        """
        rekognition = client('rekognition', region_name='us-west-2')

        response = rekognition.detect_moderation_labels(
            Image={
                'S3Object': {
                    'Bucket': '[バケット名]',
                    'Name': file_name,
                }
            },
        )

        return response


    def main():
        """                                                                                                                                                                                                                                                                         
        """
        print(detect_moderation_labels('ファイル名'))


    if __name__ == "__main__":

        main()

岸明日香画像を読み込ませた結果

.. code-block:: python

    {
        'ModerationLabels': [
            {
                'Confidence': 83.82125854492188, 
                'Name': 'Suggestive', 
                'ParentName': ''
            }, 
            {
                'Confidence': 83.82125854492188,
                'Name': 'Female Swimwear Or Underwear',
                'ParentName': 'Suggestive'
            }
        ],
        'ResponseMetadata': {
            'RequestId': '3bf428ca-ba01-11e7-a7d0-8fe3bd264e50', 
            'HTTPStatusCode': 200, 
            'HTTPHeaders': {
                'content-type': 'application/x-amz-json-1.1', 
                'date': 'Thu, 26 Oct 2017 03:53:31 GMT', 
                'x-amzn-requestid': '3bf428ca-ba01-11e7-a7d0-8fe3bd264e50', 
                'content-length': '188', 
                'connection': 'keep-alive'
            }, 'RetryAttempts': 0
        }
    }