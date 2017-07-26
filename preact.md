```javascript
import { h, h as createElement } from './h';
import { cloneElement } from './clone-element';
import { Component } from './component';
import { render } from './render';
import { rerender } from './render-queue';
import options from './options';

/**
 * 导出所有的方法，其中包括
 * 
 * h => 用来把JSX转换成virtual DOM元素
 *
 *
 *
 *
 */

export default {
	h,
	createElement,
	cloneElement,
	Component,
	render,
	rerender,
	options
};

export {
	h,
	createElement,
	cloneElement,
	Component,
	render,
	rerender,
	options
};
```