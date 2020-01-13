# Identity and Access Management \(IAM\)

{% embed url="https://docs.aws.amazon.com/ja\_jp/IAM/latest/UserGuide/best-practices.html" caption="IAMベストプラクティス" %}

{% embed url="http://awspolicygen.s3.amazonaws.com/policygen.html" %}



## 管理者グループ＆管理者ユーザの作成

### 管理者グループの作成

1. グループを新規作成
2. ポリシーのアタッチ：AdministratorAccess

{% embed url="https://console.aws.amazon.com/iam/home?\#/groups" caption="上記より「新しいグループ作成」をクリックして、新しいグループの作成ウィザードを実施する" %}

### 管理者ユーザの作成

1.  AWS アクセスの種類を選択：AWS マネジメントコンソールへのアクセスのみにチェック
2. ユーザをグループに追加：管理者グループを選択

{% embed url="https://console.aws.amazon.com/iam/home?\#/users$new?step=details" caption="新しいユーザの作成ウィザード" %}







