+++
title = 'Hugo(Mainroad)でコードハイライトのテーマを変更する'
date = 2024-02-29T20:51:09+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
### はじめに
このブログは「**Hugo**」によって作成されています。  
{{< link href="https://gohugo.io/" >}}https://gohugo.io/{{< /link >}}

使用しているテーマは「**Mainroad**」です。  
{{< link href="https://themes.gohugo.io/themes/mainroad/" >}}https://themes.gohugo.io/themes/mainroad/{{< /link >}}
* * *
## 設定ファイルの変更
設定ファイルに下記の設定を追加します。
{{< code lang="properties" title="hugo.toml" >}}
[markup]
  [markup.highlight]
    style = "github-dark"
{{< /code >}}
* * *
## 変更したイメージ
変更前
![変更前](Image_before-0.png)

変更後
![変更後](Image_after-0.png)
