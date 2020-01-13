---
description: sign-in-event-monitor-python
---

# コンソールアクセス時にSlackへ通知

## ❗ 注意 ❗ 

※無料枠で利用する場合は、S3へのアクセスが頻繁になり枠を超過する恐れがあるのでおすすめしない。

## 事前準備

CloudTrailとCloudwatchを連携させておくこと。

→Cloudwatch側でログイン情報が見れず、エラーになる。

## Lambda変数（Python2.7）

```text
# -*- encoding:utf-8 -*-
import os
import json
import commands
import urllib

def lambda_handler(event, context):
    print("Received event: " + json.dumps(event))
    message = create_message(event['detail'])
    web_hook_url = os.environ['env']
    return notify(message, "dddd", web_hook_url)

def create_message(detail):
    user_name = get_user_name(detail['userIdentity'])
    event_time = detail['eventTime']
    event_name = detail['eventName']
    event_result = detail['responseElements'][event_name]

    message = "AWSコンソールへのログインを検知しました\n" \
            + "・ユーザ名：" + user_name + "\n" \
            + "・イベント名：" + event_name + "\n" \
            + "・結果：" + event_result + "\n" \
            + "・発生時刻：" + event_time
    return message

def get_user_name(user_identity):
    if user_identity['type'] == 'Root':
        return 'root'
    elif user_identity['type'] == 'IAMUser':
        return user_identity['userName']
    else:
        # RootアカウントとIAM User以外のパターンがあるかどうかわからないが念のため
        return json.dumps(user_identity)

def notify(message, channel, web_hook_url):
    payload = {
        "text": message,
        "channel": channel,
        "username": "AWSアカウントモニターBot",
        "icon_emoji": ":ghost:"
    }
    escaped_payload = urllib.quote_plus(json.dumps(payload).encode('utf-8'))
    curl_command = 'curl -s -X POST -d "payload=%s" %s' % (escaped_payload, web_hook_url)
    return commands.getoutput(curl_command)

```

環境変数：env:Slack Webhook URL

ハンドラ：lambda\_function.lambda\_handler

実行ロール：lambda\_execution\_custom

タイムアウト：1min

同時実行：10

## 参考

{% embed url="https://engineer.crowdworks.jp/entry/2016/11/01/000000" %}





