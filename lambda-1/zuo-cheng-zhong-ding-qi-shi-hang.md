---
description: 関数名：echobot
---

# 【作成中】定期実行

## トリガー：Cloudwatch Events

{% embed url="https://us-east-1.console.aws.amazon.com/cloudwatch/home?region=us-east-1\#rules:" %}

Cloudwatch＞ルールの作成

## 関数：Python3.6

* [ ] Slackへのポスト形式が古いので、あとでなおす 💪 

```text
import json
import urllib.request

def lambda_handler(event, context):
    # TODO implement
    post_slack()
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }

def post_slack():
    message = """
    てすと
    """

    send_data = {
        "text": message
    }
    send_text = "payload=" + json.dumps(send_data)
     request = urllib.request.Request(
        "https://xxxxxxxxxxxxxxxxxxx", 
        data=send_text.encode('utf-8'), 
        method="POST"
    )
    with urllib.request.urlopen(request) as response:
        response_body = response.read().decode('utf-8')
```

{% embed url="https://console.aws.amazon.com/lambda/home?region=us-east-1\#/functions/echobot?tab=configuration" %}



