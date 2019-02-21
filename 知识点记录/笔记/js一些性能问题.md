# JavaScript性能优化

## 全局变量污染

全局变量可以削弱程序灵活性，增大了模块之间的耦合性；在多人协作时，如果定义过多的全局变量有可能造成全局变量冲突，也就是全局变量污染问题。

#### 解决思路

##### 定义全局变量命名空间

只创建一个全局变量，并定义该变量为当前应用容器，把其他全局变量追加在该命名空间下。

实例代码：

```
let my={};
        my.name={
            big_name:"小麦",
            small_name:"小小麦"
        };
        my.work={
            school_work:"study",
            family_work:"study"
       };
```

##### 利用匿名函数将脚本包裹起来

实例代码：

```
(function(){

    let exp={};
    let name="aa";

    exp.method=function(){
        return name;
    };

    window.ex=exp;
})();
```

## 减少污染

采用类似C++的命名空间，Java的包的思路。

代码实例：

```
(function(obj){  
    /* 在这里边就与外边隔离了，定义的局部变量不会与外界干扰 */  
    /* 为了跟外界达到共享的目的，还可以为其加入参数，例如obj,在最后调用的时候把相关的参数传进来，例如下边的window */  
      
    let A = {};//定义一个A包  
    let tmp;//临时变量  
  
    A.i = 1;//定义这个包里边的i变量  
    A.func = function(){alert('I am A');};  
      
    obj.A = A;/* 把A包挂到obj底下 */  
      
})(window);  

```

程序员A为全局添加一个A变量，然后他把自己定义的函数/变量全部挂到A底下，这样就跟程序员B所定义的隔离了。

当离开了这个函数域之后，tmp等局部变量被销毁（只要不要存在在闭包里边），程序员A定义的东西通通挂到了变量window.A底下，从而减少了很多污染，避免了不必要的冲突。

## 内存泄漏

内存泄漏：不再用到的内存，没有及时释放。

产生的问题：反应迟缓，崩溃，高延迟，以及其他应用问题。

类比：手机应用软件开太多未及时关闭，导致手机反应迟缓。

#### 常见类型

##### 全局变量

JavaScript 处理未定义变量的方式会在全局对象创建一个新变量，在浏览器中，全局对象是 window ；这样会产生一些意外的全局变量。

##### 被遗忘的计时器或回调函数

代码示例：

```

let element = document.getElementById('button');
function onClick(event) {
    element.innerHTML = 'text';
}

element.addEventListener('click', onClick);
```

老版本的 IE 是无法检测 DOM 节点与 JavaScript代码之间的循环引用，会导致内存泄露。

现代的浏览器使用了更先进的垃圾回收算法，已经可以正确检测和处理循环引用了。换言之，不必非要调用removeEventListener了。

##### 脱离 DOM 的引用

假如你的 JavaScript 代码中保存了表格某一个 td 的引用。将来决定删除整个表格的时候，直觉认为 GC 会回收除了已保存的 td 以外的其它节点。实际情况并非如此：此 td 是表格的子节点，子元素与父元素是引用关系。由于代码保留了 td 的引用，导致整个表格仍待在内存中。

代码示例：

```

let elements = {
    button: document.getElementById('button'),
    image: document.getElementById('image'),
    text: document.getElementById('text')
};

function doStuff() {
    image.src = 'http://some.url/image';
    button.click();
    console.log(text.innerHTML);
    // 更多逻辑
}

function removeButton() {
    // 按钮是 body 的后代元素
    document.body.removeChild(document.getElementById('button'));

    // 此时，仍旧存在一个全局的 #button 的引用
    // elements 对象里面的 button 元素仍旧在内存中，不能被 GC 回收。
}
```

此时，同样的 DOM 元素存在两个引用：一个在DOM树中，另一个在elements对象中。将来删除这些时，需要把两个引用都清除。

##### 闭包

闭包：匿名函数可以访问父级作用域的变量。

代码示例：

```

(function(){
    let leak = '内部变量';// 被闭包所引用，不会被回收
    return function(){
        console.log(leak);
    }
})()

```

## 内存溢出

内存溢出：申请内存时，没有足够的内存空间供其使用。






