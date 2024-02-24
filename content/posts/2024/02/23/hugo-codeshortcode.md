+++
title = 'Hugoのコードブロックの見た目を修正する'
date = 2024-02-23T22:28:33+09:00
draft = false
tags = ['hugo']
categories = ['備忘録']
+++
### ショートコードファイルの作成
コードブロックにファイル名を表示させたいと思ったので、ショートコードで作成します。  
`layouts/shortcodes` 配下に `code.html` を作成します。
{{< code lang="html" title="code.html" >}}
{{ $title := .Get "title" }}
{{ $lang := or (.Get "lang") "" }}
<figure class="CodeBlock">
{{ with $title }}<figcaption class="CodeBlock_title">{{ . }}</figcaption>{{ end }}
<div class="CodeBlock_code">{{ highlight (trim .Inner "\r\n") $lang "" }}</div>
</figure>

{{< /code >}}
* * *
### マークダウンからショートコードの呼び出し
{{< code lang="markdown" title="sample.md" >}}
{{</* code lang="go" title="sample.go" */>}}
package main
import "fmt"
func main() {
    fmt.Println("Hello World")
}
{{</* /code */>}}
{{< /code >}}
* `lang` に表示するコードの言語を記載します。
* `title` にコードブロックに表示させるファイル名を記載します。
* * *
### 生成されるhtml
htmlでは以下のように表示されます。
{{< code lang="go" title="sample.go" >}}
package main
import "fmt"
func main() {
    fmt.Println("Hello World")
}
{{< /code >}}
* * *
### CSSの修正
見た目を少し修正したかったので、カスタムCSSを使用します。  
まず設定ファイルでカスタムCSSのファイルを登録します。
{{< code lang="properties" title="hugo.toml" >}}
[Params]
  customCSS = ["css/custom.css"]
{{< /code >}}
`static/css/custom.css` を作成します。  
見た目の設定はお好みで。
{{< code lang="css" title="custom.css" >}}
.CodeBlock .CodeBlock_code pre {
    margin-top: 0;
    margin-bottom: 0;
    padding: 5px;
}
{{< /code >}}
* * *
### 参考にしたサイト
* {{< link href="https://maku77.github.io/p/gxk6qat/" >}}Hugo でソースコードをハイライト表示する (highlight) - まくまく Hugo ノート{{< /link >}}
