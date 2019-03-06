# DOM

当网页被加载时，浏览器会创建页面的文档对象模型(DOM)。

通过document提供的一些能够操作页面内容的方法或者属性，赋予开发者操作页面的能力。

#### DOM可以操作什么？

a.能够改变页面中的所有 HTML 元素

b.能够改变页面中的所有 HTML 属性

c.能够改变页面中的所有 CSS 样式

d.能够对页面中的所有事件做出反应


## 查找 HTML 元素

document.querySelector()<br>
返回文档中匹配指定的CSS选择器的第一元素

document.querySelectorAll()<br>
HTML5中引入的新方法，返回文档中匹配的CSS选择器的所有元素节点列表

document.getElementById()<br>
返回对拥有指定 id 的第一个对象的引用。

document.getElementsByTagName()<br>
返回带有指定标签名的对象集合

document.getElementsByName()<br>
返回带有指定名称的对象集合。

document.getElementsByClassName()<br>
返回文档中所有指定类名的元素集合，作为 NodeList 对象

## 改变 HTML 元素的内容

document.innerHTML 设置或获取标签所包含的标签+文本信息

document.innerText 设置或获取标签所包含的文本信息

## 改变 HTML 元素的样式

document.getElementById(id).style.property=新样式

示例代码：
```
document.getElementById("p2").style.color="blue";
```

封装一个兼容的获取样式的方法，示例代码：

```
//tag是标签，attr是需要获取的属性。
function getStyle(tag,attr){
    if(tag.currentStyle[attr]){
        return tag.currentStyle[attr];
    }else{
        return getComputedStyle(tag,null)[attr];
}
```

## DOM的节点类型

元素节点 = 1

属性节点 = 2

文本节点 = 3（空格、换行也是文本）

注释节点 = 8

document = 9

代码示例：

```
//输出9
console.log(document.nodeType);
```


## 节点的三大属性

nodeType：用于获取节点的类型，获取结果是一个数值

nodeName：节点名，元素节点的节点名就是标签名

nodeValue：节点值，元素节点没有节点值，值为null,文本节点的节点值就是文本，属性节点的节点值就是该属性值。

## 判断是否有子节点

parentNode.hasChildNodes()：有子节点返回值是true，没有子节点返回值是false；空格内节点被认为是文本节点,所以如果留下任何空格或换行一个元素,该元素仍有子节点。

```
//  div.hasChildNodes()返回true；span.hasChildNodes()返回false
<div>
    <span></span>
    这里有文本
</div>
```

## 查找节点

parentNode：查找某个元素的父节点方法

childNodes：可以得到某个节点的所有子节点，包含文本节点（空格和换行）

children：可以得到某个节点中的所有元素子节点（不是标准方法，但是所有浏览器都支持）

#### 兄弟节点之间查找

previousSibling 查找上个兄弟节点方法（有可能是文本节点）

previousElementSibling 查找某个元素的上个兄弟节点方法（ie低版本不支持）

nextSibling 查找下个兄弟节点方法（有可能是文本节点）

nextElementSibling 查找某个元素的下个兄弟节点方法（ie低版本不支持）

#### 查找某个子节点

firstElementChild：找到某个元素的第一个子节点（ie低版本不支持）

lastElementChild：找到某个元素的最后一个子节点（ie低版本不支持）

firstChild：第一个子节点（有可能是文本节点）

lastChild：最后一个子节点（有可能是文本节点）

## 获取子节点

node.firstChild：表示第一个子节点（返回全部元素，包括空格以及元素等）

node.lastChild：最后一个子节点（返回全部元素，包括空格以及元素等）

## 获取元素子节点

node.firstElementChild 第一个元素子节点（返回的是element元素，而不是文本元素或注释）

node.lastElementChild 最后一个元素子节点（返回的是element元素，而不是文本元素或注释）

## 有定位属性的节点

offsetParent：获取最近的有定位属性的祖先节点，如果祖先节点没定位默认是body。

offsetLeft / offsetTop：获取最近的有定位属性的祖先节点的距离,子级的外边框到有定位的最近父级的内边框。

## 元素的操作

#### 创建节点

document.createElement(tagName)：通过标签名的形式创建一个元素

#### 添加子节点

parentNode.appendChild(childNode)：往一个节点里边添加一个子节点，注意是添加在最后

parentNode.insertBefore(childNode1,childNode2)：往一个节点的指定子节点前边插入一个节点；如childNode1插入到childNode2前边

#### 删除子节点

parentNode.removeChild(childNodes)：从一个节点中删除指定的子节点，如果指定的子节点没有就会报错

#### 替换节点

parentNode.replaceChild(node,childNode)：node是用来替换的节点，childNode被替换的子节点，两个参数都必须写。

#### 克隆节点

node.cloneNode(boolean)：克隆一个节点，true：克隆元素和元素包含的子孙节点；false：克隆元素但不包含元素的子孙节点；事件是不会克隆。

代码示例：

```
let box=document.getElementById("box");

//如果传入的是true那么就是标签和内容一起复制。
let newNode=box.cloneNode(true);

//如果传入的false那么就是只克隆标签不再复制内容。
let newNode=box.cloneNode(false);
```

##### 注意

appendChild / insertBefore / replaceChild 在操作一个已有的元素时是将已有的元素移动，而不是复制一份进行操作。

## 元素的属性操作

node.getAttribute(attr)：获取元素行间的指定属性名的属性值

node.setAttribute(attr,value)：设置元素行间的指定属性名的属性值

node.removeAttribute(attr)：删除元素行间的指定属性

## 表单操作

table.tHead：获取表格头部

table.tFoot：获取表格底部

table.tBodies：获取表格主体，获取到的是一个集合

代码示例：
```
<body>
	<table border="" id="box">
        <thead id="thead">
            <tr>
                <th>头1</th>
                <th>头2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>内容一</td>
                <td>内容二</td>
            </tr>
            <tr>
                <td>内容一</td>
                <td>内容二</td>
            </tr>
        </tbody>
        <tbody>
            <tr>
                <td>内容一</td>
                <td>内容二</td>
            </tr>
            <tr>
                <td>内容一</td>
                <td>内容二</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>统计一</td>
                <td>统计二</td>
            </tr>
        </tfoot>
    </table>
<script type="text/javascript">

    //  tBodies[n].rows / tHead.rows / tFoot.rows：获取的是表格的行，也就是tr
    //  rows[n].cells：获取的是单元格，也就是td

    var box = document.getElementById('box');

    <!--  获取表格头部 -->
    box.tHead.style.borderColor = 'red';

    box.rows[1].style.background = 'greenyellow';

    <!-- 获取表格底部 -->
    box.tFoot.style.background = '#ccc';

    <!-- 获取表格主体，获取到的是一个集合 -->
    box.tBodies[1].style.background = 'blue';
    box.tBodies[0].rows[0].cells[1].style.background = 'pink';

</script>
</body>
```

## 获取元素宽高

#### 可视区的宽/高

document.documentElement.clientWidth

document.documentElement.clientHeight

#### 元素的宽/高

1、不计算边框，加上padding

element.clientWidth / element.clientHeight

2、计算边框，加上padding

element.offsetWidth / element.offsetHeight

## 获取位置

element.getBoundingClientRect()：获取元素的盒模型信息返回值为一个对象，包含left、top、right、width、height等属性相对于浏览器可视区域名。

注意：获取的值是会根据滚动条变化的


