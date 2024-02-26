+++
title = 'JavaScriptのmoduleのimport/exportについて'
date = 2024-02-26T22:49:50+09:00
draft = false
tags = ['javascript']
categories = ['備忘録']
+++

正直、こんな記法があることを知らなかった。

### その１
{{< code lang="javascript" title="module.js" >}}
export const hello = () => {
    console.log("hello!");
};
{{< /code >}}
{{< code lang="javascript" title="main.js" >}}
import { hello } from "./module.js";
hello(); // hello!
{{< /code >}}

### その２
{{< code lang="javascript" title="module.js" >}}
const funcB = () => {
  console.log("funcB output");
};
export default funcB;
{{< /code >}}
{{< code lang="javascript" title="main.js" >}}
import functionB from "./module.js"; // export default では別名も付けられる
functionB();　// funcB output
{{< /code >}}

### その３
{{< code lang="javascript" title="module.js" >}}
class User {
  constructor(name) {
    this.name = name;
  }
  hello() {
    console.log(this.name);
  }
}
export { User }
{{< /code >}}
{{< code lang="javascript" title="main.js" >}}
import { User } from "./module.js";
conset user = new User('john');
user.hello(); // john
{{< /code >}}
