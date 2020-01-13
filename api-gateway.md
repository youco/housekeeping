# API Gateway

## API Gatewayとは

* 受け取ったリクエストを、それぞれのマイクロサービスにルーティングする仕組み
* Lambda関数をREST形式等のWeb APIとして呼び出すことができる
* 受け取った API コールと送出したデータ量に応じて課金される

## ログ設計Tips

![](.gitbook/assets/image%20%288%29.png)



![](.gitbook/assets/image%20%281%29.png)

### ドキュメント

{% embed url="https://aws.amazon.com/jp/api-gateway/" %}

{% embed url="https://docs.aws.amazon.com/ja\_jp/apigateway/latest/developerguide/welcome.html" %}





{% embed url="https://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-online-seminar-2016-amazon-api-gateway" %}





## API Gateway呼び出し時に、IPアドレス制限をかける

### 制限をかけるIPアドレスを確認する

Lambdaに下記コードを追加し、アクセス元のIPアドレス等をCloudwatchログに出力する。

```text
from logging import getLogger, DEBUG, INFO

logger = getLogger(__name__)
logger.setLevel(DEBUG)

def lambda_handler(event, context):
    logger.debug(event['requestContext']['identity']['sourceIp'])
```

### API Gateway側でIPアドレス制限を行う

1. リソースポリシー＞右画面に設定を記載（下記コード参考）
2. APIをデプロイ

```text
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "execute-api:Invoke",
            "Resource": "*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": "11.22.33.44" ★上記で確認したアドレス
                }
            }
        }
    ]
}
```

#### 参考

{% embed url="https://www.wakuwakubank.com/posts/520-aws-api-resource-policies/" %}



## APIキー

呼び出し時に認証を加える

* [ ] メソッドリクエスト：API必要性True → 項目横のチェックをクリックして反映
* [ ] 使用量プラン→新規作成（初回のみ）

  * [ ] 関連付けられたAPIステージ→APIとステージを選択
  * [ ] APIキーを作成して使用量プランに紐付け→名前（自由）APIキー：自動生成

  →完了

* [ ] 左メニュー：APIキー
  * [ ] 作成したAPIの名前を選択→APIキー

{% embed url="https://mashpote.net/2019/08/26/aws-api-gateway%E3%82%92%E5%AE%9F%E8%A3%85%E3%81%97%E3%81%A6%E3%81%BF%E3%81%A6%E6%80%9D%E3%81%A3%E3%81%9F%E3%81%93%E3%81%A8/" %}

{% embed url="https://reiki4040.hatenablog.com/entry/2017/02/11/232357" %}



