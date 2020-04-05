---
title: '''json,异步加载,时间线'''
author: Darren
avatar: 'https://cdn.jsdelivr.net/gh/MINTACO/cdn@1.3/img/custom/avatar.jpg'
authorLink: mintaco.cn
authorAbout: 像风一样自由
authorDesc: 像风一样自由
categories: 开发
comments: true
tags: Javascript
photos: 'https://i.loli.net/2019/12/14/j36bxu5srdUBtH7.png'
date: 2020-02-28 15:54:52
keywords:
description:
---
# 1.JSON
取代xml作为前后端传输数据的方式，传输JSON字符串
```
//属性名必须加双引号
{
    "name" : "Darren",
    "age" : 23 
}
//JSON ==> string
JSON.stringify(obj);

//string ==> JSON
JSON.parse(str)
```

# 2.异步加载js
1. defer异步加载,但要等到dom文档全部解析完才会被执行。只有IE生效，也可以将代码写到内部。
   ```
   <script type="text/javascript" src="./tool.js" defer="defer"></script>
   ```
2. async异步加载，加载完就执行（异步执行，不会阻断页面），async只能加载外部脚本，不能把js写在标签内部。标准浏览器均生效。
3. （最常用，兼容性最好）创建script，插入到DOM中，加载完后callback
   ```
   function loadScript(url, callback){
        var script = document.createElement('script');
        script.type = "text/javascript";
        if(script.readyState){
            script.onreadystatechange = function(){
                if(script.readyState === "complete" || script.readyState === "loaded"){
                    callback();
                }
            }
        }else{
            script.onload = function(){
                callback();
            }
        }
        script.src = url;
        document.head.appendChild(script);
    }
   ```
   # 3.时间线
   1. 创建Document对象，开始解析web页面。解析HTML元素和他们的文本内容后添加Element对象和Text节点到文档中。这个过程document.readyState = 'loading'。
   2. 遇到link外部css，创建线程加载，并继续解析文档。
   3. 遇到script外部js，并且没有设置async和defer，浏览器加载并阻塞，等待js加载完成并执行该脚本，然后继续解析文档；对于有设置async和defer的，浏览器创建线程加载并继续解析文档，对于async属性的脚本，加载完后立即执行（异步禁止使用document.write()）。
   4. 遇到img等，先正常解析dom结构，然后浏览器异步加载src，并继续解析文档。
   5. 当文档解析完成，document.readyState = 'interactive'。
   6. 文档解析完成后，所有设置defer的脚本会按顺序执行。（同样禁止使用document.write()）。
   7. document对象触发DOMContentLoaded事件，这也标志着程序执行从同步脚本执行阶段转化为事件驱动阶段。
   8. 当所有async的脚本加载完成并执行后，img等加载完成后，document.readyState = 'complete',window对象触发load事件。
   9. 至此浏览器以异步方式处理用户输入，网络事件等。
   
   代替window.onload的方法
   ```
    document.addEventListener('DOMContentLoaded',function(){
            //执行语句
    },false)
   ```