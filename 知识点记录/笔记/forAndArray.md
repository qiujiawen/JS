## 跳出多层循环

break 语句可用于跳出循环；跳出循环后，会继续执行该循环之后的代码（如果有的话）

continue 用于跳过循环中的一个迭代，如果出现了指定的条件，然后继续循环中的下一个迭代

```
outerloop:
for (var i = 0; i < 10; i++)
{
    innerloop:
    for (var j = 0; j < 10; j++)
    {
        if (j > 3) break;
        if (i == 2) break innerloop;
        if (i == 4) break outerloop;   
    }
}
```

总结：

1、无标签：当 break 和 continue 同时用于循环时，没有加标签，此时默认标签为当前"循环"的代码块；当 break 用于 switch 时，默认标签为当前的 switch 代码块；

2、有标签：break 标签名；会跳出该标签名的代码块

## 判断是否是数组

在JavaScript中，可以通过typeof操作符来判断基本数据类型(Undefined、Null、Boolean、Number和String)，但是typeof对于对象的判断是不准确的，因为特殊值Null被认为是一个空的对象的引用。

因此在ES5还是ES6中，最可靠和最安全的数组判断方法是使用原生的Array.isArray()。