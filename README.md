# preact 源码解析

此时[preact](https://github.com/developit/preact)的版本为8.2.1。

如何使用preact请参考[官网指导](https://preactjs.com/guide/getting-started)。

如有发现存在分析错误或不严谨之处，请前往**issue**提出。

## Source Code Tree

```
dom/
  - index.js
vdom/
  - component-recycler.js
  - component.js
  - diff.js
  - index.js
clone-element.js
component.js
h.js
options.js
preact.js
render-queue.js
render.js
util.js
vnode.js
```
