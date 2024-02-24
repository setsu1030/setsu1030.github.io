+++
title = 'Hugoのコードブロックでショートコードの内容を表示させる'
date = 2024-02-23T23:26:46+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
### 事象
{{< link href="/posts/2024/02/23/hugo-linkshortcode/" >}}前回の記事{{< /link >}}でマークダウンの記述内容をコードブロックに記載した際、  
こう表示させたかったのが、
{{< code lang="markdown" title="sample.md" >}}
{{</* link href="https://gohugo.io/" */>}}Hugo{{</* /link */>}}
{{< /code >}}
こう表示されてしまった。
{{< code lang="markdown" title="sample.md" >}}
{{< link href="https://gohugo.io/" >}}Hugo{{< /link >}}
{{< /code >}}
Hugoのショートコードが実行されてしまったため、aタグが表示されていた。
* * *
### 解決方法
ショートコードの呼び出し部分を `{{＜/* link */＞}}` のように`/* */` で囲う。  
※大なり小なりを全角にしています。
* * *
### 参考にしたサイト
* {{< link href="https://liatas.com/posts/escaping-hugo-shortcodes/" >}}Escaping Hugo shortcodes{{< /link >}}
