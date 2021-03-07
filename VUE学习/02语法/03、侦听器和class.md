### 侦听器和class

1、由于计算属性会存在缓存，若获取了当前时间，那么使用计算属性的话，这个时间就不会再改变。所以需要侦听器来实现。watch

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>侦听器</title>
</head>
<body>
    <div id = "app">
        <h1>{{msg}}</h1>
        <h1>{{resvermsg}}</h1>
    </div>
    <script type="text/javascript">
        var firstVue = new Vue({
            // 元素id、类名
            el : "#app",
            data : {
                msg : "hello!"
            },
            //计算属性
            computed : {
                resvermsg :{
                    get : function() {
                        return this.msg.split("").reverse().join("");
                    },
                    set : function(val) {
                        return this.msg = val;
                    }
                }
            },
            //侦听器val为更新的值
            watch : {
                msg : function(val) {
                    console.log("监听事件");
                    console.log(val);
                }
            }
        });
    </script>
    
</body>
</html>
~~~

2、class，我们可以传给v-bind:class一个对象，以动态切换class，可放置多个class样式，若class名存在-等非法字符，需要用双引号

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style>
        .page{
            width: 200px;
            height: 200px;
            background: skyblue;
            display: none;
        }
        .active{
            display: block;;
        }
    </style>
    <title>class样式</title>
</head>
<body>
    <div id = "app">
        <!-- 通过对象的方式觉定是否存在某个类 -->
        <div class = "page" :class = "{active:isActive}"></div>
        <!-- 直接放置对象 -->
        <div class = "page" :class = "styleObj"></div>
        <!-- 直接放置数组 -->
        <div class = "page" :class = "styleArr"></div>
        <!-- 直接放置字符串 -->
        <div class = "page" :class = "styleStr"></div>
        <!-- 数组和对象同时使用 -->
        <div class = "page" :class = "styleArrObj"></div>
        <button @click = "changeColor">改变样式</button>
    </div>
    <script type="text/javascript">
        var firstVue = new Vue({
            // 元素id、类名
            el : "#app",
            data : {
                isActive : true,
                styleObj : {active:true,laochen:true},
                styleArr : ['col-12-xs','red-bg'],
                styleStr : "abc def ghi",
                styleArrObj : ["abc",{active:true}]
            },
            methods : {
                changeColor : function() {
                    this.isActive = !this.isActive;
                }
            }
        });
    </script>
    
</body>
</html>
~~~

