---
description: ローカル環境：python 3.7 windows10
---

# レイヤー作成方法

## PKGの準備

```text
$ mkdir python
$ pip install -t ./python requests #　-> pythonフォルダでPKGをインストール

```

![&#x4E0A;&#x8A18;&#x30B3;&#x30DE;&#x30F3;&#x30C9;&#x306E;&#x7D50;&#x679C;&#x3001;python&#x914D;&#x4E0B;&#x306B;PKG&#x304C;&#x30C0;&#x30A6;&#x30F3;&#x30ED;&#x30FC;&#x30C9;&#x3055;&#x308C;&#x308B;](../.gitbook/assets/image%20%282%29.png)

pythonフォルダをZip化（Zipの名前は何でもよい）

## Layer作成

AWS &gt; Lambda &gt; Layers

Layerの利用

Lambda関数で、通常どおり`import` \(例：`import requests`\)

## 参考

{% embed url="https://aws.amazon.com/jp/blogs/aws/new-for-aws-lambda-use-any-programming-language-and-share-common-components/" %}

{% embed url="https://dev.classmethod.jp/cloud/aws/lambda-layer-first-action/" %}





