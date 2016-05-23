?:$(myForm.elements).hide()
// 在 IE 中无效:
$("<input>").attr("type", "checkbox");
// 在 IE 中有效:
$("<input type='checkbox'>");

?   $("<div>", {
  "class": "test",
  text: "Click me!",
  click: function(){
    $(this).toggleClass("test");
  }
    }).appendTo("body");

?   $("<input>", {
  type: "text",
  val: "Test",
  focusin: function() {
    $(this).addClass("active");
  },
  focusout: function() {
    $(this).removeClass("active");
  }
}).appendTo(document.forms);

?:index([selector|element])
<ul>
  <li id="foo">foo</li>
  <li id="bar">bar</li>
  <li id="baz">baz</li>
</ul>

$('li').index(document.getElementById('bar')); //1，传递一个DOM对象，返回这个对象在原先集合中的索引位置
$('li').index($('#bar')); //1，传递一个jQuery对象
$('li').index($('li:gt(0)')); //1，传递一组jQuery对象，返回这个对象中第一个元素在原先集合中的索引位置
$('#bar').index('li'); //1，传递一个选择器，返回#bar在所有li中的做引位置
$('#bar').index(); //1，不传递参数，返回这个元素在同辈中的索引位置。 

?:data([key],[value])
如果jQuery集合指向多个元素，那将在所有元素上设置对应数据。 这个函数不用建立一个新的expando，就能在一个元素上存放任何格式的数据，而不仅仅是字符串。
NEW data(obj) 可传入key-value形式的数据。

    // $('em').data("blabla");
    $("em").data("blabla","haha");
    alert($("em").data("blabla"));
    $("em").data("blabla",66);
    alert($("em").data("blabla"));
    $("em").removeData("blabla");
    alert($("em").data("blabla"));
    $("em").data("array",{'a':'a','b':'b','c':"c"});
    alert($("em").data("array"));
    alert($("em").data("array").a);
    alert($("em").data("array").b);

removeData([name|list])
在元素上移除存放的数据,与$(...).data(name, value)函数作用相反
alert($("em").removeData("array").b);
alert($("em").data("array").b);

jQuery.data(element,[key],[value])
在元素上存放数据,返回jQuery对象。
注意：这是一个底层方法。你应当使用.data()来代替。
jQuery.data(document.body,"foo","heihei");
    alert($(document.body).data('foo'));

queue(element,[queueName]),返回值:Array/jQuery
    $("#show").click(function(){
        var n=$("code").queue("fx");
        $("i").text("queue length is:"+n.length);   
    });
    function runit(){
        $("code").show("slow");
        $("code").animate({left:"+=200"},2000);
        $("code").slideToggle(1000);
        $("code").slideToggle("fast");
        $("code").animate({left:"-=200"},1500);
        $("code").hide("slow");
        $("code").show(1200);
        $("code").slideUp("normal",runit);
    }
    runit();

参数：element,queueName,newQueue 
newQueue:替换当前函数列队内容的数组
通过设定队列数组来删除动画队列



$("#stop").click(function () {
      $("div").queue("fx", []);
      $("div").stop();
});

插入一个自定义函数 如果函数执行后要继续队列，则执行 jQuery(this).dequeue();
$(document.body).click(function () {
      $("div").show("slow");
      $("div").animate({left:'+=200'},2000);
      $("div").queue(function () {
          $(this).addClass("newcolor");
          $(this).dequeue();
      });
      $("div").animate({left:'-=200'},500);
      $("div").queue(function () {
          $(this).removeClass("newcolor");
          $(this).dequeue();
      });
      $("div").slideUp();
});


dequeue([queueName])，返回值:jQuery,队列名，默认为fx
从队列最前端移除一个队列函数，并执行他。
使用 dequeue() 终止一个自定义的队列函数
$("div").queue(function(){
        $(this).toggleClass("red");
        $(this).dequeue();
    });

用dequeue来结束自定义队列函数，并让队列继续进行下去。
$("button").click(function () {
      $("div").animate({left:'+=200px'}, 2000);
      $("div").animate({top:'0px'}, 600);
      $("div").queue(function () {
          $(this).toggleClass("red");
          $(this).dequeue();
      });
      $("div").animate({left:'10px', top:'30px'}, 700);
  });


  clearQueue([queueName]),返回值:jQuery
清空对象上尚未执行的所有队列,如果不带参数，则默认清空的是动画队列。这跟stop(true)类似，但stop()只能清空动画队列，而这个可以清空所有通过 .queue() 创建的队列。
queueName:含有队列名的字符串。默认是"Fx"，动画队列。
停止当前正在运行的动画：
$("#stop").click(function(){
  $("#box").clearQueue();
});

返回值:jQueryjQuery.noConflict([extreme])
运行这个函数将变量$的控制权让渡给第一个实现它的那个库。

#选择器
$("*")找到每一个元素，多用于上下文搜索
$("div,span,p.myClass")找打每一个匹配的元素合并到一个结果内
$("div p")
$("div > p")
$("prevp + p")选择同辈元素的紧挨着下一个选择器，且该选择器必须是p
$("prevp ~ p")选择知之后同辈指定元素的所有选择器，上面的是一个，这里是所有
$("li:first")在指定区域(这里为li)搜索第一个，搜索到即停止搜索
$("ol li:first")指定区域(这里为ul li)
$("li:last")在指定区域搜索最后一个，搜索到即停止搜索，相当于在区域从后向前搜索
$("ol li:last")指定区域(这里为ol li)
？？：$("input:not(:text)")//不明白时尽量少用
$("li:even")
$("li:odd")
$("li:eq(5)")
$("li:lt(3)")不包括3
$("li:gt(7)")不包括7
$(":header")匹配所有h1-h6元素
$("span:animated")匹配所有正在执行动画的元素
$("span:not(:animated)")
？？？$("div:focus");
$("div:contains('John')")
:empty 匹配所有不包含子元素或者文本的空元素
$("div:empty")
$("div:has('p')")    $("div:has('.p')")
:parent 匹配含有子元素或者文本的元素
$("div:parent"),匹配的是div
:hidden 匹配所有不可见元素，或者type为hidden的元素
$(":hidden").css("display","block");
:visible 匹配所有的可见元素
===========================
[attribute] 匹配包含给定属性的元素
$("span[id]") id不要加引号

[attribute=value]
匹配给定的属性是某个特定值的元素
$("input[type=text]") 或者属性值加引号$("input[type='text']")

[attribute!=value]
匹配所有不含有指定的属性和有指定属性但属性值不等于特定值的元素
$("div[id!='hello']") 匹配所有不包含id属性且有该属性但值不等于hello的div
$("div[id!='hellow']")

[attribute^=value]
匹配给定的属性是以某些值开始的元素
$("div[id^='he']") 匹配到id=hello的div

[attribute$=value]
匹配给定的属性是以某些值结尾的元素

[attribute*=value]
匹配给定的属性是以包含某些值的元素
$("div[id*='ll']")

[selector1][selector2][selectorN]
复合属性选择器，需要同时满足多个条件时使用。
$("div[id*='ll'][class]")

:nth-child
匹配其父元素下的第N个子或奇偶元素
:eq(index)只匹配一个元素，而这个将为每一个父元素匹配子元素。
:nth-child从1开始的，而:eq()是从0算起的！
可以使用:
    :nth-child(even)
    :nth-child(odd)
    :nth-child(3n)
    :nth-child(n)
    :nth-child(3n+1)
    :nth-child(3n+2)

$("div dd:nth-child(2n+1)")
$("div dd:nth-child(even)")
$("div dd:nth-child(3n+2)")
$("div dd:nth-child(5n+2)")

:first-child
匹配第一个子元素
':first' 只匹配一个元素，而此选择符将为每个父元素匹配一个子元素
$("ul li:first-child")匹配每一ul下的第一个li

:last-child
匹配最后一个子元素
':last'只匹配一个元素，而此选择符将为每个父元素匹配一个子元素
$("ul li:last-child") 匹配到每一个ul下的最后一个子元素

:only-child
如果某个元素是父元素中唯一的子元素，那将会被匹配，如果父元素中含有其他元素，那将不会被匹配。
$("div p:only-child")
==================================
:input
匹配所有 input, textarea, select 和 button 元素
$("span :input") 这个的冒号和前边一定要有空格

:text
匹配所有的单行文本框即input

:password
匹配所有密码框

:radio
匹配所有单选按钮

:checkbox
匹配所有复选框

:submit
匹配所有提交按钮

:image
匹配所有图像域

:reset
匹配所有重置按钮

:button
匹配所有按钮

:file
匹配所有文件域

:enabled
匹配所有可用元素

:disabled
匹配所有不可用元素

:checked
匹配所有选中的被选中元素(复选框、单选框等，不包括select中的option)

:selected
匹配所有选中的option元素
=========================================
#属性
attr(name|properties|key,value|fn) 返回值:String
设置或返回被选元素的属性值。
$('img').attr('src')返回所有img的src属性，默认仅返回第一个值但选中了所有
$("img").attr({'src':"test1.jpg",'title':'test'});
$("img").attr("src","test2.jpg");
$("img").attr("title", function() { return this.src });
$("img").attr("title",function(){
        return $(this).attr("src");
    });

removeAttr(name)
从每一个匹配的元素中删除一个属性
$("img").removeAttr("src");

prop(name|properties|key,value|fn)
获取在匹配的元素集中的第一个元素的属性值。
$('img').prop('src')
$("input[type='checkbox']").prop("disabled","true");
$("input[type='checkbox']").prop({"disabled":"true"});

$("input[type='checkbox']").prop({"disabled":"false"});
$("input[type='checkbox']").prop("checked", true);

$("input[type='checkbox']").prop("checked", function( i, val ) {
  return 1;
});

removeProp(name)
用来删除由.prop()方法设置的属性集
$("input[type='checkbox']").removeProp("checked");

addClass(class|fn)
为每个匹配的元素添加指定的类名,一个或多个空格分隔。
函数必须返回一个或多个空格分隔的class名。接受两个参数，index参数为对象在这个集合中的索引值，class参数为这个对象原先的class属性值。
$("ul li:last").addClass("c1 c2");

$("ul li:last").addClass(function(){
        return "c3 c4";
    });

removeClass([class|fn])
从所有匹配的元素中删除全部或者指定的类。
$("ul li:last").removeClass("c3");

toggleClass(class|fn[,sw])
如果存在（不存在）就删除（添加）一个类。
class:要切换的CSS类名. 
sw:用于决定元素是否包含class的布尔值,默认一次一切换

var count=0;
    $("p").click(function(){
        $(this).toggleClass("c1",count++%3==0);
    });

$('div.foo').toggleClass(function() {
  if ($(this).parent().is('.bar') {
    return 'happy';
  } else {
    return 'sad';
  }
});

html([val|fn])
取得第一个匹配元素的html内容。这个函数不能用于XML文档。但可以用于XHTML文档。
在一个 HTML 文档中, 我们可以使用 .html() 方法来获取任意一个元素的内容。 如果选择器匹配多于一个的元素，那么只有第一个匹配元素的 HTML 内容会被获取。
    $("ul").html("<hr/><br/>hhahahh");改写里面的所有内容

  $("ul").html(function(m){
        return "这个ul元素的index是"+m;
});

text([val|fn]);返回值:String
取得所有匹配元素的内容。
结果是由所有匹配元素包含的文本内容组合起来的文本。这个方法对HTML和XML文档都有效。
alert($("p").text());//返回所匹配元素的文本组成的文本集合,不包含标签
$("p").text("haha");//设置所匹配元素的文本，包含的标签

$("p").text(function(n){
    return "这个 p 元素的 index 是：" + n;
    });


val([val|fn|arr])
获得匹配元素的当前值。,元素应该具有value属性
在 jQuery 1.2中,可以返回任意元素的值了。包括select。如果多选，将返回一个数组，其包含所选的值
$("input").val();//设定文本框的值
$("input").val("hello world!");//设定文本框的值
$('input:text.items').val(function() {
  return this.value + ' ' + this.className;
});

#文档处理
append(content|fn)
向每个匹配的元素内部追加内容。
这个操作与对指定的元素执行appendChild方法，将它们添加到文档中的情况类似。
$(document.body).append("<span>hahah</span>");
$("div").append("<strong>强调</strong>");
$("div").append(function(){
        return "hahaa";
});

appendTo(content)
把所有匹配的元素追加到另一个指定的元素元素集合中。
实际上，使用这个方法是颠倒了常规的$(A).append(B)的操作，即不是把B追加到A中，而是把A追加到B中。
$("p").appendTo(".div");
$("p").appendTo($(".div"));
$("<p>这也行</p>").appendTo($("div:not('.div')"));

prepend(content)
向每个匹配的元素内部前置内容。这是向所有匹配元素内部的开始处插入内容的最佳方式。
$("p").prepend("div");
$("div").prepend("<em>加载前边</em>");

prependTo(content)
把所有匹配的元素前置到另一个、指定的元素元素集合中。
实际上，使用这个方法是颠倒了常规的$(A).prepend(B)的操作，即不是把B前置到A中，而是把A前置到B中。
$("span").prependTo($(".dd"));
$("p").prependTo("#foo");


返回值:jQueryafter(content|fn)
在每个匹配的元素之后插入内容。
$("span").after("<i>加到span</i>");
$("span").after($("em"));

before(content|fn)
在每个匹配的元素之前插入内容。


insertAfter(content)
把所有匹配的元素插入到另一个、指定的元素元素集合的后面。
实际上，使用这个方法是颠倒了常规的$(A).after(B)的操作，即不是把B插入到A后面，而是把A插入到B后面。

 
insertBefore(content) 返回值:jQuery
把所有匹配的元素插入到另一个、指定的元素元素集合的前面。
实际上，使用这个方法是颠倒了常规的$(A).before(B)的操作，即不是把B插入到A前面，而是把A插入到B前面
$("p").wrap("<div class='c1'></div>");
$("p").wrap(document.getElementById("content"));//原来的content并没有变化，而是生成了新的id为content的包裹层
$('.inner').wrap(function() {
  return '<div class="' + $(this).text() + '" />';
});

unwrap()
这个方法将移出元素的父元素。这能快速取消 .wrap()方法的效果。匹配的元素（以及他们的同辈元素）会在DOM结构上替换他们的父元素。
$("p").unwrap();

？？？wrapAll(html|ele)


wrapInner(htm|ele|fnl) 返回值:jQuery
将每一个匹配的元素的子内容(包括文本节点)用一个HTML结构包裹起来
$("p").wrapInner("<b></b>");
$("div").wrapInner("<b></b>");//包装div里的所有内容
$("p").wrapInner(document.createElement("b"));
$("b").wrapInner(function(){
        return "<em></em>";
    });


replaceWith(content|fn) 将所有匹配的元素替换成指定的HTML或DOM元素。
$("div").replaceWith("<b>替换成功</b>");//全部替换，包括里面的内容清空
$(".third").replaceWith($(".first"));//用第一段替换第三段，你可以发现他是移动到目标位置来替换，而不是复制一份来替换。


replaceAll(selector) 用匹配的元素替换掉所有 selector匹配到的元素。与上面的方法效果相反
$("<b>Paragraph. </b>").replaceAll("p"); //b替换p

empty() 删除匹配的元素集合中所有的子节点。
$("div,p").empty();//清空p和div里的内容

remove([expr])
从DOM中删除所有匹配的元素。
这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。但除了这个元素本身得以保留之外，其他的比如绑定的事件，附加的数据等都会被移除。
$("p").remove();//上面是清空元素，这是删除
$("p").remove(".hello");//删除类为hello的p元素


detach([expr])
从DOM中删除所有匹配的元素。
这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。与remove()不同的是，所有绑定的事件、附加的数据等都会保留下来。



clone([Even[,deepEven]])
克隆匹配的DOM元素并且选中这些克隆的副本。
在想把DOM文档中元素的副本添加到其他位置时这个函数非常有用。
Events:一个布尔值（true 或者 false）指示事件处理函数是否会被复制
deepEvents:一个布尔值，指示是否对事件处理程序和克隆的元素的所有子元素的数据应该被复制

$("b").clone().prependTo("p");
克隆所有b元素（并选中这些克隆的副本），然后将它们前置到所有段落中。

创建一个按钮，他可以复制自己，并且他的副本也有同样功能。
$("button").click(function(){
  $(this).clone(true).insertAfter(this);
});

####筛选
eq(index|-index)
获取第N个元素
index:一个整数，表示元素基于0的位置
-index:一个整数，表示元素的位置，从集合中的最后一个元素开始倒数




