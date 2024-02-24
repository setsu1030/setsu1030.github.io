+++
title = 'Hugoで見出しにタグ一覧を表示する'
date = 2024-02-24T14:36:36+09:00
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
### 部分ファイルの作成
`layouts/partials/post_meta/` 配下に `tags.html` を作成する。  
~~categories.htmlを元にしたらなんかできた。~~
{{< code lang="html" title="tags.html" >}}
{{- $taxo := "tags" -}}
{{- with .Param $taxo -}}
<div class="meta__item-tags meta__item">
	{{- partial "svg/tag.svg" (dict "class" "meta__icon") -}}
	<span class="meta__text">
		{{- range $index, $tag := . }}
			{{- $url := urls.Parse ($tag | urlize) -}}
			{{- $path := $url.Path -}}
			{{- with $.Site.GetPage (printf "/%s/%s" $taxo $path) }}
				{{- if gt $index 0 }}, {{ end -}}
				<a class="meta__link" href="{{ .RelPermalink }}" rel="tag">{{ .Title }}</a>
			{{- end }}
		{{- end }}
	</span>
</div>
{{- end }}
{{< /code >}}
* * *
### 設定ファイルの修正
`hugo.toml` の `Params.post_meta` に `tags` を追加します。
{{< code lang="properties" title="hugo.toml" >}}
[Params]
  post_meta = ["date", "categories", "tags"]
{{< /code >}}
* * *
これで見出し部分にタグが表示されるようになりました。
![例](displaytags.png)
