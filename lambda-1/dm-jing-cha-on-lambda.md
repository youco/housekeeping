# リアク字がついたら、なにかする

#### 前提

slackeventsapi, requestsはLayerにて設定済み

## コード

```python
import logging
import os
import sys
import requests
from urllib import request, parse
from slackeventsapi import SlackEventAdapter

# Slack signing secret認証チェック
SIGNING_SECRET  = os.environ['SIGNING_SECRET']
slack_events_adapter = SlackEventAdapter(SIGNING_SECRET, endpoint="/slack/events")

# log setting
logger = logging.getLogger()
loglevel  = os.environ['LOG_LEVEL'] # 環境変数の設定値は大文字
logger.setLevel(loglevel)
logger = logging.getLogger()
formatter = logging.Formatter(
    '[%(levelname)s]\t%(aws_request_id)s\t%(filename)s\t%(funcName)s\t%(lineno)d\t%(message)s\n',
    '%Y-%m-%dT%H:%M:%S'
)
for handler in logger.handlers:
    handler.setFormatter(formatter)

# OAuth Access Token
TOKEN  = os.environ['TOKEN']
logger.info("token")

def lambda_handler(event, context):
    # メイン処理 postMessage
    logger.info("main")
    logger.debug(event)
    if ('challenge' in event):
        return {
            "statusCode": 200,
            "body": json.dumps({'challenge': event['challenge']})
            }
    else:
        post_result()
        return { "statusCode": 200 }
    
def post_result():
    url    = 'https://slack.com/api/chat.postMessage'
    params = {
        'token':     TOKEN,
        'channel':   "CPQ7RKK5Y",
        'text':      "test"
    }
    requestUrl = '{}?{}'.format(url, parse.urlencode(params))
    req = request.Request(requestUrl)
    
    with request.urlopen(req) as response:
       response_body = response.read().decode("utf-8")
    logger.info("END post")
    logger.info(str(response_body))
    
```

