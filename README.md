# Note-JavaScript11
DOM,Element对象，对CSS内外联样式的简单操作
### DOM
#### Element对象  
- DOM 访问或操作 HTML 页面内容主要是依靠 DOM 节点树这个模型。但在 DOM 中的三个主要对象，除了 Document 和 Node 之外，还有一个就是 Element 对象。 
- Element 对象描述了所有相同种类的元素所普遍具有的方法和属性，也是访问和操作 HTML 页面内容的主要途径之一
- Element 对象和 Node 对象类似，同样提供了一个 DOM 元素树这个模型。如下图所示:
![DOM 元素树](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/bbXBrek7aIHgcQAW.tk18WIooshZTzePvu2sO*IdGnc!/m/dPIAAAAAAAAA&bo=9gOAAgAAAAADB1U!&rf=photolist)   
##### 遍历元素  
1. 获取父元素  
> 通过 HTML 页面的指定标签查找其父元素

```js
element.parentElement
```
2. 获取子元素 
- firstElementChild: 获取指定标签的第一个子元素。
- lastElementChild: 获取指定标签的最后一个子元素。
- children: 获取指定标签的所有子元素。
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>获取子元素</title>
</head>
<body>
<ul id="parent">
    <li>苹果</li>
    <li>小米</li>
    <li>华为</li>
</ul>
<script>
    /*
        浏览器兼容问题 - IE 8及之前版本浏览器
        * lastElementChild
        * firstElementChild
        * childElementCount
     */
    var parent = document.getElementById('parent');
    // 获取第一个子元素
    var firstChild = parent.firstElementChild;
    console.log(firstChild);
    // 获取最后一个子元素
    var lastChild = parent.lastElementChild;
    console.log(lastChild);
    // 获取所有子元素的集合
    var children = parent.children;
    console.log(children);
    // 获取所有子元素的个数
    var num = parent.childElementCount;
    console.log(num);

    console.log(childElementCount(parent));
    console.log(firstElementChild(parent));
    console.log(lastElementChild(parent));

    console.log(parent.firstChild);

</script>
</body>
</html>
```
3. 获取兄弟元素  
- previousElementSibling: 获取指定节点的前一个兄弟节点。
- nextElementSibling: 获取指定节点的后一个兄弟节点。
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>获取兄弟元素</title>
</head>
<body>
<ul>
    <li>苹果</li>
    <li id="mi">小米</li>
    <li>华为</li>
</ul>
<script>
    var mi = document.getElementById('mi');
    /*
        存在浏览器的兼容问题 - IE 8及之前版本
        * previousElementSibling
        * nextElementSibling
     */
    console.log(mi.previousElementSibling);
    console.log(mi.nextElementSibling);

    /*var parent = mi.parentElement;
    var list = parent.children;
    console.log(list);
    // HTMLCollection对象不能直接调用数组的方法
    /!*var index = list.indexOf(mi);
    console.log(index);*!/
    var arr = [];
    for (var i=0;i<list.length;i++){
        arr.push(list[i]);
    }
    console.log(arr);

    var index = arr.indexOf(mi);
    console.log(index);*/

</script>
</body>
</html>
```
##### 操作属性  
>  Element 对象提供的属性操作的方法，是实际开发中应用最多的。（因为 Element 对象操作属性要比 Node 对象简便。） 
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作属性</title>
</head>
<body>
<ul id="parent">
    <li>苹果</li>
    <li id="mi" class="miClass">小米</li>
    <li>锤子</li>
</ul>
<script>
    // 使用Node对象的方式，添加一个新的子节点 - <li id="huawei">华为</li>
    var newLi = document.createElement('li');
    var text = document.createTextNode('华为');
    newLi.appendChild(text);

    // 属性节点的操作
    // 1. 创建属性节点 -> 只能设置属性名称，而不能设置属性的值
    var attr = document.createAttribute('id');
    // 2. 通过 nodeValue 属性设置指定属性的值
    attr.nodeValue = 'huawei';
    // 3. 只能通过 setAttributeNode() 方法设置属性节点
    newLi.setAttributeNode(attr);

    var parent = document.getElementById('parent');
    parent.appendChild(newLi);

    /*
        Element对象提供操作属性的方式 - 元素的属性
        * 获取指定元素的属性 - getAttribute(attrName)
        * 设置指定元素的属性 - setAttribute(attrName, attrValue)
        * 删除指定元素的属性 - removeAttribute(attrName)
        * 判断指定元素是否具有某个属性 - hasAttribute(attrName)
     */
    var mi = document.getElementById('mi');

    mi.setAttribute('class','mi2Class');
    // mi.setAttributeNode(属性节点);

    console.log(mi.getAttribute('class'));
    console.log(mi.getAttributeNode('class'));

    mi.removeAttribute('class');
    // mi.removeAttributeNode(属性节点);

    console.log(mi.hasAttribute('class'));// false
    console.log(mi.hasAttributes());// 是否包含属性

</script>
</body>
</html>
```
##### DOM查询  
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DOM查询</title>
</head>
<body>
<ul id="parent">
    <li>苹果</li>
    <li id="xigua">西瓜</li>
    <li>香蕉</li>
</ul>
<script>
    /*
        Element对象也提供了相关的DOM查询的方法
        * 返回值为HTMLCollection，依旧是动态NodeList
          * getElementsByTagName()
          * getElementsByClassName()
        * 返回值为NodeList，依旧是静态NodeList
          * querySelector()
          * querySelectorAll()
        Document、Node和Element对象之间的关系
        * Document和Element对象都是继承于Node
        * Document提供的DOM查询与Element提供的DOM查询之间没有关系
     */
    console.log(Element.prototype instanceof Node);// true

    console.log(Element.prototype instanceof Document);// false
    console.log(Document.prototype instanceof Element);// false

    console.log(Document.prototype instanceof Node);// true
    // 元素节点，也是元素
    var parent = document.getElementById('parent');

    console.log(parent.getElementsByTagName('li'));
    console.log(parent.querySelectorAll('li'));

    // console.log(parent.getElementById('xigua'));
</script>
</body>
</html>
```
##### 获取或更新文本  
- 操作文本  
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作文本</title>
</head>
<body>
<p id="p1">这是一个段落内容.</p>
<script>
    // nodeValue属性
    /*var p1 = document.getElementById('p1');// 1. 获取元素节点
    var textNode = p1.firstChild;// 2. 通过元素节点的字节点方式 -> 文本节点
    console.log(textNode.nodeValue);// 3. 通过 nodeValue 获取文本内容*/
    /*
        textContent属性 -> 该属性是Node对象的属性
        * 注意 -> 浏览器兼容问题 -> IE 8及之前的版本不支持
        * IE 8及之前版本的浏览器提供了另一个属性
          * innerText属性 -> 作用与textContent属性作用保持一致
      */
    var p1 = document.getElementById('p1');// Node Element
    console.log(p1.textContent);
    console.log(p1.innerText);

    // 提供浏览器的兼容解决方法
    function getText(node){
        var result;
        if (node.textContent !== undefined){
            result = node.textContent;
        } else {
            result = node.innerText;
        }
        return result;
    }
    // DOM的代码逻辑尽量遵循W3C的规范标准 -> 不能只看浏览器的情况

</script>
</body>
</html>
```
- innerText:不能获取被 CSS 样式隐藏的文本内容
- textContent:可以获取全部文本内容     
##### 获取或更新 HTML
1. innerHTML属性 
```html   
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>innerHTML</title>
</head>
<body>
<p id="p1">这是一个段落. <a href="#">链接</a></p>
<div id="show"></div>
<script>
    var p1 = document.getElementById('p1');
    // 获取指定元素的所有后代元素的文本内容
    // console.log(p1.textContent);
    // 获取指定元素内部的所有HTML源代码
    console.log(p1.innerHTML);
    // 设置指定元素内部的HTML源代码
    p1.innerHTML = '<strong>这是新的内容.</strong>';

    // 向<div>标签添加一个无序列表
    var ul = document.createElement('ul');
    // DOM方式操作
    /*var li = document.createElement('li');
    li.setAttribute('id','mi');
    li.textContent = '小米';

    ul.appendChild(li);*/

    // innerHTML属性方式操作 - 安全问题(innerHTML属性不操作用户输入的内容)
    ul.innerHTML = '<li id="mi">小米</li><li id="huawei">华为</li>';

    var show = document.getElementById('show');
    show.appendChild(ul);

</script>
</body>
</html>
``` 
2. innerHTML的相关问题   
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>innerHTML的问题</title>
</head>
<body>
<!--
    提交的地址链接
    http://localhost:63342/code/07_innerHTML的问题.html?data=zhangwuji
-->
<form id="myform" action="#" method="get">
    <input type="text" id="data" name="data">
    <input type="submit" value="提交">
</form>
<div id="show"></div>
<script>
    var myform = document.getElementById('myform');
    // 提交事件
    myform.onsubmit = function(){
        var data = document.getElementById('data');
        var str = data.value;

        //eval(str);

        var show = document.getElementById('show');
        show.innerHTML = str;

        return false;
    }

    //cookies - 存在安全上的隐患

</script>
</body>
</html>
```
#### CSS的相关操作  
1. 操作CSS
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作css</title>
    <style>
        .pClass {
            color: lightseagreen;
        }
        .aClass {
            color: lightblue;
        }
    </style>
</head>
<body>
<p id="p1" style="color: lightcoral">这是一个段落内容.</p>
<p id="p2" class="pClass">这是一个段落内容.</p>
<script>
    // Element对象提供操作属性的方法
    var p1 = document.getElementById('p1');

    // 获取或设置style属性值的方式 -> 获取或设置CSS样式
    var result = p1.getAttribute('style');
    // CSS样式的内容 -> 是字符串类型
    console.log(result);
    // 修改CSS样式的内容
    p1.setAttribute('style','color:#000');

    var p2 = document.getElementById('p2');
    // 获取或设置class属性值的方式
    var result2 = p2.getAttribute('class');
    // CSS样式的类选择器名称
    console.log(result2);
    // 修改CSS样式的内容
    p2.setAttribute('class','aClass');
</script>
</body>
</html>
```
- 如果设置CSS样式时，使用了`!important`预定义的CSS样式优先级最高，会导致改变内联样式失效。
- 在修改例如background-color这样的CSS属性时，不能使用 element.style.background-color 这种方式，浏览器会解析成 JavaScript 的表达式。最终会报错。
- 所有例如background-color这样的CSS属性在使用时，必须要改为`驼峰式`命名方式（例如 backgroundColor）。    

2. 操作内联样式  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作内联样式</title>
</head>
<body>
<p id="p1" style="color: hotpink">这是一个段落内容.</p>
<script>
    // 内联样式的有效范围 -> 当前标签
    var p1 = document.getElementById('p1');

    console.log(HTMLParagraphElement.prototype);

    /*
        获取到的标签(Node对象或Element对象) - style属性
        * 返回值 - CSSStyleDeclaration对象
          * 经过测试发现 -> 该对象中只存在属性，而没有方法
          * 作用 - 该对象用于封装有关CSS样式属性的对象
     */
    var result = p1.style;
    console.log(result.color);

</script>
</body>
</html>
```
![两种方式获取内联样式的对比图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/ATJ7KyoIf3BEeJLT58r21nJWVOKV6PtwTmHIy7ywGkg!/m/dPMAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)   

3. 操作外联样式  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作外联样式</title>
    <link rel="stylesheet" href="style.css">
    <style>
        /* 一个选择器 -> 一个CSS规则 */
        .pClass {
             color: hotpink;
         }
        .miClass {
            background-color: lightseagreen;
        }
    </style>
</head>
<body>
<p id="p1" class="pClass">这是一个段落内容.</p>
<script>
    // 通过获取<style>标签
    /*var style = document.getElementsByTagName('style')[0];
    // 得到的CSS内容 -> 字符串类型
    console.log(style.innerHTML);*/

    /*
        document.styleSheets属性
        * 返回值 - 一个包含所有外联样式的集合
          * styleSheetList对象 -> 是类数组对象
        * 存储的顺序 -> 是按照外联样式定义的前后顺序排列
     */
    var styleSheets = document.styleSheets;
    console.log(styleSheets[0]);// <link>
    /*
        styleSheetList对象中每个元素都是一个 CSSStyleSheet 对象
        * 该对象就代表某一个具体的CSS样式表
        * 属性
          * href - 代表<link>标签中的href属性
          * disabled - 表示当前的CSS样式表是否为可用，默认为可用
          * cssRules/rules - 返回CSSRuleList对象
            * CSSRuleList对象 - 包含当前CSS样式表中每个CSS规则内容
     */
    var cssStyleSheet = styleSheets[1];// <style>
    console.log(cssStyleSheet.cssRules);

    /*
        CSSRuleList对象中每一个元素都是一个CSSStyleRule对象
        * 该对象就代表某一个具体的CSS规则（一个选择器）
        * 属性
          * cssText - 获取当前CSS规则的所有内容，是字符串类型
          * selectorText - 获取当前CSS规则的选择器名称
          * style - 返回CSSStyleDeclaration对象
            * 该对象包含了所有有关CSS属性的对象
     */
    var cssRule = cssStyleSheet.cssRules[1];
    console.log(cssRule);

    var cssStyle = cssRule.style;
    console.log(cssStyle.backgroundColor);

    /*
        如果静态HTML页面的标签只具有外联样式的话
        * 由于内联样式的优先级别高于外联样式
        * 通过为指定标签设置内联样式的方式 -> 覆盖原本静态HTML页面中具有的外联样式
     */

</script>
</body>
</html>
```
![获取外联样式的内容](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/euuFYgDfZ4KL*d.qcL9j1p4ESe8t176.XPX4i4Yg0LQ!/m/dPMAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)     




