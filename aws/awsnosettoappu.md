---
description: 作業用のユーザを作成する。本手順は管理者ユーザで実施する
---

# AWSのセットアップ（lambda実行ユーザの作成）

#### 作成するユーザについて

LambdaとAPI Gatewayを使う開発者ユーザを作る。後々サービス・権限が増えるかも。

## 管理者ユーザでコンソールにサインイン

{% embed url="https://xxxxxxx.signin.aws.amazon.com/console" %}

## IAMでグループ・ユーザを作成する

グループに付与する管理ポリシー

1. AWSLambdaFullAccess
2. AmazonAPIGatewayAdministrator
3. AWSAccountUsageReportAccess
4. AWSAccountActivityAccess

3・4：開発者ユーザにもリソース利用状況、請求情報の参照権限を付与しておく。

### Lambda開発ユーザを作成

管理ポリシーを新規作成し、グループに追加する

{% embed url="https://console.aws.amazon.com/iam/home?region=ap-northeast-1\#/policies" %}

管理ポリシーの作成＞Jsonで、「MFA\_Policy」「IAM\_Policy」を作成

{% embed url="https://github.com/youco/home/blob/f8f38b4e6b725cfeb575d00d9acf97d1c01aacba/MFA\_Policy.json" %}

{% embed url="https://github.com/youco/home/blob/master/IAM\_Polict.config" %}

ユーザを新規作成し、作成したグループに追加する

### Lambda実行用ロールの作成

{% embed url="https://console.aws.amazon.com/iam/home?region=ap-northeast-1\#/roles" %}

ロールの作成＞AWSサービス：Lambda＞ポリシー：「AWSLambdaBasicExecutionRole」









## 参考

{% embed url="https://qiita.com/dcm\_kawasaki/items/50716af413ad4fdb0153" %}



{% embed url="https://qiita.com/tmknom/items/303db2d1d928db720888\#%E8%AB%8B%E6%B1%82%E6%83%85%E5%A0%B1%E3%81%AE%E8%A8%AD%E5%AE%9A" %}

{% embed url="https://www.slideshare.net/AmazonWebServicesJapan/awswebinar-aws-56260969" %}



