# OBS Calender widget
OBSのブラウザソースを介してカレンダーを表示するwidgetです。

CustomCSS用にたくさん必要そうなクラス振ってるので自由に使ってください

## Recommended Setting
URL: https://calender.tsutori.ngo/  
幅: 600  
高さ: 800

カスタムCSS
```css
body { background-color: rgba(0, 0, 0, 0); margin: 0px auto; overflow: hidden; }


/* Macを使用している場合、右上の文字が小さくなってしまうためなってしまうためMacの場合推奨 */
/* .mini-calender td.date span {
    transform: scale(2.2);
} */

.calender > table td.date.today {
  position: relative;
}

.calender > table td.date.today span:not(.before) {
  z-index: 2;
  position: absolute;
}

```

## クレジット表記について

クレジット表記については載せても載せなくてもかまいません！
おまかせします！

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)
