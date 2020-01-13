# Lambda

## 概要

* アップロードした関数を実行してくれるサーバレスなマイクロサービス環境（基盤はLinux\)
* アップロードされた関数は都度実行され、終わると破棄されるステートレスな構成
* 最大稼働時間は5分
* 課金単位が「実行時間」なので、実行されていない時は費用がかからない

{% embed url="https://docs.aws.amazon.com/ja\_jp/lambda/latest/dg/welcome.html" %}

{% embed url="https://qiita.com/yhsmt/items/0605d2f7c259267f01b5" %}

{% embed url="https://docs.aws.amazon.com/ja\_jp/lambda/latest/dg/limits.html" %}

## Lambda関数のバージョン（環境）ごとにAPI Gatewayをアタッチする

### Lambdaの設定

1. Lambda関数＞アクション＞エイリアスの作成
2. Lambda関数＞アクション＞新しいバージョンの作成

エイリアス＞１で作成した

![](../.gitbook/assets/image%20%284%29.png)

## API Gatewayの設定

![](../.gitbook/assets/image%20%285%29.png)

## 実装Tips

{% embed url="https://github.com/slackapi/python-slack-events-api" %}



### 注意

* Python3.8では、**requests ライブラリーが含まれなくなった** 
* python3.7以前でも、requetsを利用する場合は、20/4/1以降**個別にインストール**が必要\( ◽ Layer化する\)

> /var/runtime/botocore/vendored/requests/api.py:64: DeprecationWarning: You are using the post\(\) function from 'botocore.vendored.requests'. This dependency was removed from Botocore and will be removed from Lambda after 2020/03/31. [https://aws.amazon.com/blogs/developer/removing-the-vendored-version-of-requests-from-botocore/](https://aws.amazon.com/blogs/developer/removing-the-vendored-version-of-requests-from-botocore/). Install the requests package, 'import requests' directly, and use the requests.post\(\) function instead.

* python3.8でrequetstを利用しようとした場合のエラーメッセージ

`AttributeError: module 'botocore.vendored.requests' has no attribu\te` 

