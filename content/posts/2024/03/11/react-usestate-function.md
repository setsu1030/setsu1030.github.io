+++
title = 'ReactのuseStateで値を更新する時に関数を使った方がいいのはなぜか'
date = 2024-03-11T15:11:45+09:00
draft = false
tags = ['react']
categories = ['記事']
Params.toc = true
+++
## 1. はじめに
React の勉強をしていると、以下のような事が書かれていました。  
> useState で値を更新する時は、関数で値を返した方がいい

useState を使って値を更新する方法は以下の２つがあります。
- 直接状態を更新する方法
{{< code lang="jsx" title="example.js" >}}
const [obj, setObj] = useState(obj);
const changeItem = (e) => {
  setObj({ ...obj, item: e.target.value });
};
{{< /code >}}
- 【推奨】関数を使って状態を更新する方法
{{< code lang="jsx" title="example.js" >}}
const [obj, setObj] = useState(obj);
const changeItem = (e) => {
  setObj(obj => ({ ...obj, item: e.target.value }));
};
{{< /code >}}

直観的には上の直接状態を更新する方法の方が分かりやすく感じたのですが、推奨は下の関数を使って状態を更新する方法の方だそうです。  
この事について私にはいまいち理解が難しかったので少し掘り下げたいと思います。
- - -
## 2. オブジェクト型以外の場合も関数を使った方がいい
まず最初に私が勘違いしていたのが、関数を使って更新した方がいいのはオブジェクト型の更新だと思っていた事です。  
実際はプリミティブ型（`Number`や`String`や`Boolean`等）の更新でも関数を使って更新した方がいいです。  
つまり、**useStateで値を更新する時は基本関数で設定する**という事です。
- - -
## 3. 直接状態を更新する方法の問題点
ここからは実際にコードを実行してみて、直接状態を更新するとどういう事象が発生するのか見たいと思います。  
コードの実行には`JSFiddle`を使用しました。
- {{< link href="https://jsfiddle.net/" >}}JSFiddle - Code Playground{{< /link >}}

以下の通りコードを作成します。
{{< code lang="html" title="HTML" >}}
<div id="app"></div>
{{< /code >}}

{{< code lang="jsx" title="React + No-Library (pure JS)" >}}
const useState = React.useState;

const Example = () => {
	const [count, setCount] = useState(0);
  const updateCount = () => {
    // 直接状態を更新する
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  };
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={updateCount}>５回カウントアップします</button>
    </div>
  );
}

ReactDOM.render(<Example />, document.getElementById('app'));
{{< /code >}}

以下のような画面が表示されます。  
![画面イメージ](image1.png)

ここでボタンを押すと`setCount`が５回呼ばれているため、`Count: 5`と表示される想定です。  
しかし実際にボタンを押してみると、  
![画面イメージ2](image2.png)

`1`しかカウントされませんでした。  

これは１回目の`setCount(count + 1);`を実行後、２～５回目の`setCount(count + 1);`を実行する時はまだ`count`の値は`0`であることを示しています。  
つまり、`setCount`を実行しても`count`にはその値がすぐには反映されないという事です。  

これはReactの**バッチ処理**と呼ばれる動作であり、パフォーマンス最適化のために行われているそうです。  
実際に`setCount`のような処理を連続で実行する事はないかもしれませんが、意図せずに想定と異なる値を使用してしまう可能性があります。
- - -
## 4. 関数で更新する方法で動作確認
次は関数で更新する方法を確認します。

{{< code lang="jsx" title="React + No-Library (pure JS)" >}}
const useState = React.useState;

const Example = () => {
	const [count, setCount] = useState(0);
  const updateCount = () => {
    // 関数で状態を更新する
    setCount(count => count + 1);
    setCount(count => count + 1);
    setCount(count => count + 1);
    setCount(count => count + 1);
    setCount(count => count + 1);
  };
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={updateCount}>５回カウントアップします</button>
    </div>
  );
}

ReactDOM.render(<Example />, document.getElementById('app'));
{{< /code >}}

ボタンを押してみると、  
![画面イメージ3](image3.png)

想定通りカウントされました。  
これは`count => count + 1`のように関数を渡すと、Reactの内部でキューに追加されていき、画面描画時に関数が順番に実行されていく仕様があるためだそうです。
- - -
## 5. まとめ
実際にコードを実行する事で、直接状態を更新する方法では想定外の古い値を参照する可能性がある事、関数を使用して状態を更新する方法では最新の値が取得できる事を確認できました。  
直観的には直接状態を更新する方が分かりやすいですが、関数で設定する理由があるというのを知っていただければと思います。  

ここまで書いたのですが、Reactのドキュメントに同じようなことが書いてありました。。
- {{<link href="https://ja.react.dev/learn/queueing-a-series-of-state-updates">}}一連の state の更新をキューに入れる – React{{< /link >}}
