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

## 双向绑定
双向绑定使用v-model，将input、select等等与data中的数据绑定起来，这样修改了这些输入区的数据，data中的数据也会改变
。ps：下拉框所选值没有option时会变成未选中状态
```html
<div id="app">
    输入的文本：<input v-model="message" type="text">{{message}}
    <textarea v-model="message"></textarea>
    <input type="radio" name="sex" value="男" v-model="cp">男
    <input type="radio" name="sex" value="女" v-model="cp">女

    <p>选中了谁：{{cp}}</p>

    <p>下拉框</p>
    <select v-model="selected">
        <option>a</option>
        <option>b</option>
        <option>c</option>
    </select>
    <p>下拉框选中了{{selected}}</p>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            message:"cpcppc",
            cp:"",
            selected:""
        }
    });
</script>
```

## component(组件)
vue中可以使用``Vue.component(name,{})``创建一个组件,组件中有prop字段用来绑定来自其他地方的参数
```html
<div id="app">
<cp v-for="item in items" v-bind:cp="item"></cp>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    ///定义一个vue组件component
    Vue.component("cp",{
        props:['cp'],
        template: '<li>{{cp}}</li>'
    });

    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            items:["Java","Linux","前端"]
        }
    });
</script>
```