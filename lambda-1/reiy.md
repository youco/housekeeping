---
description: ローカル環境：python 3.7 windows10
---

# レイヤー作成方法

レイヤのイメージ

![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F239179%2F9324220a-e369-1bcb-12dc-40fc37570514.png?ixlib=rb-1.2.2&auto=format&gif-q=60&q=75&s=b8e701408344fd0af351ed93707c084d)

## PKGの準備

```bash
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





