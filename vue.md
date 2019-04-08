# Vue

##### 指令

> 在vue中提供了一些对于页面+数据的更为方便的操作，这些操作就叫做指令  `v-xxx`
>
> 指令中封装了一些DOM行为，结合属性作为一个暗号，根据不同的值框架会进行相关的DOM操作的绑定

- v-text  ：innertext

- v-html：innerhtml

- v-if   ：是否插入元素

- v-else-if

- v-else

- v-show  ：是否隐藏元素

- v-bind：给元素的属性赋值    绑定属性值  单向数据绑定  vue->页面

  - ```html
    <div v-bind:属性名 = "变量"></div>
    <div :属性名 = "变量"></div>
    
     // 当给dom元素绑定一个原生的属性值  而需要用到Data里面的值时
    <div :title = "data.name"></div>
    ```

- v-on  绑定事件

  - ```html
    <button v-on:click="btn"></button>
    <button @click="btn"></button>
    ```

- v-model只能给有value属性的元素进行双向数据绑定    vue->页面,页面->vue

  - ```javascript
    object.defineProperty(obj.key,
                          {get(){return value;}
                           ,set(newVal){}}
                         )
    ```

- v-for

  - ```html
    <ul>
        <li v-for="item in arr" :class="item.myclass">
        	{{ iten }}
        </li>
    </ul>
    //数组
    <ul>
        <li v-for="(item,index) in arr" :class="index%2==0?'red':'green'">
        	{{ iten }}
        </li>
    </ul>
    
    //对象
    <ul>
        <li v-for="(val,key,index) in obj" :class="index%2==0?'red':'green'">
        	{{ val }}{{key}}{{index}}
        </li>
    </ul>
    ```

##### 父子路由传值

父传子：子组件 声明  props：   接收参数    用时直接用父组件定义的变量

父用子   子组件 声明子组件  使用子组件的变量



##### options的常用选项

**一、new一个Vue事例**

- el：（string｜｜DOM元素） 挂载元素

- template  模版

- data    在组件中是一个函数，return一个对象  对象中的key，可以直接在页面中使用。在js中，this.key名

  - data中的属性   在dom中直接用   ，在js中  this.xxx

- components：key是组件名，value是组件对象

- methods：一般用来配合  事件的调用

- props：子组件接受的参数设置['title']

- ```javascript
  var app = new Vue({
      el:'#app',
      data:{
          item:['item','item1'],
          todo:''
      },
      methods:{
          rm:function(i){
              this.items.splice(i,1)
          }
      }
  })
  ```

  

**二、直接使用**

```javascript
export default {
    name:'',
    components:{},
    data:(){},
    watch:{},  // 监视
    computed:{},  // 计算成员
    created: function(){},
    methods:{},  // methods  对象成员
    actions:{}
}
```

- watch监视

  - watch监视是一个对象，键是需要观察的表达式，值可以是回调函数、方法名、包含选项的对象

- watch和computed各自处理的数据关系场景不同

  1.**watch**擅长处理的场景：**一个数据影响多个数据**

  2.**computed擅**长处理的场景：**一个数据受多个数据影响**

##### filter||filters

- 全局过滤器

  - ```javascript
    Vue.filter('capitalize', function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    })
    Vue.filter('reverse', function (value) {
       return value.split('').reverse().join('');
    })
    ```

  - 

- 自定义过滤器  组件中的过滤器

  - ```javascript
    // HTML
    <div id="app">
     <input type="text" v-model="message" />
     {{message | capitalize }}
    </div>
    
    // JS中
    var vm=new Vue({
        el:"#app",
        data:{
            message:''
        },
        filters: {
          capitalize: function (value) {
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
          }
        }
    })
    ```

  - 

# 父子路由之间传值

**父传子组件的值或方法: **  

```javascript
//父组件
<parent>
    <child :child-msg="msg"></child>    //这里必须要用 - 代替驼峰
</parent>
data(){
    return {
        msg: [1,2,3]
    };
}

//子组件  
// 方法一    数组方式
props：['childMsg']
//方法二  对象方式  可以指定类型和默认值
props: {
    childMsg: Array //这样可以指定传入的类型，如果类型不对，会警告
}
//方法三
props: {
    childMsg: {
        type: Array,
        default: [0,0,0] //这样可以指定默认的值
    }
}


```



**子调父:**  

```java
子组件绑定一个方法 在方法中调用  this.$emit(‘父方法’，‘值’)

// 子组件:
<template>
    <div @click="up"></div>
</template>

methods: {
    up() {
        this.$emit('upup','hehe'); //主动触发upup方法，'hehe'为向父组件传递的数据
    }
}

// 父组件:
<div>
    <child @upup="change" :msg="msg"></child> //监听子组件触发的upup事件,然后调用change方法
</div>
methods: {
    change(msg) {
        this.msg = msg;
    }
}
```



**非父子传值:**  

```javascript
// 如果2个组件不是父子组件那么如何通信呢？这时可以通过eventHub来实现通信. 
// 所谓eventHub就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件.

let Hub = new Vue(); //创建事件中心

//组件1触发：
<div @click="eve"></div>
methods: {
    eve() {
        Hub.$emit('change','hehe'); //Hub触发事件
    }
}

//组件2接受：
<div></div>
created() {
    Hub.$on('change', () => { //Hub接收事件
        this.msg = 'hehe';
    });
}
```



### vue更新插件版本

```javascript
//查看最新版本
ncu
//upgrade package.json  升级 package.json
ncu -u
//下载新版本
 npm install
```



```
//清空data（）中 的数据
Object.assign(that.$data, that.$options.data())
```





### element  table  列中的数据循环

```javascript
<el-table-column prop="position" label="求职职位" show-overflow-tooltip>
  <template scope="scope">
    <div v-for='(index,item) in JSON.parse(scope.row.position)'>{{item.dictName}}</div>
  </template>
</el-table-column>
```



### vue  key的作用

两个相同的组件产生类似的DOM结构，不同的组件产生不同的DOM结构

同一层级的一组节点，他们可以通过唯一的id进行区分

**如果节点类型不同，直接干掉前面的节点，再创建并插入新的节点，不会再比较这个节点以后的子节点了。**

**如果节点类型相同，则会重新设置该节点的属性，从而实现节点的更新。**

**需要使用key来给每个节点做一个唯一标识，Diff算法就可以正确的识别此节点，找到正确的位置区插入新的节点。**

**key的作用主要是为了高效的更新虚拟DOM**



