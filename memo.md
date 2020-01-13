# memo

{% embed url="https://qiita.com/coto/items/8561113fbafd6133248a" %}

{% embed url="https://www.slideshare.net/AmazonWebServicesJapan" %}

{% embed url="https://www.slideshare.net/AmazonWebServicesJapan/20190813-aws-black-belt-online-seminar-serverless" %}

\*\*\*\*



[https://console.aws.amazon.com/cost-reports/home?region=us-east-1\#/custom?groupBy=None&hasBlended=false&hasAmortized=false&excludeDiscounts=true&excludeTaggedResources=false&excludeCategorizedResources=false&excludeForecast=false&timeRangeOption=Custom&granularity=Daily&reportName=&reportType=CostUsage&isTemplate=true&startDate=2019-12-01&endDate=2020-01-08&filter=%5B%7B%22dimension%22:%22RecordType%22,%22values%22:%5B%22Refund%22,%22Credit%22%5D,%22include%22:false,%22children%22:null%7D%5D&forecastTimeRangeOption=None&usageAs=usageQuantity&chartStyle=Group](https://console.aws.amazon.com/cost-reports/home?region=us-east-1#/custom?groupBy=None&hasBlended=false&hasAmortized=false&excludeDiscounts=true&excludeTaggedResources=false&excludeCategorizedResources=false&excludeForecast=false&timeRangeOption=Custom&granularity=Daily&reportName=&reportType=CostUsage&isTemplate=true&startDate=2019-12-01&endDate=2020-01-08&filter=%5B%7B%22dimension%22:%22RecordType%22,%22values%22:%5B%22Refund%22,%22Credit%22%5D,%22include%22:false,%22children%22:null%7D%5D&forecastTimeRangeOption=None&usageAs=usageQuantity&chartStyle=Group) コスト管理



```text
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "NotAction": "kms:*",
      "Resource": "*",
      "Condition": {
        "NotIpAddress": {
          "aws:SourceIp": [
            "163.135.17.41/32",
            "163.135.17.42/32",
            "163.135.17.43/32",
            "163.135.17.44/32",
            "163.135.17.45/32",
            "163.135.151.64/26",
            "163.135.251.64/27",
            "211.129.78.125/32",
            "121.2.76.65/32",
            "121.2.76.161/32"
          ]
        }
      }
    }
  ]
}

次のことを実行する権限がありません: iam:CreateRole.iam:CreateRole.

グループ※（ユーザ）へアタッチ頂きたい管理ポリシー
・LambdaFullAccess
・API Gateway

・サービス実行ロール
　lambda basic execution policyをLambdaにアタッチ

※ご相談です。
今後、ユーザが増えると想定されますので、グループでの管理としたいと考えております。
また、当該グループに対してMFA認証・PWポリシーを加えたいのですが、可能でしょうか。


Qwer1234
```



