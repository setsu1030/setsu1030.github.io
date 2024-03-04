+++
title = 'Visual Studio CodeのEmmetで「lang="ja"」を出力させる'
date = 2024-03-04T14:27:38+09:00
draft = false
tags = ['vscode']
categories = ['備忘録']
+++
Visual Studio Codeで html のテンプレートを出力した場合、デフォルトでは `<html lang="en">` で出力されています。  
これを `<html lang="ja">` で出力されるように修正します。
## 設定変更
- キー `ctrl + ,` を押して Visual Studio Code の設定画面を開きます。
- 設定の検索欄に `emmet: variables` と入力します。
- "Emmet のスニペットで使用される変数"の「項目の追加」ボタンを押します。
- `項目：lang` `値：ja` で設定します。

![image](image1.png)

**これで `<html lang="ja">` で出力されるようになりました。**
