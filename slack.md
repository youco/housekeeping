# slack

## 画像リサイズ

```bash
# アセンブリの読み込み
[void][Reflection.Assembly]::LoadWithPartialName("System.Drawing")

# 画像ファイルの読み込み
$image = New-Object System.Drawing.Bitmap("C:\Users\youco\Desktop\ws2\a.gif")

# 縮小先のオブジェクトを生成
$canvas = New-Object System.Drawing.Bitmap(512, 512)

# 縮小先へ描画
$graphics = [System.Drawing.Graphics]::FromImage($canvas)
$graphics.DrawImage($image, (New-Object System.Drawing.Rectangle(0, 0, $canvas.Width, $canvas.Height)))

# 保存
$canvas.Save("C:\Users\youco\Desktop\ws2\aaa.gif", [System.Drawing.Imaging.ImageFormat]::Gif)

# オブジェクトの破棄
$graphics.Dispose()
$canvas.Dispose()
$image.Dispose()
```

conversation APIのデータ

{% embed url="https://api.slack.com/types/conversation" %}



