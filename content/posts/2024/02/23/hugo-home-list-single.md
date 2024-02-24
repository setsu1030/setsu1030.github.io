+++
title = 'Hugoの「home, list, single」について'
date = 2024-02-23T15:00:16+09:00
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
### 「home, list, single」って何？
以下はサイドバーの表示非表示・表示位置を設定している項目です。  
このブログでは全てのページでサイドバーを右側に表示する設定にしています。
{{< code lang="properties" title="hugo.toml" >}}
[Params.sidebar]
  home = "right"
  list = "right"
  single = "right"
{{< /code >}}

|パラメータ|ページ|例|
|---|---|---|
|home|ホームページ|このブログの[トップページ](/)|
|list|リストページ|このブログの[投稿一覧](/posts)|
|single|単一ページ|このページ（ブログの記事）|

* * *
### 参考にしたサイト
* {{< link href="https://gohugo.io/templates/lists/" >}}Lists of content in Hugo | Hugo{{< /link >}}
