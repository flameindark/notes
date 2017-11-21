## 种子模块
> 也叫核心模块，是框架最先执行的部分
### 1.1 命名空间
> 防止变量的污染，功能多了后产生的变量命名冲突问题以及多个库之间的变量冲突。(最初的prototype.js库直接污染了js的原生对象)

- jQuery的解决方式：
``` javascript
    var _jQuery = window.jQuery, _$ = window.$; //先把可能的同名变量保存，如果没有的话那么_jQuery,_$为undefined
    jQuery.extend({
        noConflict: function(deep) {
            window.$ = _$; // 如果调用了noConflict方法jQuery则将$让出去
            if(deep)
                window.jQuery = _jQuery;// 如果deep都为true的话那么将jQuery也让出去
            return jQuery; // 然后将闭包中间的jQuery(真正的jQuery)返回，只要调用noConflict方法时在外面用自己命名的变量接住就行。
        }
    })
```
