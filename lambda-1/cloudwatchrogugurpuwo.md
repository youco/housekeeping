# CloudWatchロググループ期間を一括設定

## トリガー

Cloudwatchイベント

## 関数

```text
import boto3
import os

client = boto3.client('logs')
# 対象外とするロググループをカンマ区切りで指定。
except_loggroups = os.environ.get("EXCEPT_LOGGROUPS").split(",")
# ログの保持期間を日数で指定
retention_days = os.environ.get("RETENTION_DAYS")


def lambda_handler(event, context):
  　"""
    ロググループのログ保存期間を指定の値に上書きする
    """
    log_group_retention_days = {}
    for log_group_des in get_log_group_des(next_token=None):
        log_group_retention_days.update(
            get_log_group_retention_days(log_group_des))
    for log_group in log_group_retention_days:
        if log_group_des['logGroupName'] not in except_loggroups and log_group_retention_days[log_group] != int(retention_days):
            response = client.put_retention_policy(
                logGroupName=log_group,
                retentionInDays=int(retention_days)
            )
            print(
                f"successfully change {log_group} retention days : {retention_days} days")


def get_log_group_des(next_token):
    if next_token is not None and next_token != '':
        response = client.describe_log_groups(
            limit=50,
            nextToken=next_token
        )
    else:
        response = client.describe_log_groups(limit=50)
    if 'logGroups' in response:
        yield from response['logGroups']
    # ロググループが多くて50件(最大)を超えるようなら再帰呼出し
    if 'nextToken' in response:
        yield from get_log_group_des(next_token=response['nextToken'])

def get_log_group_retention_days(log_group_des):
    """
    ロググループの保存期間を取得する。
    
    Parameters
    ----------
    log_group_des
        {ロググループ名：保持期間}

    Returns
    -------
    log_group_retention_days: list of int
        ロググループの保存期間を格納したリスト。
    """
    try:
        log_group_retention_days = {
            log_group_des['logGroupName']: log_group_des['retentionInDays']}
    except KeyError:
        log_group_retention_days = {log_group_des['logGroupName']: 'NotExpire'}
    return log_group_retention_days
```

{% embed url="https://qiita.com/chii-08/items/624d22078b30bbc5abc3" %}



