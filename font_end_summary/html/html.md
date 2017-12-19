### DOM-HTML5

### 浏览器工作机制

#### 浏览器内核
渲染引擎和JS引擎  
渲染引擎： HTML，CSS；  
JS引擎：javascript执行；  

常见浏览器内核：webkit（safari，chrome）

#### 浏览器加载机制
浏览器加载html，会”自上而下“加载，解析，渲染，遇到图片，视频之类的资源，会进入另一个下载
线程，去加载图片和视频，不会影响html文档本身加载；

这就是为什么通常UXD在设计的时候，会设置图片占位符，因为图片不会和文档内容同时加载出来。通常，
图片要比文档后加载出来，这就需要添加占位符来给用户一个过渡等待的效果。

当浏览器加载html遇到js文件，浏览器会挂起渲染和其他线程，进入js加载和解析线程，js执行完毕，
html渲染线程才可恢复。

这就是为什么将外部js放到`</body>`前;

** 异步加载js方案: **
1. 给js 加defer，缺点是无法控制js脚本的依赖次序和加载时机；
2. 通过js脚本创建createElement("script")加载脚本，可以手动控制js脚本加载次序；

#### 浏览器五个常驻线程
1. 浏览器GUI渲染线程；
2. javascript引擎线程；
3. 浏览器定时器触发线程setTimeOut；
4. 浏览器事件触发线程；
5. 浏览器http异步请求线程（.jpg  <link/>这类请求）;

>当涉及到阻塞现象时，当js引擎线程进行时，会挂起其他一切线程，


#### HTML5新特性
canvas，svg，video&audio;  
webworker, websocket;  
sessionStorage, localstorage;

## Web App工程化
1.模块化：
---
[JS Moduling](../js/js_modulization_solution.md)

2.构建工具：
---

3.包管理：
---

4.代码质量：
---

























