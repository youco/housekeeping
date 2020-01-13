# Singning Secretsを実装する

{% embed url="https://api.slack.com/docs/verifying-requests-from-slack" %}

## EventAPI用のライブラリ

{% embed url="https://github.com/slackapi/python-slack-events-api" %}

### ライブラリの呼び出し

```python
import os
import sys
from slackeventsapi import SlackEventAdapter

# Slack signing secret認証チェック
SIGNING_SECRET  = os.environ['SIGNING_SECRET']
slack_events_adapter = SlackEventAdapter(SIGNING_SECRET, endpoint="/slack/events")
```

## スラッシュコマンド用

インポートは`import slack_SigningSecret`

{% code title="slack\_SigningSecret.py" %}
```python
import os
import hmac
import hashlib

def verify_request(event):
    """
    リクエストがSlackからのものか確認する
    
    Parameters
    ----------
    event : dict
        API Gatewayイベント(slack slashコマンド）

    Returns
    -------
    request_hash : str
        環境変数に設定されたキーから生成したハッシュ値
    signature : str
        slackからの送信リクエストに含まれる署名
    
    Notes
    -----
    環境変数SIGNING_SECRETを定義し、Signing Secret(slack app > basic information)を設定する
    https://api.slack.com/docs/verifying-requests-from-slack
    """

    signature = event['headers']['X-Slack-Signature']
    req = 'v0:' + event['headers']['X-Slack-Request-Timestamp'] + ':' + event['body']
    request_hash = 'v0=' + hmac.new(
        os.environ["SIGNING_SECRET"].encode(),
        req.encode(), hashlib.sha256
    ).hexdigest()
    
    return hmac.compare_digest(request_hash, signature)

```
{% endcode %}



