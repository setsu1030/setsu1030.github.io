+++
title = 'JavaScriptの分割代入について'
date = 2024-02-27T22:26:58+09:00
draft = false
tags = ['javascript']
categories = ['備忘録']
+++
## その１
通常のパターン
{{< code lang="javascript" title="test.js" >}}
const arr = ["配列1", "配列2", "配列3"];
console.log(arr[0]);
console.log(arr[2]);
{{< /code >}}

分割代入のパターン
{{< code lang="javascript" title="test.js" >}}
const [a, ,c] = ["配列1", "配列2", "配列3"];
console.log(a);  // 配列1
console.log(c);  // 配列3
{{< /code >}}

## その２
通常のパターン
{{< code lang="javascript" title="test.js" >}}
const obj = { x: "オブジェクト1", y: "オブジェクト2", z: "オブジェクト3" };
console.log(obj.x);
console.log(obj.z);
{{< /code >}}
分割代入のパターン
{{< code lang="javascript" title="test.js" >}}
const {x, z} = { x: "オブジェクト1", y: "オブジェクト2", z: "オブジェクト3" };
console.log(x);  // オブジェクト1
console.log(z);  // オブジェクト3
{{< /code >}}

## その３
通常のパターン
{{< code lang="javascript" title="test.js" >}}
const arr = ["Japan", "Tokyo", "Shinjuku"];
const fnArr = (arr) => {
  console.log(`country: ${arr[0]}`);
  console.log(`state: ${arr[1]}`);
  console.log(`city: ${arr[2]}`);
};
fnArr(arr);
{{< /code >}}
分割代入のパターン
{{< code lang="javascript" title="test.js" >}}
const arr = ["Japan", "Tokyo", "Shinjuku"];
const fnArr = ([country, state, city]) => {
  console.log(`country: ${country}`); // Japan
  console.log(`state: ${state}`); // Tokyo
  console.log(`city: ${city}`); // Shinjuku
};
fnArr(arr);
{{< /code >}}

## その４
通常のパターン
{{< code lang="javascript" title="test.js" >}}
const objAddress = { country: "Japan", state: "Tokyo", city: "Shinjuku" };
const fnObj = (obj) => {
  console.log(`country: ${obj.country}`);
  console.log(`city: ${obj.city}`);
};
fnObj(objAddress);
{{< /code >}}
分割代入のパターン
{{< code lang="javascript" title="test.js" >}}
const objAddress = { country: "Japan", state: "Tokyo", city: "Shinjuku" };
const fnObj = ({country, city}) => {
  console.log(`country: ${country}`); // Japan
  console.log(`city: ${city}`); // Shinjuku
};
fnObj(objAddress);
{{< /code >}}
