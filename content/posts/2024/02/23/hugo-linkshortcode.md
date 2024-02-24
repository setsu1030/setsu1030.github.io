+++
title = 'Hugoでリンクを別タブで開くようにする'
date = 2024-02-23T21:31:41+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
見様見真似でやってみました。
### ショートコードファイルの作成
`layouts/shortcodes` 配下に `link.html` を作成する。
{{< code lang="html" title="link.html" >}}
{{- $href := .Get "href" -}}
<a href="{{ $href }}" target="_blank">{{- .Inner -}}</a>

{{< /code >}}
* * *
### マークダウンからショートコードを呼び出す
ポストのマークダウンファイルに以下のように記載します。
{{< code lang="markdown" title="sample.md" >}}
{{</* link href="https://gohugo.io/" */>}}Hugo{{</* /link */>}}
{{< /code >}}
* `link` はショートコードファイルのファイル名と紐づいている
* `href` に設定した値を、ショートコードファイルの `.Get "href"` で取得している。
* タグに囲まれている「Hugo」という文字を、ショートコードファイルの `{{- .Inner -}}` で取得している。
* * *
### 生成されるhtml
以下のようなhtmlが生成され、別タブで開くことができるようになりました。
{{< code lang="html" title="index.html" >}}
<a href="https://gohugo.io/" target="_blank">Hugo</a>
{{< /code >}}
* * *
### 参考にしたサイト
* {{< link href="https://blog.chick-p.work/blog/hugo-shortcode/" >}}HUGO で独自 Shortcode を作る - ひよこまめ{{< /link >}}
