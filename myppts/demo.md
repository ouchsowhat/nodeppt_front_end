title: 前端培新——DOM、CSS和Vue
speaker: 杨亚
transition: slide3
files: /js/demo.js,/js/zoom.js,/css/bootstrap.css,/css/demo.css,/js/vue.min.js
theme: moon
date: 2017年8月10日

[slide]
# DOM
## 文档对象模型

[slide]
## HTML DOM
----
* 所有事物都是节点，DOM是被视为节点树的HTML {:&.rollIn}
* 定义了所有 HTML元素的对象和属性，以及访问它们的方法

<div style="padding-top: 30px">
	<img src="/domtree.jpg" height="400" width="550">
</div> {:&.rollIn}

[slide]
## DOM属性
----
* 属性代表DOM节点的内容，可通过编程接口访问

<div class="pptrow">
  <div class="ppt-col-6">
    <h3><span>innerHTML属性:</span><br>返回开始和结束标签之间的HTML</h3>
    <div><h4>var txt = document<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.getElementById("id")<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.innerHTML</h4></div>
  </div>
  <div class="ppt-col-6">
    <h3><span>nodeName属性:</span><br>规定节点的名称，只读</h3>
    <div>
    <h4>根节点->#document</h4>
    <h4>元素节点->与标签名相同</h4>
    <h4>属性节点->与属性名相同</h4>
    <h4>文本节点->始终是#text</h4>
    </div>
  </div>
</div>
<div class="pptrow">
  <div class="ppt-col-6">
    <h3><span>nodeValue属性:</span><br>规定节点的值</h3>
    <div>
    <h4>元素节点->undefined或null</h4>
    <h4>文本节点->文本本身</h4>
    <h4>属性节点->属性值</h4>
    </div>
  </div>
  <div class="ppt-col-6">
    <h3><span>nodeType属性:</span><br>返回节点的类型，只读</h3>
    <div>
    <h4>元素节点->1</h4>
    <h4>属性节点->2</h4>
    <h4>文本节点->3</h4>
    <h4>注释节点->4</h4>
    <h4>根节点->9</h4>
    </div>
  </div>
</div>
<style>
.pptrow{
  margin-right: -15px;
  margin-left: -15px;
}
.ppt-col-6{
    width: 50%;
    float: left;
    position: relative;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
}
.ppt-col-6 h3,.ppt-col-6 h4{
  text-align: left
}
.ppt-col-6 span{
  color: yellow
}
.ppt-col-6 div{
  background-color: rgb(11,108,150);
  padding: 10px;
  border-radius: 5px
}
</style>

[slide]
## DOM接口
----
* Document对象表示文档本身的根节点对象
* Element对象提供单个元素使用的方法和属性

<div>
<table class="table table-hover">
	<thead>
    <tr>
      <th style="text-align: center;">接口</th>
      <th style="text-align: center;">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>document.getElementById</td>
      <td>返回对拥有指定 id 的第一个对象的引用</td>
    </tr>
    <tr>
      <td>element.getElementsByTagName</td>
      <td>返回带有指定标签名的对象集合</td>
    </tr>
    <tr>
      <td>document.createElement</td>
      <td>创建元素节点</td>
    </tr>
    <tr>
      <td>element.appendChild</td>
      <td>把新的子节点添加到指定节点</td>
    </tr>
    <tr>
      <td>element.getAttribute</td>
      <td>返回属性值</td>
    </tr>
    <tr>
      <td>element.setAttribute</td>
      <td>修改属性值</td>
    </tr>
    <tr>
      <td>element.addEventListener</td>
      <td>注册事件回调</td>
    </tr>
  </tbody>
</table>
</div> {:&.moveIn}
<div>
<pre><code>//eg:
window.onload = function() {
	heading = document.createElement("h1");
	heading_text = document.createTextNode("Big Head!");
	heading.appendChild(heading_text);
	document.body.appendChild(heading);
}
</code></pre>
</div> {:&.moveIn}
<style>
	table td, table th{
		font-size:14px;
	}
	pre code{
		font-size:18px;
	}
</style>

[slide]
## DOM事件
----
__事件捕获 ->  事件目标 ->  事件冒泡__ {:&.rollIn}
<div class="row"> 
	<span class="col-md-3">事件发生时首先派发在document上，然后依次传递给body，最后到达目的节点（即事件目标）</span>
	<img src="/eventdispatch.png" class="col-md-6">
	<span class="col-md-3">事件到达事件目标之后不会结束，会逐层向上冒泡，直至document对象</span>
</div> {:&.rollIn}

[slide]
### 常用DOM事件
----
句柄 | 触发条件
:----: | :-----:
onchange | 域的内容被改变
onclick | 点击某个对象时
ondblclick | 双击某个对象时
onfocus/onblur | 元素获得焦点/元素失去焦点
onkeydown/onkeyup/onkeypress | 某个键盘按键被按下/被松开/被按下并松开
onmousedown/onmouseup | 鼠标按钮被按下/鼠标按键被松开
onmouseover/onmouseout | 鼠标移到某元素之上/鼠标从某元素移开
onmousemove | 鼠标被移动
onsubmit | 确认按钮被点击
onselect | 文本被选中

[slide]
[note]
* addEventListener参数1：监听的事件；参数2：事件触发的方法；参数3：默认false，事件在冒泡阶段执行，true捕获时执行
[/note]
###注册事件监听
----
<div style="text-align: left">&bull; EventTarget.addEventListener</div>
<pre><code class="javascript">//Assuming myButton is a button element
myButton.addEventListener('click', 
	function(){
		alert('Hello world');
	}, false);
</code></pre>

<div style="text-align: left">&bull; HTML属性</div>
<pre><code class="html">&lt;button onclick="alert('Hello world!')"&gt;
</code></pre>

<div style="text-align: left">&bull; DOM元素属性</div>
<pre><code class="javascript">//Assuming myButton is a button element
myButton.onclick = function(event){
	alert('Hello world');
};
</code></pre>

[slide]
# CSS
## 层叠样式表

[slide]
## CSS简介
----
* 主要作用: 样式化和排版网页 {:&.rollIn}
* 语法规则: 一个选择器,一组属性 <br>
<div><img style="padding-left: 130px" src="/cssgraph.png"><div>
* 应用方式: <button class="btn btn-rounded btn-warning" onclick="openout()">外部样式表</button> <button class="btn btn-rounded btn-primary" onclick="openin()">内部样式表</button> <button class="btn btn-rounded btn-success" onclick="openinline()">内联样式</button> <br>
<div style="height:150px;width: 100%">
<pre id="css_out" style="display: none"><code>//外部样式表
&lt;link rel="stylesheet" href="style.css"&gt;
</code></pre>
<pre id="css_in" style="display: none"><code>//内部样式表
&lt;style&gt;
p {
    color: red;
  }
&lt;/style&gt;
</code></pre>
<pre id="css_inline" style="display: none"><code>//内联样式
&lt;p style="color:red;"&gt;Hello&lt;/p&gt;
</code></pre>
<div>
<script>
	function openout(){
		document.getElementById("css_out").style.display = 'block';
		document.getElementById("css_in").style.display = 'none';
		document.getElementById("css_inline").style.display = 'none';
	}
	function openin(){
		document.getElementById("css_in").style.display = 'block';
		document.getElementById("css_out").style.display = 'none';
		document.getElementById("css_inline").style.display = 'none';
	}
	function openinline(){
		document.getElementById("css_inline").style.display = 'block';
		document.getElementById("css_out").style.display = 'none';
		document.getElementById("css_in").style.display = 'none';
	}
</script>

[slide]
## CSS常用选择器
----
选择器 | 标志 | 用法
:----: | :-----: | :----:
元素选择器 | | p { }
id选择器 | # | #id_1 { }
类选择器 | . | .center { }
属性选择器 | [] | [title = one] { }
后代选择器 | | ul li { }
子选择器 | > | div > span { }
相邻兄弟选择器 | + | h1 + p { }

[slide]
## CSS布局
### 块级元素和行内元素
----
* 块级元素 <br> {:&.moveIn}
> 通常浏览器会在块级元素前后另起一个新行，块级元素可以包含行内元素和其他块级元素
* 行内元素 <br>
> 只占据它对应标签的边框所包含的空间
* 改变元素默认布局模式——display <br>
> display:block 显示为块级元素，前后带有换行符<br>
	display:inline 显示为内联元素，前后无换行符

[slide]
###常用块级元素和行内元素
---
<div class="columns-2">
<table class="table table-hover">
	<thead>
    <tr>
      <th style="text-align: center;">块级元素</th>
      <th style="text-align: center;">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;canvas&gt;</td>
      <td>绘制图形</td>
    </tr>
    <tr>
      <td>&lt;div&gt;</td>
      <td>文档分区</td>
    </tr>
    <tr>
      <td>&lt;footer&gt;/&lt;header&gt;</td>
      <td>区段尾或页尾/区段头或页头</td>
    </tr>
    <tr>
      <td>&lt;form&gt;</td>
      <td>表单</td>
    </tr>
    <tr>
      <td>&lt;h1&gt;, &lt;h2&gt;, &lt;h3&gt;, <br> &lt;h4&gt;, &lt;h5&gt;, &lt;h6&gt;</td>
      <td>标题级别 1-6</td>
    </tr>
    <tr>
      <td>&lt;hr&gt;</td>
      <td>水平分割线</td>
    </tr>
    <tr>
      <td>&lt;ol&gt;/&lt;ul&gt;</td>
      <td>有序列表/无序列表</td>
    </tr>
    <tr>
      <td>&lt;p&gt;</td>
      <td>行</td>
    </tr>
    <tr>
      <td>&lt;section&gt;</td>
      <td>一个页面区段</td>
    </tr>
    <tr>
      <td>&lt;table&gt;</td>
      <td>表格</td>
    </tr>
  </tbody>
</table>

<table class="table table-hover">
	<thead>
    <tr>
      <th style="text-align: center;">行内元素</th>
      <th style="text-align: center;">描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;a&gt;</td>
      <td>锚点</td>
    </tr>
    <tr>
      <td>&lt;br&gt;</td>
      <td>换行</td>
    </tr>
    <tr>
      <td>&lt;button&gt;</td>
      <td>按钮</td>
    </tr>
    <tr>
      <td>&lt;img&gt;</td>
      <td>图片</td>
    </tr>
    <tr>
      <td>&lt;input&gt;</td>
      <td>输入框</td>
    </tr>
    <tr>
      <td>&lt;label&gt;</td>
      <td>标签</td>
    </tr>
    <tr>
      <td>&lt;map&gt;</td>
      <td>图片区块</td>
    </tr>
    <tr>
      <td>&lt;span&gt;</td>
      <td>组合行内元素</td>
    </tr>
    <tr>
      <td>&lt;select&gt;</td>
      <td>选择框</td>
    </tr>
    <tr>
      <td>&lt;textarea&gt;</td>
      <td>多行文本</td>
    </tr>
  </tbody>
</table>
</div>

[slide]
[note]
* 块级元素和行内元素规定元素占据一整行还是只占据内容的宽度
* 框模型规定元素内容的宽度和高度，元素的内边距、外边距以及边框的样式
* margin:10px 5px 15px 20px; 上外边距是10px,右外边距是5px,下外边距是15px,左外边距是20px
* margin:10px 5px 15px; 上外边距是10px, 右外边距和左外边距是5px, 下外边距是15px
[/note]
## CSS布局
### 框模型
----
规定了元素框处理元素内容、内边距、边框和外边距的方式
<div class="columns-2">
  <div><img style="width: 500px;height: 350px;margin-top:20px;margin-bottom: 20px" src="/cssbox.png"></div>
  <div class="marginsty">
    <span> margin:10px 5px 15px 20px;</span>
    <span> margin:10px 5px; </span>
    <span> margin:10px; </span>
    <hr/>
    <span> margin-top:10px; </span>
    <span> margin-right:10px; </span>
    <span> margin-bottom:10px; </span>
    <span> margin-left:10px; </span>
  </div>
</div>

<div>
	<span>ps:</span>
	<span style="text-align: left !important;">增加内、外边距和边框不会影响内容区域的尺寸，<br>但是会增加元素框的总尺寸</span>
</div>

<style>
  .marginsty{
    padding-top: 50px;
  }
  .marginsty span{
    display: block;
    text-align: left
  }
</style>

[slide]
[note]
* 框模型规定元素自身的大小和边距，位置属性控制元素相对于整个视图的位置
* position属性为更精准定位的需求提供服务
[/note]
## CSS布局
### 位置
----
控制网页元素相对正常布局、周边元素、父容器或者主视图/窗口的位置 <br>
* float属性 -> 允许元素浮动到另外一个元素的左侧或右侧 {:&.zoomIn}
<div class="div_pos"> left | right | none | inherit </div>
* position属性 -> 允许将一个元素从它在页面的原始位置准确地移动到另外一个位置 <br>
<div class="div_pos"> static | <a onclick="relative()">relative</a> | <a onclick="absolute()">absolute</a> | <a onclick="fixed()">fixed</a> | inherit </div>
<div style="height: 90px">
<p id="relative" style="display:none;position:relative;padding-left: 125px;top:20px">元素框偏移某个距离,相对于其正常位置进行定位</p>
<p id="absolute" style="display:none;position:relative;padding-left: 265px;top:20px;">元素框从文档流完全删除，相对于static 定位以外的第一个父元素进行定位</p>
<p id="fixed" style="display:none;position:relative;padding-left:405px;top:20px;">相对于浏览器窗口进行定位</p>
</div>

<style>
	.div_pos{
		background-color:rgb(11,108,50);
		height: 45px;
		padding-left: 20px
	}
</style>

<script>
	function relative(){
		document.getElementById('relative').style.display = 'block'
		document.getElementById('absolute').style.display = 'none'
		document.getElementById('fixed').style.display = 'none'
	}
	function absolute(){
		document.getElementById('relative').style.display = 'none'
		document.getElementById('absolute').style.display = 'block'
		document.getElementById('fixed').style.display = 'none'
	}
	function fixed(){
		document.getElementById('relative').style.display = 'none'
		document.getElementById('absolute').style.display = 'none'
		document.getElementById('fixed').style.display = 'block'
	}
</script>

[slide]
# Vue.js
## 一套构建用户界面的渐进式框架

[slide]
##安装
----
通过&lt;script&gt;直接引入 {:&.pull-left}

<br><pre><code>&lt;script type="text/javascript" src="https://unpkg.com/vue@2.4.2/dist/vue.js" &gt;&lt;/script&gt;
</code></pre>

[slide]
##Vue实例
----
* Vue.js应用通过new Vue创建一个Vue的根实例启动 {:&.rollIn}
* 实例化Vue时需要传入一个选项对象
>数据、模板、挂载元素、方法、生命周期钩子
* 只有被代理的属性是响应式的，值的改变会触发视图重新渲染
<pre><code>var data = { a: 1 }
var vm = new Vue({
    // 选项
    data: data
})
</code></pre>

[slide]
##MVVM模型与数据双向绑定
----
* Model -> View -> ViewModel
* 模型到视图 -> {{msg}}
* 视图到模型 -> v-model

[slide]
##模板语法
----
* 插值 {:&.rollIn} <br>
 + 文本 -- &lt;span&gt;Message:{{msg}}&lt;/span&gt;
 + 纯HTML -- &lt;div v-html="rawHtml"&gt;&lt;/div&gt;
 + 属性 -- &lt;div v-bind:id="dynamicId"&gt;&lt;/div&gt;
 + JavaScript表达式 -- {{ ok ? 'YES' : 'NO' }} {{message.split('').reverse().join('') }}
* 指令<br>
> 指令(Directives)是带有v-前缀的特殊属性
* 过滤器<br>
> 在{{ }}绑定和v-bind表达式中使用
{{ message | filterA | filterB }}

[slide]
##计算属性
----
<div class="columns-2">
  <div>
     <pre><code>&lt;div id="example"&gt;
  {{ message.split('').reverse().join('')}}
&lt;/div&gt;
    </code></pre>
    <p style="text-align:left">模板不再简单和清晰</p>
    <p style="text-align:left">多次使用时要重复写逻辑</p>
    <p style="color:yellow;margin-top:50px">对于任何复杂逻辑，都应当使用计算属性
</p>
<button type="button" class="btn btn-default" style="float:right" onclick="showComputed()">
  <span class="glyphicon glyphicon-arrow-right"></span>
</button>
  </div>
  <div id="computedCode" style="visibility:hidden">
    <pre><code>&lt;div id="example"&gt;
   计算属性: "{{ reversedMessage }}"
&lt;/div&gt;
    </code></pre>
    <pre><code>var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  }
})
    </code></pre>
  </div>
</div>

<script>
function showComputed(){
  document.getElementById("computedCode").style.visibility = "visible";
}
</script>

[slide]
##条件渲染和列表渲染
###条件渲染
----
<div style="text-align: left">&bull; v-if</div>
<h4 style="text-align: left;padding-left:50px">v-if为true时渲染，v-else表示v-if的"else"块，v-else-if表示v-if的"else if"块</h4>
<div class="row">
<div class="col-md-6">
<pre><code>&lt;div v-if="type === 'A'"&gt;A&lt;/div&gt;
&lt;div v-else-if="type === 'B'"&gt;B&lt;/div&gt;
&lt;div v-else&gt;Not A/B&lt;/div&gt;
</code></pre>
</div>
<div id="vif-example" class="col-md-6">
  <div><label>type:</label><input v-model="type" style="color:black"></div>
  <div v-if="type === 'A'">A</div>
  <div v-else-if="type === 'B'">B</div>
  <div v-else>Not A/B</div>
</div>
</div>
<div style="text-align: left">&bull; v-show</div>
<h4 style="text-align: left;padding-left:50px">v-show为true时显示，v-show的元素始终会被渲染并保留在DOM中</h4>

<script type="text/javascript" src="https://unpkg.com/vue@2.4.2/dist/vue.js"></script>
<script>
new Vue({
  el: '#vif-example',
  data: {
    type: ''
  },
})
</script>

[note]
<pre><code>
&lt;div id="vif-example" class="col-md-6"&gt;
  &lt;div&gt;&lt;label&gt;type:&lt;/label&gt;&lt;input v-model="type" style="color:black"&gt;&lt;/div&gt;
  &lt;div v-if="type === 'A'"&gt;A&lt;/div&gt;
  &lt;div v-else-if="type === 'B'"&gt;B&lt;/div&gt;
  &lt;div v-else&gt;Not A/B&lt;/div&gt;
&lt;/div&gt;

&lt;script&gt;
new Vue({
  el: '#vif-example',
  data: {
    type: ''
  },
})
&lt;/script&gt;
</code></pre>
[/note]

[slide]
###列表渲染
----
用v-for指令根据一组数组的选项列表进行渲染
<div class="row">
<pre class="col-md-4"><code>
&lt;ul id="example-1"&gt;
  &lt;li v-for="item in items"&gt;
    {{ item.message }}
  &lt;/li&gt;
&lt;/ul&gt;
</code></pre>
<pre class="col-md-4"><code class="javascript">
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      {message: 'One' },
      {message: 'Two' }
    ]
  }
})
</code></pre>
<div id="example-1" class="col-md-4" style="color:black">
  <input v-model="newTodoText" v-on:keyup.enter="addNewTodo" placeholder="Add a todo">
  <ul>
    <li v-for="(item, index) in items" v-bind:key="item.id" v-bind:title="item.message ">
      {{ item.message  }}
      <button class='btn btn-default' v-on:click="items.splice(index, 1)">X</button>
    </li>
  </ul>
</div>
</div>

<script>
new Vue({
  el: '#example-1',
  data: {
    newTodoText: '',
    items: [
      {
        id: 1,
        message : 'One',
      },
      {
        id: 2,
        message : 'Two',
      }
    ],
    nextTodoId: 3
  },
  methods: {
    addNewTodo: function () {
      this.items.push({
        id: this.nextTodoId++,
        message : this.newTodoText
      })
      this.newTodoText = ''
    }
  }
})
</script>

[note]
<pre><code  style="height:550px">&lt;div id="example-1"&gt;
  &lt;input v-model="newTodoText" v-on:keyup.enter="addNewTodo" placeholder="Add a todo"&gt;
  &lt;ul&gt;
    &lt;li v-for="(item, index) in items" v-bind:key="item.id" v-bind:title="item.message "&gt;
      {{ item.message  }}
      &lt;button class='btn btn-default' v-on:click="items.splice(index, 1)"&gt;X&lt;/button&gt;
    &lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;

&lt;script&gt;
new Vue({
  el: '#example-1',
  data: {
    newTodoText: '',
    items: [
      {
        id: 1,
        message : 'One',
      },
      {
        id: 2,
        message : 'Two',
      }
    ],
    nextTodoId: 3
  },
  methods: {
    addNewTodo: function () {
      this.items.push({
        id: this.nextTodoId++,
        message : this.newTodoText
      })
      this.newTodoText = ''
    }
  }
})
&lt;/script&gt;
</code></pre>
[/note]

[slide]
##事件处理器
----
* 监听事件 {:&.fadeIn}
 + 通过v-on指令监听原生DOM事件
 > &lt;button v-on:click="greet(param,$event)"&gt;Greet&lt;/button&gt;
* 事件修饰符
 + 处理DOM事件细节
 > v-on:click.stop="greet" 调用 event.stopPropagation() <br>
 v-on:submit.prevent="greet" 调用 event.preventDefault()

[slide]
##组件
###扩展HTML元素，封装可重用的代码
----
<pre><code>//First
//创建一个组件
var Child = {
  template: '&lt;div&gt;A custom component!&lt;/div&gt;'
}
</code></pre>
<pre><code>//Second
//在实例中注册组件
var vm = new Vue({
  //...
  components: {
    'my-component': Child
  }
})
</code></pre>
<pre><code>&lt;!--Third--&gt;
&lt;!--在父模板中使用组件--&gt;
&lt;div&gt;
  &lt;my-component&gt;&lt;/my-component&gt;
&lt;/div&gt;
</code></pre>

[slide]
##组件通信
----
###父子组件的通讯方式可以总结为 props down, events up
<img style="width:320px;height:300px;margin-top:30px" src="/vuecomponent.png">

[slide]
<div class="row">
<div class="col-md-6">
<pre><code>//子组件
var Child = {
  data: function () {
    return {
      counter: 0
    }
  },
  props: ['message'],
  template: "&lt;div&gt;&lt;span&gt;{{ myMessage }}&lt;/span&gt;
    &lt;button v-on:click='incrementCounter'&gt;
      {{ counter }}&lt;/button&gt;&lt;div&gt;",
  methods:{
    incrementCounter:function(){
      this.counter += 1
      this.$emit('increment')
    }
  }
}
</code></pre>
</div>
<div class="col-md-6">
<pre><code>//父实例
var vm = new Vue({
  el: '#example',
  data: {
    parentMsg: 'Hello',
    total: 0
  },
  components: {
    Child
  },
  methods:{
    incrementTotal: function () {
      this.total += 1
    }
  }
})
</code></pre>
</div>
</div>
<div class="row">
<div class="col-md-12">
<pre><code>&lt;!-- prop使用 --&gt;
&lt;div id="example"&gt;
  &lt;input v-model="parentMsg"&gt;
  &lt;child v-bind:message="parentMsg" v-on:increment="incrementTotal"&gt;&lt;/child&gt;
  &lt;p&gt;{{ total }}&lt;/p&gt;
&lt;/div>
</code></pre>
</div>
</div>

[slide]
#### component通讯示例
----
<iframe data-src="https://jsfiddle.net/ouchyaya/628ozrq4/4/" src="about:blank;"></iframe>

[slide]
##总结
----
* DOM {:&.moveIn}
 [对象](#1),[属性](#2),[方法](#3),[事件](#4)
* CSS
 [语法](#8),[选择器](#9),布局([块级元素和行内元素](#10),[框模型](#12),[位置](#13))
* Vue
 [数据绑定](#17),[条件渲染](#20),[列表渲染](#21),[事件处理器](#22),[组件](#23),
