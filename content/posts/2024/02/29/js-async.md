+++
title = 'JavaScriptの非同期処理（Promise await async）について'
date = 2024-02-29T21:45:24+09:00
draft = false
tags = ['javascript']
categories = ['備忘録']
+++
## Promise
非同期処理の後に何らかの処理を実行したい場合に使用する。
{{< code lang="javascript" title="sample.js" >}}
new Promise((resolve, reject) => {
    setTimeout(() => {
        let a = 1;
        resolve(a); // thenを実行する。
    }, 2000);
}).then((a) => {
    // resolve()が実行されたら呼び出される。引数を受け取ることができる。
    console.log(a); // 1
}).catch((e) => {
    // reject()が実行されたら呼び出される。
    console.log('error');
});
{{< /code >}}
* * *
## await async
Promiseを使った処理を `then` を使わずに記述することができる。
{{< code lang="javascript" title="sample.js" >}}

init();
// 実行する関数に async を付ける必要がある。
async function init() {
    try {
        // new Promise の前に await を付ける。
        const result = await new Promise((resolve, reject) => {
            setTimeout(() => {
                let a = 1;
                resolve(a); // 引数が戻り値として渡される。
            }, 2000);
        });
        // 非同期処理が実行された後に実行される
        console.log(result); // 1
    } catch(e) {
        // reject()が実行されたら呼び出される。
        console.log('error');
    }
}
{{< /code >}}
