### 01、VUE学习

VUE给元素添加数据语法：

```html
	<div id = "app">
        <!-- {{}}里是一个变量名，也可以是一个方法名 -->
        <h1>website : {{website}}</h1>
        <h1>URL : {{URL}}</h1>
        <h1>{{details()}}</h1>
    </div>

	<script type="text/javascript">
        var firstVue = new Vue({
            // 元素id、类名
            el : "#app",
            data : {
                website : "菜鸟教程",
                URL : "https://www.runoob.com/vue2/vue-start.html",
                alexa: "10000"
            },
            methods : {
                details : function() {
                    return this.website + "-学的不仅是技术，更是梦想！";
                }
            }
        });
    </script>
```

这样之后，会将script标签中firstVue对象的data中对应的数据赋值给对应的{{}}中，例如website会赋值给website