# Slack Eventを契機にLambdaを動かす

## Slack App作成

1. Slack App新規作成
2. WorkspaceにAppをインストール
3. OAuth & Permissionsで「 `reactions:read` 」を追加→Appを再インストール

## API gatewayとの疎通作成

1. Lambda関数を作成
2. 関数作成後、トリガーを追加＞API Gatewayを選択
3. 新規（REST\)＞セキュリティ：オープン
4. 作成したAPI Gatewayを選択し、API Gateway画面に遷移
5. プルダウン「アクション」で「APIのデプロイ」を選択（デプロイ先は、関数と同じステージ）
6. 作成したAPI GatewayのAPI エンドポイントURLをコピー

## SlackにEventを受信するためのテストコードを実装

```python
import json

def lambda_handler(event, context):
  print(json.dumps(event))
  if ('challenge' in event):
    return {
      "statusCode": 200,
      "body": json.dumps({'challenge': event['challenge']})
    }
  else: 
    return { "statusCode": 200 }
```

```python
import json
import os

def lambda_handler(event: dict, context):

    # EventのVerify用(lambdaプロキシ統合はチェックしない)
    if "challenge" in event:
        return event.get("challenge")
```

## APIエンドポイント情報を設定

1. Slack EventsをONにして、Request URLにコピーしたAPIエンドポイントを貼り付け →Verified　※通らなかったら、なにか不備がある
2. Subscribe to workspace eventsにて、`reaction_added`を追加→Save



