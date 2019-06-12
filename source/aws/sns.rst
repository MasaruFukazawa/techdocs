Amazon SNS
=======================================

前提条件
---------------------------------------

- アクセスキーにAmazonSNSFullAccess権限を付与しておく
- boto3 を使用


SMSを送信する
---------------------------------------

.. code-block:: python

    import boto3

    sns = boto3.client("sns")

    phone_number = '+81[電話番号]'

    message = 'Test Message'

    message_attributes = {
        'AWS.SNS.SMS.SenderID': {
            'DataType': 'String',
            'StringValue': 'northshore' # 通知者表示に使用される送信者ID
        }
    }

    sns.publish(
        PhoneNumber=phone_number, 
        Message=message,
        MessageAttributes=message_attributes)