+++
title = 'フレームワークを使わないReactのサンプル'
date = 2024-03-01T22:52:27+09:00
draft = false
tags = ['react']
categories = ['備忘録']
+++
React の勉強のためフレームワークを使わずに html で記述したサンプルです。  
Example というコンポーネントを宣言して描画しています。
{{< code lang="html" title="index.html" >}}
<!DOCTYPE html>
<html>
<head>
   <script src="/js/react.development.js"></script>
   <script src="/js/react-dom.development.js"></script>
   <script src="/js/babel-standalone.js"></script>
</head>
<body>
    <div id="app"></div>
    <script type="text/babel">
        const appEl = document.querySelector('#app');
        const root = ReactDOM.createRoot(appEl);
        const Example = () => {
            return (
                <div>
                    <h1>Hello React</h1>
                </div>
            );
        }
        root.render(<Example />);
    </script>
</body>
</html>
{{< /code >}}
