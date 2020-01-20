# 新規チャンネル追加時にお知らせ

```python
import os
import json
import hmac
import hashlib
import urllib.request
import logging
# log setting
logger = logging.getLogger()
loglevel  = os.environ['LOG_LEVEL'] # 環境変数の設定値は大文字
logger.setLevel(loglevel)
logger = logging.getLogger()
formatter = logging.Formatter(
    '[%(levelname)s]\t%(filename)s\t%(funcName)s\t%(lineno)d\t%(message)s\n[%(aws_request_id)s]',
    '%Y-%m-%dT%H:%M:%S'
)
for handler in logger.handlers:
    handler.setFormatter(formatter)
    
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
    WEBHOOK_GEN = os.environ['WEBHOOK_GEN']
    SLACK_POST_URL = WEBHOOK_GEN
    method = "POST"

    # メッセージの内容
    message = "Lambdaのテストです created channel"
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

    #受信したjsonをLogsに出力
    logger.info(json.dumps(event))

    # json処理
    if 'body' in event:
        body = json.loads(event.get('body'))
    elif 'token' in event:
        body = event
    else:
        logger.error('unexpected event format')
        return {'statusCode': 500, 'body': 'error:unexpected event format'}

    #url_verificationイベントに返す
    if 'challenge' in body:
        challenge = body.get('challenge')
        logger.info('return challenge key %s:', challenge)
        return {
            'isBase64Encoded': 'true',
            'statusCode': 200,
            'headers': {},
            'body': challenge
        }

    if "X-Slack-Retry-Reason" in event["headers"]:
        logger.info("lambdaがリトライしようとしたので、予期せぬ処理とみなして終了")
        return { "statusCode": 200 }

    if verify(event):
        logger.info("verify ok")
        body = json.loads(event.get('body'))
        logger.debug(body)
        
        # Bot自身の書き込みなら処理終了
        creator = body['event'].get('channel').get('creator')
        logger.debug(creator)
        if creator == os.environ["APP_ID"]:
            logger.info("Bot自身の書き込みのため処理を終了します")
            return { 'statusCode': 200 }
            
        # 呼び出しイベント確認
        type = body['event'].get('type')
        logger.debug(type)
        if type != os.environ["type"]:
            logger.info("イベントタイプが異なるため処理を終了します")
            return { 'statusCode': 200 }        

        # メッセージ書き込み処理呼び出し
        response = ""
        response = post_slack()
        return { "statusCode": 200 }
        
    else:
        logger.info("Error: verify request")
        return {"statusCode": 200 }        
```

