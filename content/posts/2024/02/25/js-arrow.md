+++
title = 'JavaScriptのアロー関数について'
date = 2024-02-25T21:57:50+09:00
draft = false
tags = ['javascript']
categories = ['備忘録']
+++
まず、JavaScriptの普通の関数。
{{< code lang="javascript" title="test.js" >}}
function fn(number) {
  return number * 2;
}
console.log(fn(2)); // 4
{{< /code >}}
これを無名関数にする。
{{< code lang="javascript" title="test.js" >}}
const fn2 = function(number) {
  return number * 2;
}
console.log(fn2(2)) //4
{{< /code >}}
`function` をとって代わりに `=>` をつけてアロー関数にする。
{{< code lang="javascript" title="test.js" >}}
const fnArrow = (number) => {
  return number * 2;
}
console.log(fnArrow(2)); // 4
{{< /code >}}
引数が１つだけの場合、`()` を省略できる。また、関数内の処理が1文だけの場合 `{}` と `return` も省略できる。
{{< code lang="javascript" title="test.js" >}}
const fnArrow2 = number => number * 2;
console.log(fnArrow2(2)); //4
{{< /code >}}
オブジェクトを返すアロー関数
{{< code lang="javascript" title="test.js" >}}
const fnArrowObj = number => ({result: number * 2})
console.log(fnArrowObj(2)); // {result: 4}
{{< /code >}}
