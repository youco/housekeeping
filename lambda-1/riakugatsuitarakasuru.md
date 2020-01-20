# リアク字がついたら何かする３

python 3.8

```python
import os
import json
import boto3
import hmac
import hashlib
from urllib.parse import parse_qs
import urllib.request
import logging
logger = logging.getLogger(__name__)
logger.setLevel(os.environ['LOG_LEVEL']) # 環境変数の設定値は大文字

def verify(event):
    # リクエストがSlackからのものかチェック
    # https://api.slack.com/docs/verifying-requests-from-slack

    signature = event['headers']['X-Slack-Signature']
    req = 'v0:' + event['headers']['X-Slack-Request-Timestamp'] + ':' + event['body']
    request_hash = 'v0=' + hmac.new(
        os.environ["SIGNING_SECRET"].encode(),
        req.encode(), hashlib.sha256
    ).hexdigest()
    logger.debug("sig："+ signature)
    logger.debug("req："+ request_hash)
    return hmac.compare_digest(request_hash, signature)

def post_slack():

    # 設定
    SLACK_POST_URL = WEBHOOK_GEN
    method = "POST"

    # メッセージの内容
    message = "Lambdaのテストです"
    send_data = {
        "text": message
    }

    send_text = ("payload=" + json.dumps(send_data)).encode('utf-8')

    request = urllib.request.Request(
        SLACK_POST_URL,
        data=send_text,
        method=method
    )
    with urllib.request.urlopen(request) as response:
        response_body = response.read().decode('utf-8')

    return response_body

    
def lambda_handler(event, context):
    logger.debug(json.dumps(event))

    if "X-Slack-Retry-Reason" in event["headers"]:
        logger.info("lambdaがリトライしようとしたので、予期せぬ処理とみなして終了")
        return {
            "statusCode": 200,
            "body": "retry"
        }

    if verify(event):
        logger.info("verify ok")
            
        # Bot自身の書き込みなら処理終了
        body = event['body']
        dict_body = json.loads(body)
        user = dict_body['event'].get('user')
        
        if user == os.environ["APP_ID"]:
            logger.info("Bot自身の書き込みのため処理を終了します")
            logger.debug(user)
            return { 'statusCode': 200 }

        # メッセージ書き込み処理呼び出し
        response = ""
        response = post_slack()
        return {
            "statusCode": 200,
            "body": response
            }
    else:
        logger.info("Error: verify request")
        return {"statusCode": 200,
            "body": "ng"
        }
        
    return {"statusCode": 200,
            "body": "ok"
        }

        
```

