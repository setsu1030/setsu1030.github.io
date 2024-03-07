+++
title = 'JavaScriptのスプレッド演算子が便利'
date = 2024-03-07T08:20:04+09:00
draft = false
tags = ['javascript','react']
categories = ['備忘録']
Params.toc = true
+++
## 1. はじめに
### スプレッド演算子とは何か？
JavaScriptにおいて、スプレッド演算子（...）は配列やオブジェクトを展開し、その要素を個々の値として扱える構文です。

### スプレッド演算子の重要性
スプレッド演算子には以下の特徴があり、これによりコードの可読性と効率性が向上します。
- 関数の引数を配列から展開可能。
- 配列の複製や結合をシンプルに実行できる。
- オブジェクトの複製や結合をシンプルに実行できる。
- Reactにおいて、オブジェクトの内容の更新やテンプレートへのパラメータの渡しに使用可能。

以下でそれぞれの特徴を詳しく解説します。
- - -
## 2. 関数の引数として展開
スプレッド演算子を使用すると、関数の引数を配列から展開できます。  
例えば、配列内の数字を合計する場合、スプレッド演算子を使用しないと以下のようなコードになります。
{{< code lang="javascript" >}}
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];
console.log(sum(numbers[0], numbers[1], numbers[2])); // 6が出力されます
{{< /code >}}

スプレッド演算子を使用すると、`...numbers`と記載することで配列`numbers`の値を引数`x, y, z`に展開できます。
{{< code lang="javascript" >}}
// 配列の値が x, y, z にそれぞれ展開されます。
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];
console.log(sum(...numbers)); // 6が出力されます
{{< /code >}}
これによりコードの可読性と効率性が向上します。  
また、`const numbers = [1, 2, 3, 4]`のように配列の長さが引数の数より多い場合、引数の数だけ値が展開され残りは無視されます。  
つまり`numbers`の`1, 2, 3`は引数に展開され`4`は無視されます。
- - -
## 3. 配列の操作
### 配列の複製
スプレッド演算子を使用すると、配列の複製がシンプルにできます。  
スプレッド演算子を使用しないと以下のようなコードになります。（Array オブジェクトを使う方法もあります。）
{{< code lang="javascript" >}}
let numberStore = [0, 1, 2];
let newStore = [];

for(let i = 0; i < numberStore.length; i++) {
  newStore[i] = numberStore[i];
}

console.log(numberStore); // [0, 1, 2]が出力されます
console.log(newStore); // [0, 1, 2]が出力されます
{{< /code >}}
スプレッド演算子を使用すると、以下のコードで配列が複製できます。
{{< code lang="javascript" >}}
let numberStore = [0, 1, 2];
// numberStoreの内容を展開します
let newStore = [...numberStore];

console.log(numberStore); // [0, 1, 2]が出力されます
console.log(newStore); // [0, 1, 2]が出力されます
{{< /code >}}

### 配列の結合
スプレッド演算子を使用すると、配列の結合がシンプルにできます。  
スプレッド演算子を使用しないと以下のようなコードになります。（Array オブジェクトを使う方法もあります。）
{{< code lang="javascript" >}}
let numberStore = [0, 1, 2];
let newStore = [12, 13, 14];

for (let i = 0; i < newStore.length; i++) {
  numberStore[numberStore.length] = newStore[i];
}

console.log(numberStore); // [0, 1, 2, 12, 13, 14]が出力されます
{{< /code >}}
スプレッド演算子を使用すると、以下のコードで配列が結合できます。
{{< code lang="javascript" >}}
let numberStore = [0, 1, 2];
let newStore = [12, 13, 14];

// numberStore と newStore の値を展開します
numberStore = [...numberStore, ...newStore];

console.log(numberStore); // [0, 1, 2, 12, 13, 14]が出力されます
{{< /code >}}
配列を結合する場合、`numberStore`の値も展開する必要があることに注意してください。
- - -
## 4. オブジェクトの操作
### オブジェクトの複製
スプレッド演算子を使用すると、オブジェクトの複製がシンプルにできます。  
スプレッド演算子を使用しないと以下のようなコードになります。
{{< code lang="javascript" >}}
const obj = {name: "TARO", age: 30};
const obj2 = {};

obj2.name = obj.name;
obj2.age = obj.age;

console.log(obj); // {age: 30, name: "TARO"}が出力されます
console.log(obj2); // {age: 30, name: "TARO"}が出力されます
{{< /code >}}
オブジェクトを複製する際に`const obj2 = obj;`としてしまうと同じ場所が参照され、一方の値を変更するともう一方の値まで変更されてしまうので注意してください。  

スプレッド演算子を使用すると、以下のコードでオブジェクトの複製ができます。  
`注：オブジェクト内にオブジェクトがネストされている場合、ネストされたオブジェクトは同じ参照を共有します。`
{{< code lang="javascript" >}}
const obj = {name: "TARO", age: 30};
// objの内容を展開します
const obj2 = {...obj};

console.log(obj); // {age: 30, name: "TARO"}が出力されます
console.log(obj2); // {age: 30, name: "TARO"}が出力されます
{{< /code >}}

### オブジェクトのマージ
スプレッド演算子を使用すると、以下のコードでオブジェクトのマージができます。
{{< code lang="javascript" >}}
const obj = {name: "TARO", age: 30};
const obj2 = {name: "TARO", bloodType: "A"};
// オブジェクトをマージします
const objMerge = {...obj, ...obj2};

console.log(objMerge); // {age: 30, bloodType: "A", name: "TARO"}が出力されます。
{{< /code >}}
マージする場合、プロパティ名が被っていると後から宣言した値が反映されるため注意が必要です。
{{< code lang="javascript" >}}
const obj = {name: "TARO", age: 30};
const obj2 = {name: "JIRO", age: 35};

const objMerge = {...obj, ...obj2};

console.log(objMerge); // {age: 35, name: "JIRO"}が出力されます。
{{< /code >}}

- - -
## 5. Reactでの応用
スプレッド演算子はReactのJSXにも応用可能です。
### テンプレートへのパラメータ渡し
テンプレート内でスプレッド演算子を用いると、オブジェクトを展開してパラメータを渡すことができます。  
渡されたパラメータの名前はオブジェクトのプロパティ名になります。
{{< code lang="jsx" >}}
const Example = () => {
  const obj = {
    color: "red",
    value: "Hello"
  };
  {/* オブジェクトを展開して渡します */}
  return <Child {...obj} />;
};

{/* 展開されたプロパティ名で受け取ります */}
const Child = ({color, value}) => {
  return (
    <h2 className={color}>{value}</h2>
  );
};
{{< /code >}}
### useStateによるオブジェクト内容の更新
useStateを使用してオブジェクトの内容を更新する際は、新しいオブジェクトの生成が必要です。  
スプレッド演算子を使用しない場合、オブジェクトの全プロパティを宣言する必要があります。  
スプレッド演算子を利用することで、オブジェクトの内容を展開し、変更しないプロパティを継承しつつ、変更するプロパティのみを宣言して内容を更新できます。  

スプレッド演算子の使用により、更新するオブジェクトに多数のプロパティがある場合でも、プログラムの記述量を大幅に削減できます。
{{< code lang="jsx" >}}
const Example = () => {
  const [obj, setObj] = useState({name: "Taro", age: 30});
  
  const changeName = (e) => {
    {/* スプレッド演算子を使わない場合は、全てのプロパティを宣言する必要があります */}
    setObj({name: e.target.value, age: obj.age});
  };
  const changeAge = (e) => {
    {/* スプレッド演算子を使う場合は、変更するプロパティのみ宣言すればOKです */}
    setObj({...obj , age: e.target.value});
  };
  
  return (
    <React.Fragment>
      <h3>{obj.name}</h3>
      <h3>{obj.age}</h3>
      <input type="text" value={obj.name} onChange={changeName} />
      <input type="number" value={obj.age} onChange={changeAge} />
    </React.Fragment>
  );
};
{{< /code >}}
- - -
## 6. まとめ
JavaScriptとReactの開発において、スプレッド演算子がどのように使用できるかを見てきました。  
スプレッド演算子によりコードの可読性と効率性が向上します。  
提供したサンプルコードを元に是非お試しください。
