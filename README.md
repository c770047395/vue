## 第一个vue程序
```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--view层 模板-->
<div id="app">
    <span v-bind:title="message"> hhhhhh</span>
<!--    <span>{{message}}</span>-->
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            message:"hello,vue"
        }
    });
</script>

</body>
</html>
```


## if和for
使用v-if标签和v-for标签完成
```html
<!--view层 模板-->
<div id="app">
    <h1 v-if="type==='A'">A</h1>
    <h1 v-else-if="type==='B'">B</h1>
    <h1 v-else>C</h1>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            type: 'A'
        }
    });
</script>
```
```html
<div id="app">
    <li v-for="item in items">{{item.message}}</li>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            items:[
                {message:'cpcp'},
                {message:'apap'},
                {message:'howhow'}
            ]
        }
    });
</script>
```

## 事件绑定
使用v-on进行事件绑定，注意：方法只能在Vue对象中的methods中定义，否则取不到
```html
<div id="app">
    <button v-on:click="sayHi">click me</button>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            message:"cpcppc"
        },
        methods:{ // 方法必须定义在Vue的method对象中
            sayHi:function () {
                alert(this.message)
            }
        }
    });
</script>
```