# JavaScript 中的模块

【例】在文件/home/somebody/workspace/somemodule.js中第一行引用了一个模块：require(‘othermodule‘)，请问require查找模块的顺序是：

A. /home/somebody/workspace/node_modules/othermodule/index.js
B. /home/somebody/workspace/node_modules/othermodule. Js
C.CORE MODULES named othermodule
D./home/somebody/node_modules/othermodule/index.js

(1):首先，Node在当前目录下查找package.json(CommonJS包规范定义的包描述文件)，通过JSON.parse()解析出包描述对象，从中取出main属性指定的文件名进行定位。如果文件缺少扩展名，将会进入扩展名分析的步骤。 　　(2):而如果main属性制定的文件名错误，或者压根没有package.json文件，Node会将index当做默认文件名，然后依次查找index.js、index.node、index.json. 　　(3):如果在目录分析的过程中没有定位成功任何文件，则自定义模块进入下一个模块路径进行查找。如果模块路径数组都被遍历完毕，依然没有查找到目标文件，则会抛出查找失败异常。 　　按照上面的思路，首先应该查找package.json文件，看看里面有没有核心模块，应该是C最先，othermodule不是核心模块，那么接着应该进入扩展名分析的步骤，就应该是查找othermodule. js，对应B，紧接着就是以index为默认文件名，也就是A，再接下来就是上一个文件目录D了，
所以答案是： C B A D