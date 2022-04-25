# reactjs-learning-note

## JS ES6

### Scope Chain
+ 有就找{}，沒有往外找
+ let, const 比 var 更嚴謹

### Prototype Chain
+ 每個物件都有__proto__

### OOP
+ 參數有找到就停，沒有則往上找

### this
+ arrow function 沒有 this
+ apply, call, bind 會改變 this 的值
+ new (自動 return)
+ use strict

### JS Event
+ Event Bubbling: mouse event 才有
+ Event Capturing
+ Event Delegation
+ e.target vs e.currentTarget
  + e.target: this
  + e.currentTarget: 觸發事件的元素

## ReactJS

### 優點
+ 前後端分離
+ data binding
+ React(JSX為編譯語言) =(透過 webpack)=> 直譯語言
+ 解決 JS / CSS 變數覆蓋

### 缺點
+ virtual dom 速度快，SEO 下降
> 解決方式: 
> 
> react server side render(須以node js啟動)
> 
> 建立爬蟲用html(header判斷)

### useState vs useState
+ useState 更新 > 觸發 render
+ useRef   更新 > 不會重render，僅記錄變數值

### setCount
+ 等等可以更新 != 馬上更新、重新渲染

### useEffect
+ virtual dom -> html dom -> useEffect

### Source
+ [使用ESLint, Prettier, Husky, Lint-staged以及Commitizen提升專案品質及一致性](https://medium.com/@danielhu95/set-up-eslint-pipeline-zh-tw-990d7d9eb68e)
+ [Type Checking with PropTypes](https://zh-hant.reactjs.org/docs/typechecking-with-proptypes.html)
+ [flow js](https://flow.org/)

* * *
### 課堂練習
> [老師講義](https://reurl.cc/DvxXEN)
> 
> [Homework 2022.04.18](https://codesandbox.io/s/01-conditional-render-question-forked-gjnsrs)
> 
> [Homework 2022.04.22](https://codesandbox.io/s/02-countdown-question-forked-o8c2wl) 
