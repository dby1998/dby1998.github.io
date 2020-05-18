---
layout: post
title: "jQuer完整笔记"
date: 2020-05-18 
description: "HEXO配置，HEXO+Github，搭建自己的博客"

tag: 博客 
---   
## 一、JQuery简介

![1577156371204](assets/1577156371204.png)

jQuery是一款优秀的javaScript库（框架），该框架凭借简洁的语法和跨平台的兼容性，极大的简化了开发
人员对HTML文档，DOM事件以及Ajax的操作。

主旨口号：写的更少, 干的更多(以更少的代码,实现更多的功能)

官方网站： http://jquery.com/

中文API网站: <http://jquery.cuishifeng.cn/>

版本情况：

JQuery目前分成1.x版、2.x版和3.x版本，**从 2.0.0开始不再支持IE 6/7/8**，2.0.0版本之前通过jQuery Migrate plugin与先前版本保持兼容。 

作者：John Resig(约翰·雷西格)   于2006年1月的BarCamp NYC上发布第一个版本

![1577156258926](assets/1577156258926.png)

JQuery优点和特点(暂时先做了解)：

- 轻量级
- 免费开源
- 完善的文档
- 丰富的插件支持
- 完善的Ajax功能
- 不会污染顶级变量
- 强大的选择器功能
- 出色的DOM操作封装
- 出色的浏览器兼容性
- 可靠的事件处理机制
- 链式编程操作



总结为一句话：**JQuery是一个javascript功能库，提供了许多网页开发常见的功能供我们直接使用**。



## 二、体验JQuery

完成JQuery体验案例：

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 200px;
            height: 200px;
            background-color: pink;
            display: none;
        }
    </style>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
        $(function(){
            $("button:eq(0)").click(function(){
                $("div").show()
            })

            $("button:eq(1)").click(function(){
                $("div").hide()
            })
        })
    </script>
</head>
<body>
    <button>显示按钮</button>
    <button>隐藏按钮</button>
    <div></div>
</body>
```

## 三、JQ入口函数

JQ入口函数一般采用简写的方式，$(function(){   ...   })， 他也有完整的写法：

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        //js的入口函数
        window.onload = function(){
            //整个网页资源加载完毕再执行这里的代码
            console.log("1");
        };
        
        window.onload = function(){
            //整个网页资源加载完毕再执行这里的代码
            console.log("2");
        };
    </script>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
        $(function(){ // 简写
            //网页文档(标签)加载完毕，就执行这里的代码
            console.log("3");
        });
        $(document).ready(function(){
            //网页文档(标签)加载完毕，就执行这里的代码
            console.log("4");
        });
        $().ready(function(){
            //网页文档(标签)加载完毕，就执行这里的代码
            console.log("5");
        });
    </script>
</head>
<body>
    <div></div>
</body>
```

**两种加载模式的区别：**

1. 执行时机不同

   window.onload方法需要等所有的资源（CSS\JS\图片等）都加载完毕后再执行函数中的代码。
   jQuery框架的ready方法只等DOM文档加载完毕后立即执行包裹代码。

2. 执行次数不同

   window.onload方法，只会执行一次，后面的会把前面的覆盖

   jQuery框架的ready方法，有几次执行几次，不存在覆盖的问题。

3. jQuery存在多种简写方式

   完整的编写方式：$(document).ready(function(){})

   简写方式：

   ​	$().ready(function () {}）
   ​	$(function () {})

**总结书写JQ的步骤：**

1、引入JQ

2、书写入口函数

3、根据JQ的用谁选谁的原则，对元素进行控制



## 四、JQ操作css

jQuery框架提供了css方法，我们通过调用该方法传递对应的参数，可以方便的来批量设置标签的CSS样
式。

CSS( )--通过传递对应的参数，来实现不同的功能

1. $("selector").css(name,value);
2. $("selector").css(name1,value).css(name2,value)...;
3. $("selector").css( { name1 : value , name2 : value})

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
        $(function(){

            $("button:eq(0)").click(function(){
                console.log($("div").css('width'))
            });
            $("button:eq(1)").click(function(){
               $("div").css('width', 300).css('height', 400)
            });
            $("button:eq(2)").click(function(){
                $("div").css({
                    "width":"500px",
                    "height":"500px",
                    "background-color": "blue"
                });
                // 也可以用以下方式：
                // $("div").css({
                //     width:500,
                //     height:500,
                //     backgroundColor: "green"
                // })
            });
        })
    </script>
</head>
<body>
    <button>获取css属性值</button>
    <button>修改css属性</button>
    <button>同时修改多个css属性</button>
    <div></div>
</body>
```



## 五、JQ操作html

jQuery提供了直接控制html结构的相关方法，化简了我们操作html。

1. $("selector").html(value); 修改html
2. $("selector").html(); 访问html
3. $("selector").text(value); 修改文本内容
4. $("selector").text(); 访问文本内容

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 500px;
            height: 200px;
            border: 1px solid #000;
        }
    </style>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
        $(function(){

            $("button:eq(0)").click(function(){
                console.log($("div").html())
            });
            $("button:eq(1)").click(function(){
               $("div").html("<span>我们正在学习JQuery</span>")
            });
            $("button:eq(2)").click(function(){
                console.log($("div").text())
            });
            $("button:eq(3)").click(function(){
                $("div").text("我们正在学习JQuery....")
            });
        })
    </script>
</head>
<body>
    <button>获取内部html</button>
    <button>修改内部html</button>
    <button>获取内部纯文字文本</button>
    <button>修改内部纯文字文本</button>
    <div>
        <h1>JQuery介绍</h1>
        <p>jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（或JavaScript框架）。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。</p>
    </div>
</body>
```



## 六、JQuery选择器

jQuery 最核心的组成部分就是选择器引擎。它完全继承了 CSS 的风格,可以对 DOM 元 素的标签名、属性
名、状态等进行快速准确的选择，而且不必担心浏览器的兼容性，写法更加简洁。

jQuery 选择器实现了 CSS1~CSS3 的大部分规则之外,还实现了一些自定义的选择器,用于各种特殊状态的选
择。

优点：相对于直接使用 JavaScript 获取页面元素和处理业务逻辑相比，使用jQuery 选择器来进行操作代码
更简单，且拥有完善的代码检测机制 。

jQuery 选择器根据获取页面中元素的不同，可以划分为四大类 : **基本选择器、层级选择器、筛选选择器和表单选择器。**

#### 6.1、基本选择器

顾名思义，基本选择器是jQuery中用的最多， 使用最频繁的选择器，通过基本选择器我们可以实现大多数
页面元素的选择。基本选择器主要有： **ID选择器、类选择器、标签选择器、并集选择器和通配符选择器。**

| 选择器       | 语法       | 功能                               | 参考实例           |
| ------------ | ---------- | ---------------------------------- | ------------------ |
| ID选择器     | #id        | 根据给定的id匹配一个元素           | $("#divId")        |
| 类选择器     | .class     | 根据给定的class匹配所有的元素      | $(".classValue")   |
| 标签选择器   | element    | 根据给定的元素名匹配所有的元素     | $("elementName")   |
| 通配符选择器 | *          | 匹配所有的元素                     | $("*")             |
| 并集选择器   | #id,.class | 将每中选择器的结果合并在一起后返回 | $("#divId,.class") |

#### 6.2、层级选择器

层次选择器通过 DOM 元素间的层次关系获取元素，其主要的层次关系包括 **后代 、 直接后代 、 下一个相邻兄弟和后面所有兄弟元素**的关系，通过其中某类关系可以方便快捷地定位元素。

| 选择器         | 语法          | 功能                               | 参考实例      |
| -------------- | ------------- | ---------------------------------- | ------------- |
| 后代选择器     | parent child  | 根据祖先元素匹配所有的后代元素     | $("div p")    |
| 直接后代选择器 | parent>child  | 根据父元素匹配所有的子元素         | $("div>.box") |
| 下一个相邻兄弟 | prev+next     | 匹配所有紧接在prev元素后的相邻元素 | $("#div+p")   |
| 后面所有兄弟   | prev~siblings | 匹配prev元素之后的所有兄弟元素     | $("#div~p")   |

案例：

```html
<script>
		$(function(){
			$("button:eq(0)").click(function(){
				$("p").css('background', "pink")
			});
			$("button:eq(1)").click(function(){
				$(".left").css('background', "pink")
			});
			$("button:eq(2)").click(function(){
				$("#box").css('background', "pink")
			});
			$("button:eq(3)").click(function(){
				$("*").css('background', "pink")
			});
			$("button:eq(4)").click(function(){
				$("h1,h2,h3").css('background', "pink")
			});
			$("button:eq(5)").click(function(){
				$("ul li").css('background', "pink")
			});
			$("button:eq(6)").click(function(){
				$("body>*").css('border', "1px solid #000")
			});
			$("button:eq(7)").click(function(){
				$("p+div").css('background', "pink")
			});
			$("button:eq(8)").click(function(){
				$("p~div").css('background', "pink")
			});
		})
	</script>
... ...

<button>选择所有段落标签</button>
<button>选择class为left的标签</button>
<button>选择id为box的标签</button>
<button>选择所有不分类型标签</button>
<button>选择所有标题标签</button>
<button>选择ul里面的li标签</button>
<button>选择body下的第一级所有标签并添加边框</button>
<button>选择p后的一个div</button>
<button>选择p后的所有div</button>
```

备注：前两种选择器可以总结为，css里面可以怎么写，$(" ")里面就可以怎么写



**补充几个方法:**

在通过$(" ")选择到元素后，可以通过：

​	prev()    获取上一个相邻兄弟

​	prevAll()  获取 前面所有兄弟

​	next()   获取下一个相邻兄弟

​	nextAll()   获取后面所有兄弟



#### 6.3、基本筛选选择器

| 选择器语法     | 功能                                    |
| -------------- | --------------------------------------- |
| :first         | 获取第一个元素                          |
| :last          | 获取最后一个元素                        |
| :eq            | 获取指定索引值的元素                    |
| :gt(index)     | 获取大于给定索引值的元素                |
| :lt(index)     | 获取小于给定索引值的元素                |
| :not(selector) | 获取除给定选择器外的所有元素            |
| :header        | 获取所有标题类型的元素                  |
| :animated      | 获取正在执行动画效果的元素              |
| :even          | 获取所有索引值为偶数的元素，索引从0开始 |
| :odd           | 获取所有索引值为奇数的元素，索引从0开始 |

```html
<script>
		$(function(){
			$("button:eq(0)").click(function(){
				$("li:first").css('background', "pink")
			});
			$("button:eq(1)").click(function(){
				$("li:last").css('background', "pink")
			});
			$("button:eq(2)").click(function(){
				$("li:not(:last)").css('background', "pink")
			});
			$("button:eq(3)").click(function(){
				$("li:not(:eq(1))").css('background', "pink")
			});
			$("button:eq(4)").click(function(){
				$("li:even").css('background', "pink")
			});
			$("button:eq(5)").click(function(){
				$("li:odd").css('background', "pink")
			});
			$("button:eq(6)").click(function(){
				$("li:gt(4)").css('background', "pink")
			});
			$("button:eq(7)").click(function(){
				$("li:lt(4)").css('background', "pink")
			});
			$("button:eq(8)").click(function(){
				$("li:eq(4)").css('background', "pink")
			});
		})
	</script>

... ...
<button>选择第一个li</button>
<button>选择最后一个li</button>
<button>选择所有li排除最后一个</button>
<button>选择所有li排除第二个</button>
<button>选择所有索引值为偶数个li</button>
<button>选择所有索引值为奇数个li</button>
<button>选择大于第5个的li</button>
<button>选择小于第5个的li</button>
<button>选择等于第5个的li</button>
```



#### 6.4、内容筛选选择器

内容筛选选择器根据元素中的文字内容或所包含的子元素特征获取元素，其文字内容可以模糊或绝对匹配
进行元素定位。

| 选择器语法      | 功能                               |
| --------------- | ---------------------------------- |
| :contains(text) | 获取包含给定文本的元素             |
| :parent         | 获取含有子元素或者文本的元素       |
| :empty          | 获取所有不包含子元素或者文本的元素 |
| :has(selector)  | 获取含有选择器所匹配的元素         |

```html
<script>
        $(function(){
            $("button:eq(0)").click(function(){
                $("div:contains('天')").css('background', "pink")
            });
            $("button:eq(1)").click(function(){
                $("div:empty").css('background', "pink")
            });
            $("button:eq(2)").click(function(){
                $("div:parent").css('background', "pink")
            });
            $("button:eq(3)").click(function(){
                $("div:has('span')").css('background', "pink")
            });
        })
    </script>
   
...  ...
    <button>选择包含“天”字的div元素</button>
    <button>选择不包含子元素或文本的空元素</button>
    <button>选择含有子元素或者是文本的div元素</button>
    <button>选择含有span子标签的div</button>
```



#### 6.5、属性筛选选择器

属性过滤选择器 根据元素的某个属性获取元素，在使用的时候我们可以匹配单个属性也可以进行多个属性的匹配。

| 选择器语法         | 功能                                       |
| ------------------ | ------------------------------------------ |
| [属性名]           | 获取包含给定属性的元素                     |
| [属性名1][属性名2] | 获取满足多个条件的符合属性的元素           |
| [属性名='value']   | 获取包含给定属性且等于指定值的元素         |
| [属性名!=value]    | 获取包含给定属性且值不等于给定值的元素     |
| [属性名^=value]    | 获取包含给定属性且值以指定字符开头的元素   |
| [属性名$=value]    | 获取包含给定属性且值以指定字符结尾的元素   |
| [属性名*=value]    | 获取包含给定属性且包含指定字符或子串的元素 |

```html
<script>

$(function(){
    $("button:eq(0)").click(function(){
    	$("a[href]").css('background', "pink")
    });
    $("button:eq(1)").click(function(){
    	$("a[href='www.baidu.com']").css('background', "pink")
    });
    $("button:eq(2)").click(function(){
    	$("a[href^='www']").css('background', "pink")
    });
    $("button:eq(3)").click(function(){
    	$("a[href$='com']").css('background', "pink")
    });
    $("button:eq(4)").click(function(){
    	$("a[href*='wolf']").css('background', "pink")
    });
    $("button:eq(5)").click(function(){
    	$("a[href^='www'][title*='demo']").css('background', "pink")
    });
    $("button:eq(6)").click(function(){
    	$("input[type=text]").css('background', "pink")
    });

})
</script>
		
... ...
<button>获取所有拥有href属性的a标签</button>
<button>获取href属性值为www.baidu.com的a标签</button>
<button>获取href属性值以www开头的a标签</button>
<button>获取href属性值以com结尾的a标签</button>
<button>获取href属性值包含wolf的a标签</button>
<button>获取href属性值中以www开头且title中包含demo的a标签</button>
<button>获取type为text的表单元素</button>
```

#### 6.6、其它选择器(了解)

| 选择器语法 | 功能                                       |
| ---------- | ------------------------------------------ |
| :visible   | 获取所有可见的元素                         |
| :hidden    | 获取所有不可见元素，获取type为hidden的元素 |

| 选择器语法 | 功能                             |
| ---------- | -------------------------------- |
| :checked   | 获取表单中所有被选中的元素       |
| :selected  | 获取表单中所有被选中的option元素 |

| 选择器语法 | 功能                                    |
| ---------- | --------------------------------------- |
| :file      | 获取所有的文件上传元素                  |
| :image     | 获取所有的图片域                        |
| :text      | 获取所有的单行文本域                    |
| :reset     | 获取所有的重置按钮                      |
| :radio     | 获取所有的单选按钮                      |
| :button    | 获取所有的按钮                          |
| :submit    | 获取所有的提交按钮                      |
| :checkbox  | 获取所有的复选框                        |
| :password  | 获取所偶遇的密码框                      |
| :input     | 获取所偶遇的input、textarea、select元素 |

#### 6.7、父子兄选择器(重点)

parent() 获取当前标签的父节点
parents() 获取当前标签的祖先节点
parentsUntil() 获取当前标签的祖先节点直到… (不包含该标签)
children() 获取当前标签的子节点
siblings() 获取当前标签的兄弟节点

```html
	<script>
        $(function () {
            $("button").click(function () {
                // (1) 获取当前标签的父节点
                // $(".active").parent().css("border","1px solid #000");
                // (2) 获取当前标签的祖先节点 (可以指定就要body标签)
                // $(".active").parents("body").css("border","1px solid #000");
                //(3) 获取当前标签的祖先节点直到...(不包含指定的这个标签)
                $(".active").parentsUntil("body").css("border","1px solid #000");
            });
        })
    </script>
```

## 七、命名冲突的解决

```
今天我们一直在通过  $ 获取元素，如果  $ 已经作为其他变量在使用了，则可能发生命名冲突的问题，导致$ 不可用，可以通过以下方式解决：
```

```html
<script src="js/jquery-3.4.1.js"></script>
    <script>
        $(function(){

            //如果遇到$命名冲突，可以这么解决：
            jQuery("div").css("background", "green");

            //也可以通过以下方式解决:
            // var jq = $.noConflict();
            // jq("div").css("background", "pink");
            
        });

    </script>
```

## 八、JQuery对象和DOM对象的转换

```js
//  $("div")    通过JQuery选择器选出来的对象称为JQ对象
// 通过原生DOM方法 获取的标签称为原生DOM对象
// var odiv = document.getElementById("box");   //odiv为原生DOM对象


// 原生DOM对象不能直接调用JQ提供的方法
// 而JQ对象也不能直接使用原生js的属性和方法
// 都需要经过转换
```

```html
	<script>

        $(function(){

            // DOM对象转JQ对象
            var odiv = document.getElementById("box");
            console.log($(odiv));

            
            // JQ对象转DOM对象
            console.log($("div")[0]);    // 方式一
            console.log($("div").get(0));   // 方式二


        })
    </script>
```


## 九、显示隐藏动画切换

.show()

.hide()

.toggle()方法实现切换效果 (如果当前是显示，则切换为隐藏，如果当前为隐藏，则切换为显示)，同样可以传入数字表示动画时间

```js
	    $("button:eq(0)").click(function(){
            $("div").show();
        });
        $("button:eq(1)").click(function(){
            $("div").hide();
        });
        $("button:eq(2)").click(function(){
            $("div").toggle(400);
        });
```

## 十、滑动显示滑动隐藏动画

.slideDown()   向下滑动显示

.slideUp()  向上滑动隐藏

.slideToggle()   滑动切换

```js
 		$("button:eq(0)").click(function(){
            $("div").slideDown();
        });
        $("button:eq(1)").click(function(){
            $("div").slideUp();
        });
        $("button:eq(2)").click(function(){
            $("div").slideToggle();
        });
```

同样可以传入数字表示动画时间。

如果滑动的元素是图片，建议给width并且转块级元素。

## 十一、JQuery动画列队机制

如果用户对一个带有动画的元素频繁操作使到动画被触发，则用户的操作次数会被记录下来，用户每操作一次，都会多执行一次动画效果，直到所有次数的动画被执行完毕。这是JQ的动画列队机制。

如果希望用户停止操作后就立刻停止动画，可以在动画函数前面提前调用stop() 方法

```js
$(".nav>ul>li").mouseenter(function(){
	$(this).children("ul").stop().slideDown();
}).mouseleave(function(){
	$(this).children("ul").stop().slideUp();
})
```

## 十二、hover() 事件

hover(鼠标移上函数，鼠标离开函数)

如果两个函数代码一模一样，则可以只写一个函数

```js
$(".nav>ul>li").hover(function(){
     $(this).children("ul").stop().slideToggle();
},function(){
     $(this).children("ul").stop().slideToggle();
})

//上面代码可以简化为：
$(".nav>ul>li").hover(function(){
     $(this).children("ul").stop().slideToggle();
})
```

## 十三、index()获取元素的索引值

jq中给每个元素编号，这个编号从0开始，我们称为这个元素的索引值。

我们通过选中元素后， .index() 方法来获取到这个索引值。

```html
<script>
    $(function(){
       $("li,p").click(function(){
           alert($(this).index())
       })
    })
</script>
```

注意：**索引值表示的是这个元素在同级标签中的排行的索引值，跟它自己本身是什么标签无关**

## 十四、类的控制

**addClass() 添加类名**

**removeClass() 删除类名**

**toggleClass() 切换类名**

```html
<script>
    $(function(){
        $("button:eq(0)").click(function(){
            $("div").addClass("box box2");
        });
        $("button:eq(1)").click(function(){
            $("div").removeClass("box");
        });
        $("button:eq(2)").click(function(){
            $("div").toggleClass("box");
        });
    })
</script>
```

注意：

addClass() 可以一次性添加多个类名，类名间用空格隔开

removeClass() 如果没有指定删除的类名称，则删除所有类名

## 十五、淡入淡出动画(透明度动画)

fadeIn()   淡入动画，即改变标签的透明度让标签慢慢的显示出来。

fadeOut()   淡出动画，即改变标签的透明度让标签慢慢的消失（透明度为0）。

fadeToggle()  透明度切换动画，如果当前标签的透明度不为0，那么就执行淡出动画，否则就执行淡入动画。

fadeTo(动画时间，透明值)  透明到指定值。

备注 ：标签透明度的取值范围为0.0~1.0。

```js
		$("button:eq(0)").click(function(){
            $("div").fadeIn();
        });
        $("button:eq(1)").click(function(){
            $("div").fadeOut();
        });
        $("button:eq(2)").click(function(){
            $("div").fadeToggle();
        });
        $("button:eq(3)").click(function(){
            $("div").fadeTo(1000, .5);
        });
        $("button:eq(4)").click(function(){
            $("div").fadeTo(1000, 1);
        });
```

## 十六、JQ的自定义动画

jQuery框架中本身已经为我们封装好了一些简单的控制标签宽高、透明度相关的方法，如显示和隐藏、展开和收起、淡入和淡出，除了这些方法之外，jQuery还为我们提供了animate（）方法 ，允许我们自定义动画效果，通过一些设置我们可以实现更加复杂的动画效果，

**自定义动画的语法**
	animate(params,speed,easing,callBack)

**参数说明：**

第一个参数：

​	params是一个对象。在该对象中以键值对的方式来要控制的属性样式和对应的值表示。

第二个参数：

​	speed速度，可以是默认字符串中的某个（“slow” “normal” “fast”）或者是自定义的数字。

第三个参数：easing为动画插件使用的可选参数，用来控制动画的表现效果，通常有linear和swing等固定值。

第四个参数：动画执行完毕后的回调函数。

```js
			$("button").click(function () {
                $("div").animate({
                    width:400,  //width:"+=200"  或者：  "toggle" 在0和值之间做切换
                    height:400,
                    fontSize:100,
                    opacity:0.5,
                    marginLeft:200,
                    borderRadius:50,
                    "margin-top":"200px"
                },2000,'linear',function () {
                    alert("盒子变大了!")
                })
            });
```

注意：**animate动画只能实现属性值是数字的动画效果**

备注：JQuery所提供的其他动画函数也有这后面三个参数，例如：

```
$("div").show(1000,"linear",function(){
    alert("动画执行结束了")
});
```

## 十七、delay()让动画延迟执行

delay() 方法可以让即将执行的动画延迟一段时间之后再执行，传入数字表示延迟时间

```js
$(".ad").slideDown().delay(2000).slideUp();
//表示两秒钟之后再执行.slideUp()函数
```

## 十八、绑定事件两种方式

在jQuery中，我们可以有多种方式来为标签绑定事件，可以简单的区分为 **专用方法绑定事件 和 快捷方法 绑**
**定事件。**

#### 1.1、快捷方法

格式：  选择元素.事件类型()

```js
$(".box").click(function(){
     alert(123);
});
```



#### 1.2、专用方法绑定事件(on方法)

格式：  .on("事件名称",事件参数对象, 事件函数)

```js
$(".box").on("click", {name:"JQuery"}, function(e){
     alert(e.data.name);
});
```



jQuery中可以使用四种专用方法来绑定事件，分别是 **bind方法、live方法、delegate方法和on方法** ,每个版本各有区别，建议使用on方法。

补充说明：

​	bind方法适用于所有的版本，1.7+ 推荐使用on方法来代替。
​	live方法适用于 1.9- 的版本，1.9+ 版本使用on方法来代替。
​	delegate方法适用于1.4.2 + 的版本。
​	on方法适用于1.7+ 的版本，1.7+ 用于替代bind和live方法。

on方法为指定的元素添加一个或者是多个事件，并规定这些事件发生时指定的函数。
on方法的语法： on（eventType,childselector,data,function）

参数说明：
	eventType：必传参数，指定事件的类型如click等。
	childselector：可选参数，用于事件委托。
	data：可选参数，设计需要传递的数据。
	function：必传参数，事件发生时，执行的函数。

#### 1.3、扩展资料

【快捷方法绑定事件】

jQuery框架中定义了多个快捷方法来为标签绑定特定类型的事件，这些方法和二级事件模型中的事件类型
对应，名称相同。
具体的快捷方法如下：
**blur() 当元素失去焦点时发生 blur 事件**
**change() 当元素的值发生改变时，会发生 change 事件**
**click() 当点击元素时，会发生 click 事件**
dbclick() 当双击元素时，会发生 dblclick 事件
**focus() 当元素获得焦点时，发生 focus 事件**
keydown() 当按键被按下时，发生 keydown 事件
keyup() 当按键被松开时，发生 keyup 事件
keypress() 当按键被按下时，发生 keypress事件（响应每个字符）
**mouseenter()当鼠标指针穿过元素时，会发生 mouseenter 事件**
**mouseleave()当鼠标指针离开元素时，会发生 mouseleave 事件**
mouseover() 当鼠标指针位于元素上方时，会发生 mouseover 事件
mouseout() 当鼠标指针从元素上移开时，会发生 mouseout 事件
mousedown() 当鼠标进入元素，并按下按键时，会发生mousedown事件

mouseup() 当在元素上放松鼠标按钮时，会发生 mouseup 事件
mousemove() 当鼠标在指定的元素中移动时，会发生 mousemove 事件
**scroll() 当用户滚动指定的元素时，会发生 scroll 事件**
submit() 当提交表单时，会发生 submit 事件(表单)


【one方法的使用】
one方法 是on方法中的一种特殊使用方式，由one方法绑定的事件在执行一次响应之后就会失效。其设计思路是：在事件处理函数的内部注销当前事件

```js
//事件只执行1次就失效
$(".box").one("click", {name:"JQuery"}, function(e){
    alert(e.data.name);
});
```

【事件委托说明】
事件委托是开发中常见的绑定事件方式，参考代码如下。

```js
//事件委托格式：
$("body").on("click",".box", {name:"JQuery"}, function(e){
    alert("事件委托格式");
    alert(e.data.name);
});
```

## 十九、注销事件

有时候我们需要把一些元素的绑定事件注销，可以使用off方法来注销事件。

off方法 的使用示例

```js
$(".box").on("click", {name:"JQuery"}, function(e){
    alert(e.data.name);
    $(this).off("click");
});

// 或者直接：
$(".box").off("click");
```

## 二十、事件对象

在注册事件的时候，event对象实例将作为第一个参数传递给事件的回调函数，这和DOM事件模型是完全相
同的。另外，jQuery统一了IE事件模型和DOM事件模型中event对象属性和方法的用法，使其符合DOM标准
事件模型的规范。

| 属性名                          | 描述                                             |
| ------------------------------- | ------------------------------------------------ |
| type                            | 获取这个事件的事件类型，例如：click              |
| target                          | 获取绑定事件的DOM元素                            |
| data                            | 获取事件调用时的额外数据                         |
| relatedTarget                   | 获取移入移出目标点离开或进入的那个DOM元素        |
| currentTarget                   | 获取冒泡前触发的DOM元素，等同于this              |
| pageX/pageY                     | 获取相对于页面原点的水平/垂直坐标                |
| screenX/screenY                 | 获取显示器屏幕位置的水平/垂直坐标（非jQuery)封装 |
| clientX/clientY                 | 获取相对页面视口的水平/垂直坐标(非jQuery封装)    |
| result                          | 获取上一个相同事件的返回值                       |
| timeStamp                       | 获取事件触发的时间戳                             |
| which                           | 获取鼠标的左中右键（1,2,3），或获取键盘按键      |
| altKey/shiftKey/ctrlKey/metaKey | 获取是否按下了alt、shift、ctrl或meta键           |
| e.preventDefault();             | 防止键盘回车焦点事件                             |

在事件处理函数（回调函数）中，我们可以获取事件对象的相关信息。

```js
$("div").on("click",{name:"JQuery"},function (e) {
	console.log("点击了div");
	//获取事件的类型
	console.log(e.type);
	//获取目标对象
	console.log(e.target);
	//获取被省略的对象
	console.log(e.data);
})
```

## 二十一、阻止事件冒泡

事件冒泡的简单解释：如果某个标签的事件被触发，那么该标签父标签上被注册的相同类型事件也会被触发，并且会依次一直冒泡到顶端。

阻止事件冒泡的两种方式：
【1】在回调函数中返回false       return false
【2】调用事件对象的stopPropagation    e.stopPropagation();

```html
	<div class="big">
        大
        <div class="small">
            小
        </div>
    </div>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
    $(function(){
        $(".big").on("click",function(){
            alert("点击了大盒子");
        });
        $(".small").on("click",function(e){
            alert("点击了小盒子");
            // 阻止事件冒泡
            // e.stopPropagation();
            // return false
        });
    })
    </script>
```

## 二十二、阻止标签默认行为

**默认行为**
	默认行为 ：页面中的一些标签常常存在默认的行为，比如表单的submit事件类型，如果该类型的事件被触发，则会导致表单的提交；比如a标签存在跳转网页连接的默认行为等。

如果需要在事件被触发的时候，阻止标签默认的行为，可以通过以下两种方式：

【1】在回调函数中返回false       return false
【2】调用事件对象的preventDefault    e.preventDefault();

```html
<a href="http://www.baidu.com">百度一下</a>

... ...
<script>
$("a").on("click",function(e){
    // 阻止默认行为
    // e.preventDefault();
    return false
})
</script>
```

## 二十三、自定义事件(了解)

我们可以给标签添加自定义事件，但是自定义事件需要.trigger()方法触发才能执行：

例如：给div自定义一个"shitihua"事件

```html
	<div></div>
    <script src="js/jquery-3.4.1.js"></script>
    <script>
    $(function(){
        // 自定义事件
        $("div").on("shitihua",function(){
           $(this).css({
               width:200,
               height:200,
               background:"#ccc"
           })
        });
        
        // 触发事件
        $("div").trigger("shitihua");
    })
    </script>
```

## 二十四、鼠标跟随效果

```js
$(document).on("mousemove", function(e){
    //鼠标在网页上移动的时候，执行这里的代码
    //e.pageX为鼠标所在位置相对于网页文档左上角的水平距离
    //e.pageY为鼠标所在位置相对于网页文档左上角的竖直距离
    console.log(e.pageX, e.pageY);  
});

```

让图片跟随鼠标

```html
<style>
    img{
        position: absolute;
    }
</style>
... ...
<img src="images/dian.gif" height="192" width="390"/></body>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){

   $(document).on("mousemove", function(e){
       //鼠标在网页上移动的时候，执行这里的代码
       //e.pageX为鼠标所在位置相对于网页文档左上角的水平距离
       //e.pageY为鼠标所在位置相对于网页文档左上角的竖直距离
       // console.log(e.pageX, e.pageY);

       $("img").css({
           left: e.pageX,
           top: e.pageY,
       })
   });
})
</script>
```



## 二十五、JQ控制标签属性

JQ中通过attr() 方法控制标签属性，**使用方式和.css()方法完全一致**

格式：

**$(selector).attr(name);**   传一个字符串参数表示访问指定属性的值

**$(selector).attr(name, "value");**   传两个参数表示修改指定属性的值

**$(selector).attr({**

​		**name:"value",**

​		**name:"value",**

​		**……**

**});**    传一个对象参数表示多属性修改

备注： 

JQ中还提供了prop()方法，也可以操作标签属性，使用方式和.attr()一致，但是只能操作原生标签属性

而attr()方法可以操作原生标签属性，和自定义标签属性

```html
<button>获取标签属性</button>
<button>修改标签属性</button>
<button>同时修改多个标签属性</button>
<br><br>
<img src="images/dian.gif" height="192" width="390" class="img01" title="这是一张图片" data-mypro="123456"/>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){
    $("button").eq(0).click(function(){
        console.log($("img").attr("class"))
    });

    $("button").eq(1).click(function(){
        $("img").attr("title","这是修改过的值")
    });

    $("button").eq(2).click(function(){
        $("img").attr({
            "class":"img02",
            "title":"这是修改过的值2222"
        })
    });
    //attr可以获取自定义标签属性
    console.log($("img").attr("data-mypro"));  // 123456
    //prop只能获取原生标签属性
    console.log($("img").prop("title"));  //  这是一张图片
    console.log($("img").prop("data-mypro"));  //undefined

})
</script>
```



## 二十六、键盘事件

事件对象**e.keyCode**可以获取对应按键的键码



## 二十七、视频/音频API

W3C为原生dom对象视频/音频提供了大量属性和方法，参考链接：

http://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp

**方法：**

play()   播放

**属性：**

currentTime    设置/返回当前时间

## 二十八、网页文档坐标和窗口滚动距离

获取一个元素的网页文档坐标值： 

**$().offset().top     获取元素距离网页文档最顶部的距离**（元素的Y坐标）

**$().offset().left     获取元素距离网页文档最左边的距离**（元素的X坐标）

当窗口发生滚动事件的时候，可以获取网页超出浏览器窗口的距离：**$(window).scrollTop()**

吸顶导航案例：

```html
<script>
$(function(){
    // 获取盒子的Y坐标
    var box_ostop = $(".box").offset().top;
    $(window).scroll(function(){

        // 每当滚动的时候都需要获取超出窗口的范围  然后和盒子Y坐标做对比
        // 如果滚动距离大于等于盒子Y坐标，就设置成固定定位，否则去掉盒子定位
        var win_st = $(window).scrollTop();  
        if(win_st>=box_ostop){
            $(".box").css({
                "position":"fixed",
                top:0
            })
        }else{
            $(".box").css({
                "position":""
            })
        }
    });
})
</script>
```

## 二十九、each遍历

我们可以使用JQ提供的.each()方法来**遍历标签**

.each有两种格式的写法：

**格式一**：

```js
$("p").each(function(i, el){
    //遍历p标签，每遍历一个p标签，就会执行一遍函数里面的代码
 	//i是p标签的索引值，el是正在遍历的这个p标签(DOM对象)       
})
```

**格式二**：

```js
$.each($("p"),function(i, el){
    //遍历p标签，每遍历一个p标签，就会执行一遍函数里面的代码
	//i是p标签的索引值，el是正在遍历的这个p标签(DOM对象)
	console.log($(el).text());
})
```

注意：

**格式二这种写法还可以直接遍历数组或者对象**。例如：

```js
var arr = [10, 20, 30];
$.each(arr ,function(i, el){
	//i是元素在数组中的索引值，el是正在遍历的这个数组中的元素
	console.log(i, el);
})；

var obj = {
    name:"javascript",
    age:24,
    job:"web"
};
$.each(obj ,function(key, val){
    //i是键，el键所对应的值
    console.log(key, val);
})
```

## 三十、map遍历

.map()也可以用来遍历标签，而且**最终会返回一个数组**。

可以通过在函数内部写返回值，这些返回值最终成为数组的每一个元素。

```js
var arr1 = $("p").map(function(i, el){
    //i是p标签的索引值，el是正在遍历的这个p标签(DOM对象)
    console.log($(el).text());

    return $(el).text()    //这里书写的返回值，就是将来数组中的元素
});

console.log(arr1);
```



## 三十一、让页面滚动到指定位置(兼容写法)

```js
$("html,body").stop(true).animate({scrollTop:指定位置});

//$("html,body")——html和body兼容不同浏览器的写法
//scrollTop——jQuery封装的网页滚动坐标的属性
```



## 三十二、增加节点

在页面中增加节点的步骤：

1、准备节点

2、找到要插入节点的位置，添加刚才准备好的节点

```html
<body>
    <button>按钮</button>
    <ul>

    </ul>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){

    $("button").click(function(){

        // 1、准备节点
        var oli = $("<li>文字</li>");
        // 2、找到要插入节点的位置，添加刚才准备好的节点
        // $("ul").append(oli);   //  在ul最后追加oli节点
        // $("ul").prepend(oli);   //  在ul最开始追加oli节点

        // oli.appendTo($("ul"))   //  把oli节点追加到ul最后
        oli.prependTo($("ul"))   //  把oli节点追加到ul开始
    })
})
</script>

```

插入节点的方法：

$("ul").**append**(oli);   //  在ul最后追加oli节点

$("ul").**prepend**(oli);   //  在ul最开始追加oli节点

oli.**appendTo**($("ul"))   //  把oli节点追加到ul最后

oli.**prependTo**($("ul"))   //  把oli节点追加到ul开始

## 三十三、删除节点

jQuery框架中定义了3个删除内容的方法：它们分别是**remove（）、empty（）和detach（）**。

$().remove()   删除指定节点

$().empty()   保留选中的这个节点，清空内部内容，包括标签上的事件也清除

$().detach()   删除指定节点，但是不清除事件

```html
<button>点击删除</button>
<button>点击增加</button>
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
</ul>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){
    var lis = $("li");

    $("li").click(function () {
        alert($(this).index())
    });
    $("button:eq(0)").click(function () {
        // $("ul").remove();  // 删除指定节点

        // $("ul").empty();  //保留选中的这个节点，清空内部内容，包括标签上的事件也清除

        $("li").detach(); //删除指定节点，保留节点事件
    });


    $("button:eq(1)").click(function () {

        $("ul").append(lis);
    });
})
</script>
```

## 三十四、复制节点

复制节点的步骤：

1、复制出节点

var oli = $("要复制的节点").**clone**(true);    //复制的时候带参数true，表示事件也一起复制，默认没传参不复制事件

2、插入到指定位置

$("ul").append(oli);

```html
<button>复制节点</button>
<ul>
    <li>这是li</li>
</ul>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){

    $("li").click(function () {
        alert($(this).index())
    });
    $("button").click(function () {
       var oli = $("li:first").clone(true);   // 复制的时候带参数true，表示事件也一起复制，默认没传参不复制事件
       $("ul").append(oli);
    })
})
</script>
```

## 三十五、替换节点

替换节点的步骤：

1、准备要替换成的节点

var op = $("<p>替换成p2</p>");

2、进行替换

选中要被替换元素**.replaceWith**(准备好的节点)       或者：

准备好的节点**.replaceAll**(选中要被替换元素)

```html
<button>点击替换</button>

<div>盒子</div>
<div>盒子</div>
<script src="js/jquery-3.4.1.js"></script>
<script>
$(function(){
   $("button").click(function(){
       // 准备要替换成的节点
       var op = $("<p>替换成p2</p>");
       
       // 把div替换成准备好的op节点
       // $("div").replaceWith(op);   
       op.replaceAll($("div"));
   })
})
</script>
```









  



