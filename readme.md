# demos #
这里会用react和原生js两种方式来实现不同的组件，并努力做到兼容PC和移动端。
为了更好的操作DOM，这里我还实现了一个简单的jQuery。
## $.js ##
这是一个简单的类jQuery库，目前支持选择器、链式调用、on事件绑定以及一些工具方法。
#### 与jQuery不同的地方 ####
由于选择器实现还不够完善，目前只支持传入字符串和DOM。<br>
不管你是选择id还是class，在进行下一步操作之前（比如addClass、removeClass，on可以无视）必须先告知要获取到第几个DOM，比如$("#tabs").get(0).addClass("tabs")，如果没有get(0)，这里会报错。<br>
同时，jQuery中的$(document).ready(function() {})和$(function() {})在这里一律用$.ready(function() {})来代替。<br>
这里实现了两个观察者模式，一个是挂载到$函数上的publish和subscribe，这里绑定的是全局window。<br>
另一个是挂载到$.prototype上面的on和trigger函数，这个可以在DOM上面绑定事件并监听，但是通过trigger触发的自定义事件传入的数据，需要在on的回调函数中以event.detail的形式来获取到。<br>
## templateX.js ##
这是一个简单的模板引擎。
语法类似underscore的template，但是不同点在于不再区分<%=%>和<%%>，在这里面一律按照<%%>来进行编写。<br>
#### 推荐用法 ####
这里建议在html里面提前写好一个script标签，注意type为text/template，在标签里面可以书写模板，在页面加载完成后获取到script里面的DOM字符串后将其和数据一起传给templateX方法，最后将返回结果插入要渲染的节点下面，这里可以使用$.js中的html来获取和插入DOM字符串。<br>
具体用法可以参考tab.html里面的例子。
## 基于react的Tab组件 ##
Tab组件接受defaultKey和onSelect两个参数。<br>
defaultKey是指默认的指定key值，用于第一次渲染的时候激活指定的tab。onSelect是一个函数，参数是当前激活状态tab的key值。<br>
TabPane组件作为Tab组件的插槽使用，接受currentKey和title两个参数。<br>
currentKey是指当前tab的key，title则是当前tab头部的名称。<br>
TabPane组件还会接受用户自定义的插槽，这个会当做tab的主体内容进行渲染，用户可以传入字符串或者自定义的DOM结构。<br>
