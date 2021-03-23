---
title: jQuery基础
tags:
---

## jQuery是什么?
jQuery 是一个高效、精简并且功能丰富的 JavaScript 工具库.从命名可以看出jQuery最主要的用途是用来做查询（jQuery=js+Query）,在jQuery官方Logo下方还有一个副标题（write less, do more）, 体现了jQuery除了查询以外,还能让我们对HTML文档遍历和操作、事件处理、动画以及Ajax变得更加简单.

## 为什么要使用jQuery?
- 强大的选择器: 通过jQuery查找DOM元素比原生js使用的代码更简,而且jQuery允许开发者使用CSS1-CSS3几乎所有的选择器以及jQuery独创的选择器
- 链式调用: 可以通过.(点)不断的调用jQuery对象的方法,而原生js不一定
- 隐式遍历(迭代): 一次操作多个元素
- 读写合一: 读写数据使用的是一个函数
- 事件处理
- DOM操作(C增U改D删)
- 样式操作
- 动画
- 丰富的插件支持
- 浏览器兼容
    * 1.x: 兼容ie678,但相对其它版本文件较大,官方只做BUG维护,功能不再新增,最终版本: 1.12.4 (2016年5月20日)
    * 2.x: 不兼容ie678,相对1.x文件较小,官方只做BUG维护,功能不再新增,最终版本：2.2.4 (2016年5月20日)
    * 3.x: 不兼容ie678,只支持最新的浏览器,很多老的jQuery插件不支持这个版本,相对1.x文件较小,提供不包含Ajax/动画API版本

## 入口函数
jQuery与JavaScript加载模式对比
``` js
    <script>
        // 原生js入口函数
        window.onload=function(){
        }

        // jQuery入口函数(四种方式).
        // 基本方式
        $(document).ready(function(){
        })
        // jQuery替代$
        jQuery(document).ready(function(){
        })
        // 推荐使用,此方式最简洁
        $(function(){
        })
        // jQuery替代$
        jQuery(function(){
        })
    </script>
```
||window.onload|$(document).ready()|
|---|---|---|
|执行时机|必须等待网页全部加载完毕(包括 图片等),然后再执行包裹代码|只需要等待网页中的DOM结构 加载完毕,就能执行包裹的代码|
|执行方式|当存在多个入口函数存在时,最后面的会覆盖前面的函数,只执行最后面函数中的代码|当有多个入口函数存在时,会依次执行函数中的代码|

## 关于$符号
\$符号是jQuery框架对外暴露的一个全局变量,jQuery框架之所以提供了jQuery访问还提供\$访问,就是为了提升开发者的编码效率
``` js
    // 此代码是jQuery框架源码实现
    window.jQuery = window.$ = jQuery;
```

##### $符号冲突问题
很多js的框架都提供了类似jQuery这样的便捷访问方式,所以很有可能某一天我们在使用多个框架的时,多个框架作者提供的便捷访问方式冲突(A框架通过\$访问,B框架也通过\$访问)
- 释放\$符的使用权,当便捷访问符号发生冲突时,我们可以释放\$使用权, 释放之后只能使用jQuery
  ``` js
    <script>
        <!-- 在使用jQuery之前指定自定义符号 -->
        jQuery.noConflict();
        <!-- 使用 jQuery -->
        jQuery(function () {
        });
        <!-- 使用其他库的 $() -->
        $("content").style.display = 'none';
    </script>
  ```
- 自定义访问符号,当便捷访问符号发生冲突时,我们可以自定义便捷访问符号
  ``` js
    <script>
        <!-- 在使用jQuery之前指定自定义符号 -->
        var tj = jQuery.noConflict();
        <!-- 和使用$一样通过自定义符号调用jQuery -->
        tj(function () {
        });
    </script>
  ```
## jQuery核心函数
在jQuery文档中,jQuery核心函数一共3大类4小类
1. jQuery(callback): \$(document).ready()的简写.允许你绑定一个在DOM文档载入完成后执行的函数.这个函数的作用如同\$(document).ready()一样,只不过用这个函数时,需要把页面中所有需要在DOM加载完成时执行的\$()操作符都包装到其中来.从技术上来说,这个函数是可链接的--但真正以这种方式链接的情况并不多.你可以在一个页面中使用任意多个\$(document).ready事件.
   ``` js
        <script>
            $(function () {
                alert();
            });
        </script>
   ```
2. jQuery([sel,[context]]): 这个函数接收一个包含CSS选择器的字符串,然后用这个字符串去匹配一组元素.jQuery的核心功能都是通过这个函数实现的.jQuery中的一切都基于这个函数,或者说都是在以某种方式使用这个函数.这个函数最基本的用法就是向它传递一个表达式(通常由CSS选择器组成),然后根据这个表达式来查找所有匹配的元素.默认情况下, 如果没有指定context参数,\$()将在当前的HTML document中查找DOM元素;如果指定了context参数,如一个DOM元素集或jQuery对象,那就会在这个context中查找.在jQuery1.3.2以后,其返回的元素顺序等同于在context中出现的先后顺序.
   - 接收一个包含CSS选择器的字符串,然后用这个字符串去匹配一组元素,并包装成jQuery对象
    ``` js
        <script>
            $(function () {
                <!-- 利用jquery获取所有div,得到的是一个jQuery对象 -->
                var $box = $("div");
                console.log($box);

                <!-- 利用js原生语法获取所有div,得到的是一个js对象 -->
                var box = document.getElementsByTagName("div");
                console.log(box);
            });
        </script>
    ```
   - 原生JS对象和jQuery对象相互转换
    ``` js
        <script>
            $(function () {
                var $box = $("#box");
                $box.text("新的数据");
                <!-- jQuery对象不能使用原生js对象的方法 -->
                $box.innerText = "新的数据";
                <!-- 将jQuery对象转换为原生js对象     -->
                <!-- 注意: 不是eq(0),eq函数返回的是jQuery类型对象,get函数返回的是原生类型对象 -->
                var box = $box.get(0);
                var box = $box[0];
                box.innerText = "新的数据";

                var box2 = document.getElementById("box");
                <!-- 原生js对象不能使用jQuery对象的方法 -->
                box2.text("新的数据2");
                <!-- 原生js对象只能使用原生的js方法 -->
                box2.innerText = "新的数据2";

                <!-- 将原生js对象转换为jQuery对象 -->
                var $box2 = $(box);
                $box2.text("新的数据2");
            });
        </script>

    ```
3. jQuery(html,[ownerDoc]): 根据提供的原始HTML标记字符串,动态创建由jQuery对象包装的DOM元素.同时设置一系列的属性,事件等.你可以传递一个手写的HTML字符串,或者由某些模板引擎或插件创建的字符串,也可以是通过AJAX加载过来的字符串.但是在你创建input元素的时会有限制,可以参考第二个示例.当然这个字符串可以包含斜杠(比如一个图像地址),还有反斜杠.当你创建单个元素时,请使用闭合标签或XHTML格式.例如,创建一个span,可以用\$("<span/>")或\$("<span></span>"),但不推荐\$("<span>").在jQuery中,这个语法等同于\$(document.createElement("span")).在jQuery1.8中,通过$(html,props),您可以使用任何jQuery对象的方法或插件.在此之前，你只能使用一个方法名的短名单,并有没有成文的方式添加到列表中.现在并不需要是一个列表,在所有!然而,请注意,这可能会导致你的代码的行为改变,如果插件添加后,有相同的名称作为HTML属性.
``` js
    <script>
        // 动态创建一个div元素(以及其中的所有内容),并将它追加到body元素中.在这个函数的内部,是通过临时创建一个元素,并将这个元素的innerHTML属性设置为给定的标记字符串,来实现标记到DOM元素转换的.所以,这个函数既有灵活性,也有局限性.
        $("<div><p>Hello</p></div>").appendTo("body");
    </script>
```
``` js
    <script>
        // 创建一个<input>元素必须同时设定type属性.因为微软规定<input>元素的type只能写一次.
        // 在 IE 中无效:
        $("<input>").attr("type", "checkbox");
        // 在 IE 中有效:
        $("<input type='checkbox'>");
    </script>
```








## 参考
[从零玩转jQuery: https://www.jianshu.com/p/73c48795060b](https://www.jianshu.com/p/73c48795060b)