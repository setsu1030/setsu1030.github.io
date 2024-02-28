+++
title = 'Hugo(Mainroad)でフォントを変更する'
date = 2024-02-28T20:15:55+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
ブログのフォントをユニバーサルデザインフォントである、**BIZ UDPGothic**に変更しました。  
{{< link href="https://fonts.google.com/specimen/BIZ+UDPGothic" >}}BIZ UDPGothic - Google Fonts{{< /link >}}
* * *
### はじめに
このブログは「**Hugo**」によって作成されています。  
{{< link href="https://gohugo.io/" >}}https://gohugo.io/{{< /link >}}

使用しているテーマは「**Mainroad**」です。  
{{< link href="https://themes.gohugo.io/themes/mainroad/" >}}https://themes.gohugo.io/themes/mainroad/{{< /link >}}
* * *
## 設定ファイルの変更
設定ファイルに下記の設定を追加します。
{{< code lang="properties" title="hugo.toml" >}}
[Params]
  googleFontsLink = "https://fonts.googleapis.com/css2?family=BIZ+UDPGothic:wght@400;700&display=swap"

[Params.style.vars]
  fontFamilyPrimary = "'BIZ UDPGothic', sans-serif"
{{< /code >}}
* * *
## 参考にしたサイト
* {{< link href="https://mainroad-demo.netlify.app/docs/customization/" >}}Customization - Mainroad{{< /link >}}
