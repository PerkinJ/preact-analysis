**h**函数接受了两个主要参数以及多个其他的参数作为子节点，返回一个虚拟DOM元素。

```javascript
import { VNode } from './vnode'; // 引入VNode
import options from './options'; // 引入全局选项


const stack = []; // 用来存放除nodeName和attributes之外的参数

const EMPTY_CHILDREN = []; // 用来初始化children

/** JSX/hyperscript reviver
*	Benchmarks: https://esbench.com/bench/57ee8f8e330ab09900a1a1a0
 *	@see http://jasonformat.com/wtf-is-jsx
 *	@public
 */
export function h(nodeName, attributes) {
  let children=EMPTY_CHILDREN, lastSimple, child, simple, i;
  for (i=arguments.length; i-- > 2; ) {
    stack.push(arguments[i]); // 先把除了nodeName和attributes之外所有的参数扔到stack里面
  }
  /** 
   * 如果attributes定义了children属性并且当前stack为空时，stack插入children
   * 随后删除children属性
   * 这个步骤是针对这样的方式
   *
   * h('div', {
   *   class: 'foo',
   *   children: h('div', {
   *     class: 'bar'
   *   }, 'content: bar')
   * })
   */ 
  if (attributes && attributes.children!=null) {
      if (!stack.length) stack.push(attributes.children);
      delete attributes.children;
    }
    while (stack.length) {
      if ((child = stack.pop()) && child.pop!==undefined) {
        for (i=child.length; i--; ) stack.push(child[i]);
      }
      else {
        if (typeof child==='boolean') child = null;

        if ((simple = typeof nodeName!=='function')) {
          if (child==null) child = '';
          else if (typeof child==='number') child = String(child);
          else if (typeof child!=='string') simple = false;
        }

        if (simple && lastSimple) {
          children[children.length-1] += child;
        }
        else if (children===EMPTY_CHILDREN) {
          children = [child];
        }
        else {
          children.push(child);
        }

        lastSimple = simple;
      }
    }

    let p = new VNode();
    p.nodeName = nodeName; // 虚拟DOM的节点名称
    p.children = children; // 虚拟DOM所有的孩子们
    p.attributes = attributes==null ? undefined : attributes; // 所有的属性
    p.key = attributes==null ? undefined : attributes.key; // 指定key

    // if a "vnode hook" is defined, pass every created VNode to it
    if (options.vnode!==undefined) options.vnode(p);

    return p;
}
```