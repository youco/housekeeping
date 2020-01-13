---
description: AWSを利用する場合にまず行うことを記録。本手順はルートアカウントで実施する。
---

# AWSのセットアップ１

## まずはじめに：ルートアカウント新規作成

* 無料枠１年分がついてくるので、Gmailのエイリアスを使うと良い 📧 。

{% embed url="https://aws.amazon.com/jp/register-flow/" %}

## 🔱 ルートアカウントのセキュリティ保護

* AWSアカウントをすると「ルートアカウント」ができる。このアカウントは全権限をもつため、基本は利用しない。
* ルートアカウントが漏洩するリスクを低減するため、ルートアカウントのセキュリティ強化をはじめに行う。

下記IAMコンソールにルートユーザでログインし、セキュリティステータス（５つ）を設定していく。すべて緑になれば完了。

{% embed url="https://console.aws.amazon.com/iam/home" %}

1. [x] ルートアカウントのアクセスキー削除
2. [x] MFA認証の有効化
   * virtual MAFを選択
   * Google AuthenticatorアプリとかにインストールしてMFAする
3. [x] [IAMユーザの作成](https://youco-y.gitbook.io/my-note/iam)

   ※IAMユーザ＝作業ユーザ  
    ❗ 作成したユーザを選択し、認証情報タブ＞コンソールのサインインリンクをコピーしておく  
   例）https://xxxxx.signin.aws.amazon.com/console

4. [x] IAMパスワードポリシーの設定
5. [x] アクセスキーのローテーション

→セキュリティステータスがすべて緑になっていることを確認 😁 

## 💵 請求情報へIAMユーザのアクセスを許可する

* [x] 請求情報に対する IAM ユーザーアクセス→編集→IAMアクセスのアクティブ化

{% embed url="https://console.aws.amazon.com/billing/home\#/preferences" %}

#### Billingの設定

{% embed url="https://console.aws.amazon.com/billing/home\#/preferences" %}

* [x]  無料利用枠の使用のアラートの受信
* [x]  請求アラートを受け取る

奨励の設定

* [x] 支払い通貨を日本円に
* [x] 代替連絡先の設定



### CloudWatch請求アラームの作成

任意の金額に達したタイミングで通知を受け取る設定

{% embed url="https://console.aws.amazon.com/cloudwatch/home?region=us-east-1" %}

* [x] アラームの作成＞メトリクスの選択＞「概算＞合計＞請求（EstimatedCharges）」 →SNSサブスクリプションを確認することで、アラームが有効化される

![](../.gitbook/assets/image%20%287%29.png)

#### CostExplorerを有効化

{% embed url="https://console.aws.amazon.com/billing/home\#/costexplorer" %}

## おわり

ルートユーザをログアウト 🤝 

#### 参考

{% embed url="https://avinton.com/academy/aws-security/" %}

{% embed url="https://qiita.com/tmknom/items/303db2d1d928db720888\#%E8%AB%8B%E6%B1%82%E6%83%85%E5%A0%B1%E3%81%AE%E8%A8%AD%E5%AE%9A" %}





