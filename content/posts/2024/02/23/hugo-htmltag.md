+++
title = 'Hugoのマークダウンでhtmlタグを使えるようにする'
date = 2024-02-23T19:10:00+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
### 設定ファイルの修正
`hugo.toml`に下記の設定を行います。
{{< code lang="properties" title="hugo.toml" >}}
[markup]
  [markup.goldmark.renderer]
    unsafe = true
{{< /code >}}

* * *
### 注意事項
マークダウンのレンダラーであるGoldmarkのページには以下の記載があります。
> By default, goldmark does not render raw HTML or potentially-dangerous URLs. If you need to gain more control over untrusted contents, it is recommended that you use an HTML sanitizer such as bluemonday.

* * *
### 参考にしたサイト
* {{< link href="https://budougumi0617.github.io/2020/03/10/hugo-render-raw-html/" >}}Hugo v0.60以上を使うと、Markdown中のHTMLタグが「raw HTML omitted」となって消えてしまう - My External Storage{{< /link >}}
* {{< link href="https://github.com/yuin/goldmark/?tab=readme-ov-file#security" >}}yuin/goldmark: :trophy: A markdown parser written in Go. Easy to extend, standard(CommonMark) compliant, well structured.{{< /link >}}
