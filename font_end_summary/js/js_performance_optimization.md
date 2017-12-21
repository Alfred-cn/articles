JS的性能瓶颈与优化
====

1.作用域链查找和原型链查找  
----

作用域链查找：当查找一个变量时，先在当前作用域查找，会沿着作用域链到上层作用域查找，直到全局作用域，查找越深，性能越差；  

原型链查找：当查找一个对象属性时，会先查找当前对象的实例属性，如果没有找到则去查找原型上有没有，如果原型上没有，则会查找原型的原型，直到查找到顶级Object，查找的越深，性能越差；


2.循环
----

有些可能一层循环就可以搞定，就不必用两层；还有循环中有时会用length，`for(var i=0; i<arr.length; i++)，`每一次循环都会求值一次arr.length,性能就不如`for(var i=0,len=arr.length; i<len; i++)；`

```js
//2. 提升函数性能
//2.1 使用记忆功能保存先前函数的返回结果

//一个通用函数，和其他函数配合，一起使用，以提升性能
function memorize(fn) {
    return function() {
        var propertyName;
        //初始化记忆对象属性
        fn.storage = fn.storage || {};
    }    
};
```

3.DOM操作
----

DOM操作是很耗费性能的，如果有大量更新DOM，我们可以在js中统一更新后，再一次更新到页面中，减少重绘和回流的次数。  

>离线DOM操作优化：
>当对Dom节点有较大改动的时候，我们先将元素脱离文档流，然后对元素进行操作，最后再把操作后的元素放回文档流。 
 
3.1改变 display 属性，临时将某个元素从文档流中脱离，然后再恢复它。

```js
var ul = document.getElementById('list');
ul.style.display = 'none';
```
	
3.2 通过 createDocumentFragment，创建文档片段，操作后一次性把文档片段添加到文档流中。  

```js
var fragment = document.createDocumentFragment(); 
// 在 fragment 上进行一系列操作  
document.getElementById('list').appendChild(fragment);
```
	
3.3 通过在需要操作的节点上创建副本，然后在副本上进行操作，最后进行替换。  
 
 ```js
var ul = document.getElementById('list');
var clone = ul.cloneNode(true);
// 对 clone 节点进行操作
ul.parentNode.replaceChild(clone, ul);
```

4.事件代理
----
事件代理，如果在一个10000项的列表中每一个都绑定一个匿名函数会导致耗费过多的内存。  
如果我们使用代理就只需要在祖先级标签上绑定一个事件，根据冒泡原理，可以减少内存，提高性能。  

4.1 提升Dom事件性能
----
```html
//1. 委托事件到父元素
//1.1 在冒泡阶段监听事件；
//1.2 事件处理函数委托在父节点上；
<html>
    <ul id="list">
        <li class="list-item"><a href="/" class="list-item-link">Home</a></li>
        <li class="list-item"><a href="/news" class="list-item-link">News</a></li>
        <li class="list-item"><a href="/events" class="list-item-link">Events</a></li>
    </ul>
</html>
```

```js
var list = document.getElementById('list');
//false表示在冒泡阶段进行事件处理，为父元素ul添加事件处理，防止给每个li事件添加处理函数
list.addEventlistener("click", onClick, false);
	
function onClick(evt) {
    var clickedElem = evt.target;
    var targetSought = "A";

    if(clickedElem && clickedElem.tagName === tagNameSought) {
        window.open(clickedElem.href);
    }
	}
```