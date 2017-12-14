JS Tricker Skill
====

解决ES6无法模板字符串不支持for 循环遍历
----

```js
this.videoArroundArray = info.videoGroup.slice(1);
var tagInfoHtml = `<div id="tagInfo-id" class="tagInfo-scroll">
                        <div class="scroll-list">
                            ${this.videoArroundArray.map((item, index)=>`<div class="a-item tagInfo-item" item-store-key="tagInfo" item-data="${index}">${item.groupName}</div>`).join('<div class="vertical-divider"></div>')}
                        </div>
                    </div>`;
contentFragment.innerHTML += tagInfoHtml;
```
	
异步加载JavaScript文件：
----
```html
<script>
    //动态创建script标签异步下载js脚本, onLoad 回调函数用于执行脚本下载后的代码    
function loadScript(src, onLoad) {
        var scriptTag = document.createElement("script");
        scriptTag.src = src;
        if(typeof onLoad === "function") {
            scriptTag.onload = onLoad;
            scriptTag.onreadystatechange = function() {
                if(scriptTag.readyState === 4) {
                    onLoad();
                }
            }
        }
        document.body.appendChild(scriptTag);
    }
</script>
```

将时间戳转换成日期格式：
----
```js
// 简单的一句代码
var date = new Date(时间戳); //获取一个时间对象  注意：如果是uinx时间戳记得乘于1000。比如php函数time()获得的时间戳就要乘于1000
/**
 1. 下面是获取时间日期的方法，需要什么样的格式自己拼接起来就好了
 2. 更多好用的方法可以在这查到 -> http://www.w3school.com.cn/jsref/jsref_obj_date.asp
 */
date.getFullYear();  // 获取完整的年份(4位,1970)
date.getMonth();  // 获取月份(0-11,0代表1月,用的时候记得加上1)
date.getDate();  // 获取日(1-31)
date.getTime();  // 获取时间(从1970.1.1开始的毫秒数)
date.getHours();  // 获取小时数(0-23)
date.getMinutes();  // 获取分钟数(0-59)
date.getSeconds();  // 获取秒数(0-59)
```

### 让JS代码更优雅的一些Tips&Tricks

1. Arrow functions让回调更简洁
---

```js
    const checkedOptions = Object.keys(options).filter((k, i) => options[k]);
    Object.keys(nextOptions).forEach((k,i) => { nextOptions[k] = false });
```

2. object 遍历，有没有更优雅的写法？
---

```js
   // iterate through key-value gracefully
   var obj = {a: 5, b: 7, c: 9};
   for (let [key, value] of Object.entries(obj)) {
       console.log(key + ' ' + value); // "a 5", "b 7", "c 9"
   }
   // babel
   {
     "plugins": ["transform-runtime"],
     "presets": ["es2017"]
   }
```

3. 中括号语法
---

```js
   singleOptionHandler(field, value) {
     this.setState(
       {selected: {...this.state.selected, [field]: [value]}}
     )
   }
```