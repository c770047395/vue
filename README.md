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

## vue通信问题解决

### vue的生命周期
![](https://blog.kuangstudy.com/usr/uploads/2019/10/1579484219.jpg)


### jquery的ajax
不推荐使用

### axios
1. 首先引入js文件
```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```
2. 发送请求与接收响应
```javascript
axios.get('/vue/data.json').then(response=>(this.info=response.data));
```
接收的数据需要与Vue对象中data()方法绑定，属性一一对应
```javascript
var vm = new Vue({
    el: '#vue',
    data() {
      return{
          //请求的返回参数格式必须和json字符串一样
          info:{
              name:null,
              url:null,
              address:{
                  city:null,
                  street:null,
                  country:null
              }
          }
      }
    },
    mounted() {
        axios.get('/vue/data.json').then(response=>(this.info=response.data));
    }
})
```

## 计算属性
计算属性与data，methods同级，使用computed标识，与methods中的方法写法相似
```javascript
computed:{//计算属性,不能与methods中的方法重名，重名后会优先调用methods中的方法
    currentTime2:function () {
        this.message;//当属性发生变化时，会重新计算，否则不变
        return Date.now();//返回一个时间戳
    }
}
```
值得注意的是，计算属性是作为一个属性存在的，而不是方法，所以我们调用的时候可以直接使用``{{currentTime2}}``访问这个属性
，当计算属性内部的属性没有变化时，计算属性不会重新计算，相当于缓存，而当计算属性中的属性有变化时，则会重新计算结果
```html
<!--view层 模板-->
<div id="app">
    <p>currentTime1 {{currentTime1()}}</p>
    <p>currentTime2 {{currentTime2}}</p>

</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            message:"hello,cp"
        },
        methods:{
            currentTime1:function () {
                return Date.now();//返回一个时间戳
            }
        },
        computed:{//计算属性,不能与methods中的方法重名，重名后会优先调用methods中的方法
            currentTime2:function () {
                this.message;//当属性发生变化时，会重新计算，否则不变
                return Date.now();//返回一个时间戳
            }
        }
    });
</script>
```

## slot(插槽)
在组件中可以留出``<slot>``做为一个组件的拓展接口，称之为插槽，可以向插槽中填入不同的内容/组件以实现各种效果

1. 首先定义一个组件
```javascript
Vue.component("todo",{
    template:  '<div>\
                    <slot name="todo-title"></slot>\
                    <ul>\
                        <slot name="todo-items"></slot>\
                    </ul>\
                </div>'


});
```
2. 组件的title部分和li部分就可以由外部插入
```html
<div id="app">
    <todo>
        <h1 slot="todo-title">{{todoTitle}}</h1>
        <li slot="todo-items" v-for="item in todoItems">{{item}}</li>
    </todo>
</div>
```

或者在插槽部分插入其他的组件
```html
<div id="app">
    <todo>
        <todo-title slot="todo-title" :title="todoTitle"></todo-title>
        <todo-items slot="todo-items" v-for="item in todoItems" :item="item"></todo-items>
    </todo>
</div>
```
```html
<script>

    Vue.component("todo",{
        template:  '<div>\
                        <slot name="todo-title"></slot>\
                        <ul>\
                            <slot name="todo-items"></slot>\
                        </ul>\
                    </div>'


    });
    Vue.component("todo-title",{
        props:['title'],
        template: '<div>{{title}}</div>'
    })
    Vue.component("todo-items",{
        props:['item'],
        template: '<li>{{item}}</li>'
    })

    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            todoTitle:"hello",
            todoItems:['cpcp','linux','java']
        }
    });
</script>
```

## 自定义事件
如果在组件中想要操作vue对象中的data需要如下步骤：
1. 在vue对象中定义方法(只有vue对象中的方法才能访问vue的属性)
```javascript
methods: {
    removeItems: function(index){
        console.log("删除了"+this.todoItems[index])
        this.todoItems.splice(index,1);//一次删除一个元素
    }
}
```
2. 将需要操作数据的组件添加一个自定义事件(使用v-on:)
```javascript
<todo-items slot="todo-items" v-for="(item,index) in todoItems" :item="item" :index="index" v-on:remove="removeItems(index)"></todo-items>

```
3. 在组件内通过this.$emit('自定义事件名',参数)接收事件并绑定当前组件内的方法
```javascript
methods:{
    remove: function(index){
        this.$emit('remove',index);
    }
},
```
4. 组件内按钮绑定这个方法
```html
<button @click="remove">删除</button>
```
这样就完成了一个自定义事件

实例：
```html
<!--view层 模板-->
<div id="app">
    <todo>
        <todo-title slot="todo-title" :title="todoTitle"></todo-title>
<!--        <h1 slot="todo-title">{{todoTitle}}</h1>-->
        <todo-items slot="todo-items" v-for="(item,index) in todoItems" :item="item" :index="index" v-on:remove="removeItems(index)"></todo-items>
<!--        <li slot="todo-items" style="color:red" v-for="item in todoItems">{{item}}</li>-->
    </todo>
</div>

<!--导入vue.js-->
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<script>

    Vue.component("todo",{
        template:  '<div>\
                        <slot name="todo-title"></slot>\
                        <ul>\
                            <slot name="todo-items"></slot>\
                        </ul>\
                    </div>'


    });
    Vue.component("todo-title",{
        props:['title'],
        template: '<div>{{title}}</div>'
    })
    Vue.component("todo-items",{
        props:['item','index'],
        template: '<li>{{index}}---{{item}}<button @click="remove">删除</button></li>',
        methods:{
            remove: function(index){
                this.$emit('remove',index);
            }
        },

    })

    var vm = new Vue({
        el:"#app",
        // model层 数据
        data:{
            todoTitle:"hello",
            todoItems:['cpcp','linux','java']
        },
        methods: {
            removeItems: function(index){
                console.log("删除了"+this.todoItems[index])
                this.todoItems.splice(index,1);//一次删除一个元素
            }
        }
    });
</script>

```
