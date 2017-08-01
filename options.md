options对象用来保存全局的选项
```javascript
/** Global options
 *	@public
 *	@namespace options {Object}
 */
export default {

	/** If `true`, `prop` changes trigger synchronous component updates.
	 *	@name syncComponentUpdates
	 *	@type Boolean
	 *	@default true
	 */
	//syncComponentUpdates: true,   //同步组建更新

	/** Processes all created VNodes.
	 *	@param {VNode} vnode	A newly-created VNode to normalize/process
	 */
	//vnode(vnode) { }  	//处理所有已经创建的VNodes

	/** Hook invoked after a component is mounted. */
	// afterMount(component) { }   //组件挂载完之后触发此钩子函数

	/** Hook invoked after the DOM is updated with a component's latest render. */
	// afterUpdate(component) { }  //组件最新一次render更新dom后触发的钩子函数

	/** Hook invoked immediately before a component is unmounted. */
	// beforeUnmount(component) { }   	//组建卸载之前的钩子函数
};

```
