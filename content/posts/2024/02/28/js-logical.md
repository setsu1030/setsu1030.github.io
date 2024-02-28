+++
title = 'JavaScriptの論理積と論理和について'
date = 2024-02-28T23:11:30+09:00
draft = false
tags = ['javascript']
categories = ['備忘録']
+++
## 論理積
* 与えられた値の中で**falsy**のものを返す。
  * falsyな値が1つの場合
{{< code lang="javascript" title="" >}}
  const result = "" && 1;
  console.log(result); // ""
{{< /code >}}
  * どちらもfalsyな値の場合、**左側**の値が返される。
{{< code lang="javascript" title="" >}}
  const result = "" && 0;
  console.log(result); // ""
{{< /code >}}
  * どちらもtruthyな値の場合、**右側**の値が返される。
{{< code lang="javascript" title="" >}}
  const result = "a" && 1;
  console.log(result); // 1
{{< /code >}}
* * *
## 論理和
* 与えられた値の中で**truthy**のものを返す。
  * truthyな値が1つの場合
{{< code lang="javascript" title="" >}}
  const result = "" && 1;
  console.log(result); // 1
{{< /code >}}
  * どちらもtruthyな値の場合、**左側**の値が返される。
{{< code lang="javascript" title="" >}}
  const result = "a" && 1;
  console.log(result); // "a"
{{< /code >}}
  * どちらもfalsyな値の場合、**右側**の値が返される。
{{< code lang="javascript" title="" >}}
  const result = "" && 0;
  console.log(result); // 0
{{< /code >}}
