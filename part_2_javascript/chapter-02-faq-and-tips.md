title: JavaScript Tips
date: 2015-01-01 10:24:32
tags: illustrator
---

[http://stackoverflow.com/questions/12797118/how-can-i-declare-optional-function-parameters-in-javascript](http://stackoverflow.com/questions/12797118/how-can-i-declare-optional-function-parameters-in-javascript)

```js
function myFunc(a, b){
  b = b || 0;
  // b will be set either to b or to 0
}
```