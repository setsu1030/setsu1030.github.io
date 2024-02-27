+++
title = 'Mermaidで作成した画面遷移図がGitHubでエラーになった。'
date = 2024-02-27T10:18:45+09:00
draft = false
tags = ['mermaid','github']
categories = ['備忘録']
+++
## 事象
下記のような画面遷移図をMermaidで作成した時、VSCodeのプレビューでは表示できたがGitHubにアップするとエラーが発生した。
> Unable to render rich display  
> Diagram error not found.

{{< code lang="markdown" title="sample.md" >}}
graph LR
    画面A--[遷移]-->画面B
{{< /code >}}

## 原因
原因は `[遷移]` の部分をダブルクォーテーションで囲んでいなかったため。
{{< code lang="markdown" title="sample.md" >}}
graph LR
    画面A--"[遷移]"-->画面B
{{< /code >}}

## 修正結果
GitHubでも正しく表示できるようになった。  
![画像](Image.png)
