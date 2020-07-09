---
title: "条件付きコメント内のパスをDreamWeaverのテンプレートに認識させる"
date: 2012-07-19T02:10:02.000Z
updated: 2016-04-03T14:09:47.000Z
tags: 
  - DreamWeaver
  - IE
---

IE6対応をしていると時々条件付きコメントを使って、特定のブラウザ･･･主にIE6ですが･･･だけに読み込ませたいJavaScriptやCSSを記述すると、DreamWeaver内ではコメントと扱われてしまうため、パスが通らなくなってしまい面倒だったので、色々と試してみました。


## 条件付コメントとは

条件付コメントとは、IEだけに解釈されるHTML内に記述することが出来る条件分岐の記述のことです。  
 実際には下記のように記述します。

```html
<!--[if IE 6]>
ここはIE6のみ表示
<![endif]-->
```

この様に、通常のブラウザではコメントアウトと認識され、特定のブラウザだけ表示させられる仕組みです。  
 google-code-prettifyでもコメントアウトと扱われてしまっていますね。

### 使用例

例えばIE6だけに読み込ませ実行させたい、pngfixのライブラリであったり、印刷用のCSSだったりに使えるのですが、前述したとおりDreamWeaver上でもコメントアウトとして認識されてしまい、条件付コメント内でリンクを貼った場合も無視されてしまいます。

### DreamWeaverで扱う問題点

特定のページのみ記述するだけであれば特に気にする必要はありませんが、全ページにテンプレートを使って記述したい場合、階層が変わってしまうとリンクが外れてしまい面倒でした。


## 解決方法

DreamWeaverのテンプレートの機能の中に変数を扱う機能が含まれています。  
 それを利用しコメントアウトの部分を分割することで、テンプレート上ではコメントアウトではなく、生成されたHTMLでは条件付コメントとして出力されるようにします。

実際の方法は下記の通り。

```html
@@('<!-')@@-[if IE 6]>
<script type="text/javascript" src="./path/to/script.js"></script>
<![endif]-@@('->')@@
```

テンプレートファイル限定ではありますが、この様に記述することで、条件付コメント内のパスを崩さずに扱うことが出来ます。


## 参考

- [条件付コメント(Conditional Comments)実験ページ](http://www.keynavi.net/ja/bugh/comments.html)
- [Web制作/Dreamweaver/テンプレートタグリファレンス- zkdesign/Archives](http://www.zkdesign.jp/arch/index.php?Web%C0%A9%BA%EE%2FDreamweaver%2F%A5%C6%A5%F3%A5%D7%A5%EC%A1%BC%A5%C8%A5%BF%A5%B0%A5%EA%A5%D5%A5%A1%A5%EC%A5%F3%A5%B9)