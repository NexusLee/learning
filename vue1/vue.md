双向绑定原理
------

<p align="center">
  <img src='https://github.com/NexusLee/learning/blob/master/vue1/images/articlex.png' width='100%' height='100%' alt='vue生命周期' />
</p>


  ``` javascript
    let data = { price: 5, quantity: 2 };
    let target = null;

    class Dep { 
      constructor() {
        this.subscribers = [];
      }
      depend() { //依赖收集
        if(target && !this.subscribers.includes(target)) {
          this.subscribers.push(target);
        }
      }
      notify() { //通知
        this.subscribers.forEach(sub => sub());
      }
    }

    //遍历data属性
    Object.keys(data).forEach(key => {
      let internalValue = data[key];
      //每个属性生成单独的依赖实例
      const dep = new Dep();

      Object.defineProperty(data, key, { //拦截器
        get() {
          dep.denpend(); //添加到订阅数组
          return internalValue;
        },
        set(newVal) {
          internalValue = newVal;
          dep.notify(); //通知更新
        }
      })
    });

    function watcher(func) { //监听函数
      target = func;
      target(); //间接调用依赖收集
      target = null;
    }

    watcher(() => {
      data.total = data.price * data.quantity;
    })

    // data.total
    // 10
    // data.price = 20
    // data.total 
    // 40
    // data.quantity = 3
    // 3
    // data.total
    // 60
  ```

安装
------

  ``` sh
    # 全局安装 vue-cli
    $ npm install -g vue-cli
    # 创建一个基于 "webpack" 模板的新项目
    $ vue init webpack#1.0 my-project
    # 安装依赖
    $ cd my-project
    $ npm install
    $ npm run dev
  ```

Vue 实例
------

  ``` javascript
    var vm = new Vue({　//Vue实例
      el: "选择器",    //挂载到页面的那个元素里，即确定vue的作用范围  外部可通过vm.$el访问，得到的是一个原生dom元素，可进行对应操作
      a: '',          //自定义属性  外部可通过vm.$options访问
      data: {
          a: 1
        },      //实例属性都在这里面，外部通过实例名,即vm.$data调用
      computed: { },  //计算属性，也是实例属性，只是以方法的形式存在，并可以有逻辑运算的属性
      method: { },    //实例方法都在这里
      watch: { },     //对data和computed的属性进行监听，当属性有变化时自动触发，以方法的形式存在 外部通过$.watch调用
                      //注意：以上属性和方法，实例内部都通过this调用,外部则通过对应的实例方法访问
                      //在vue的生命周期过程中，它自身还提供了一系列的钩子函数供我们使用，进行自定义逻辑的注入：　　　
      created: function(){         
            console.log('a is: ' + this.a) // `this` 指向 vm 实例
        }, //实例已经创建
      beforeCompile: function(){ 
          模块编译之前 
        },
      compiled: function(){ 
          模块编译之后；即模板占位符被是内容替换
        },
      ready: function(){ 
          模板插入到文档中了；相当于window.onload 
        },             //Vue2.0已改为mounted
                     //注意： 以上4个方法在对象被实例化后即按顺序执行，以下2个方法需通过事件触发，并通过调用 实例名.$destory() 才执行
      beforeDestroy: function(){ 
          对象销毁之前 
        },
      destroyed: function(){ 
          对象销毁之后 
        }
    });
  ```

#### #vue 的生命周期

| 周期          |      解释      |  
|---------------|:-------------:|
| init          | 组件刚刚被创建，但是Data、method等属性还没有被计算 |
| created       | 组件创建已经完成，在加载数据中加载   |  
| beforeCompile | 模板编译之前加载 |
| compiled      | 编译完成后加载 |
| ready         | 组件准备加载的时候加载 |
| attached      | 在vm.$el从Dom时调用 |
| datched       | 在vm.$el从Dom删除时调用 |
| beforeDestory | 组件销毁之前 |
| destory       | 组件销毁之后 |

<p align="center">
  <img src='https://v1-cn.vuejs.org/images/lifecycle.png' width='50%' height='50%' alt='vue生命周期' />
</p>

#### # 属性与方法

##### 每个 Vue 实例都会代理其 data 对象里所有的属性：

  ``` javascript
    var data = { a: 1 }
    var vm = new Vue({
      data: data
    })
    vm.a === data.a // -> true
    // 设置属性也会影响到原始数据
    vm.a = 2
    data.a // -> 2
    // ... 反之亦然
    data.a = 3
    vm.a // -> 3
  ```
  
  ###### 只有这些被代理的属性是响应的。除了这些数据属性，Vue 实例暴露了一些有用的实例属性与方法。这些属性与方法都有前缀 $，以便与代理的数据属性区分。

  ``` javascript
    var data = { a: 1 }
    var vm = new Vue({
      el: '#example',
      data: data
    })
    vm.$data === data // -> true
    vm.$el === document.getElementById('example') // -> true
    // $watch 是一个实例方法
    vm.$watch('a', function (newVal, oldVal) {
      // 这个回调将在 `vm.a`  改变后调用
    })
  ```

数据绑定
------

#### # 文本插值

  ###### 数据绑定最基础的形式是文本插值，使用 “Mustache” 语法（双大括号）：

  ``` javascript
    <span>Message: {{ msg }}</span>
  ```

  ###### 你也可以只处理单次插值，今后的数据变化就不会再引起插值更新了：
  
  ``` javascript
    <span>This will never change: {{* msg }}</span>
  ```

#### # HTML 属性

  ###### Mustache 标签也可以用在 HTML 属性 (Attributes) 内：
  
  ``` javascript
    <div id="item-{{ id }}"></div>
  ```

#### # 绑定表达式

  ``` javascript
    {{ number + 1 }}
    {{ ok ? 'YES' : 'NO' }}
    {{ message.split('').reverse().join('') }}
  ```

  ###### 这些表达式将在所属的 Vue 实例的作用域内计算。一个限制是每个绑定只能包含单个表达式，因此下面的语句是无效的：
  
  ``` javascript
    <!-- 这是一个语句，不是一个表达式： -->
    {{ var a = 1 }}
    <!-- 流程控制也不可以，可改用三元表达式 -->
    {{ if (ok) { return message } }}
  ```

#### # 过滤器

  ###### Vue.js 允许在表达式后添加可选的“过滤器 (Filter) ”，以“管道符”指示：

  ``` javascript
    {{ message | capitalize }}
  ```

  ###### 过滤器可以串联：

  ``` javascript
    {{ message | filterA | filterB }}
  ```

  ###### 过滤器也可以接受参数：

  ``` javascript
    {{ message | filterA 'arg1' arg2 }}
  ```

  ###### 过滤器函数始终以表达式的值作为第一个参数。带引号的参数视为字符串，而不带引号的参数按表达式计算。这里，字符串 'arg1' 将传给过滤器作为第二个参数，表达式 arg2 的值在计算出来之后作为第三个参数。

  ###### Vue 自带的过滤器: capitalize、uppercase、lowercase、currency、pluralize、debounce、limitBy、filterBy、orderBy。

  ``` HTML
    <div id ="app">
        {{ date | formatDate }}
    </div>
  ```
  ``` javascript
    var padDate = function(){
        //在月份、日期、小时等于小于10前补0
        return value <10 ? '0' + value : value;
    }
    var app = new Vue({
        el:"#app",
        data:{
            date:new Date()
        },
        filters:{
            formatDate: function(value) {
                var date = new Date(value);
                var year = date.getFullYear();
                var month = padDate(date.getMonth()+1);
                var day = padDate(date.getDate());
                var hours = padDate(date.getHours());
                var minutes = padDate(date.getMinutes());
                var seconds = padDate(date.getSeconds());
                //将整理的数据返回出去
                return year + "-" + month + "-" + day + " " + hours + ":" + minutes + ":" + seconds;
            }
        }
    })
  ```

#### # 指令 

> 指令 (Directives) 是特殊的带有前缀 v- 的特性。指令的值限定为绑定表达式，因此上面提到的 JavaScript 表达式及过滤器规则在这里也适用。指令的职责就是当其表达式的值改变时把某些特殊的行为应用到 DOM 上。

  ``` HTML
    <p v-if="greeting">Hello!</p>
  ```

  ###### 有些指令可以在其名称后面带一个“参数” (Argument)，中间放一个冒号隔开。例如，v-bind 指令用于响应地更新 HTML 特性：

  ``` HTML
    <a v-bind:href="url"></a>
  ```

  ###### 这里 href 是参数，它告诉 v-bind 指令将元素的 href 特性跟表达式 url 的值绑定。可能你已注意到可以用特性插值 href="{{url}}" 获得同样的结果：这样没错，并且实际上在内部特性插值会转为 v-bind 绑定。

  ###### 另一个例子是 v-on 指令，它用于监听 DOM 事件：

  ``` HTML
  <a v-on:click="doSomething">
  ```

  ###### 这里参数是被监听的事件的名字

#### # 缩写

> ###### v- 前缀是一种标识模板中特定的 Vue 特性的视觉暗示。当你需要在一些现有的 HTML 代码中添加动态行为时，这些前缀可以起到很好的区分效果。但你在使用一些常用指令的时候，你会感觉一直这么写实在是啰嗦。而且在构建单页应用（SPA ）时，Vue.js 会管理所有的模板，此时 v- 前缀也没那么重要了。因此Vue.js 为两个最常用的指令 v-bind 和 v-on 提供特别的缩写：

- ##### v-bind 缩写:
  
  ``` HTML
    <!-- 完整语法 -->
    <a v-bind:href="url"></a>
    <!-- 缩写 -->
    <a :href="url"></a>
    <!-- 完整语法 -->
    <button v-bind:disabled="someDynamicCondition">Button</button>
    <!-- 缩写 -->
    <button :disabled="someDynamicCondition">Button</button>
  ```

- ##### v-on 缩写:

  ``` HTML
    <!-- 完整语法 -->
    <a v-on:click="doSomething"></a>
    <!-- 缩写 -->
    <a @click="doSomething"></a>
  ``` 

组件
------

#### # 使用组件

- ##### 注册

  ``` HTML  
    <div id="example">
      <my-component></my-component>
    </div>
  ```

  ``` javascript
    // Vue.extend() 创建一个组件构造器
    var MyComponent = Vue.extend({
      template: '<div>A custom component!</div>'
    })
    // 全局注册组件, 把这个构造器用作组件
    Vue.component('my-component', MyComponent)
    // 创建根实例
    new Vue({
      el: '#example'
    })
  ```

  ###### 渲染为：

  ``` HTML
    <div id="example">
      <div>A custom component!</div>
    </div>
  ```

- ##### 局部注册

  ###### 不需要全局注册每个组件。可以让组件只能用在其它组件内，用实例选项 components 注册：

  ``` javascript
    var Child = Vue.extend({ /* ... */ })
    var Parent = Vue.extend({
      template: '...',
      components: {
        // <my-component> 只能用在父组件模板内
        'my-component': Child
      }
    })

```

- ##### 注册语法糖

  ###### 为了让事件更简单，可以直接传入选项对象而不是构造器给 `Vue.component()` 和 `component` 选项。Vue.js 在背后自动调用 `Vue.extend()`：

  ``` javascript
    // 在一个步骤中扩展与注册
    Vue.component('my-component', {
      template: '<div>A custom component!</div>'
    })
    // 局部注册也可以这么做
    var Parent = Vue.extend({
      components: {
        'my-component': {
          template: '<div>A custom component!</div>'
        }
      }
    })
  ```

#### # Props

- ##### 使用Props传递数据

  ###### 组件实例的作用域是孤立的。这意味着不能并且不应该在子组件的模板内直接引用父组件的数据。可以使用 `props` 把数据传给子组件。

  ###### “prop” 是组件数据的一个字段，期望从父组件传下来。子组件需要显式地用 `props` 选项 声明 `props`：

  ``` javascript
    Vue.component('child', {
      // 声明 props
      props: ['msg'],
      // prop 可以用在模板内
      // 可以用 `this.msg` 设置
      template: '<span>{{ msg }}</span>'
    })

  ```  
  ###### 然后向它传入一个普通字符串：

  ``` HTML
    <child msg="hello!"></child>
  ```

- #####  动态 Props 

  ###### 类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 绑定动态 Props 到父组件的数据。每当父组件的数据变化时，也会传导给子组件：

  ``` HTML
    <div>
      <input v-model="parentMsg">
      <br>
      <child :my-message="parentMsg"></child>
    </div>
  ```

- #####  Prop 绑定类型

  ###### prop 默认是单向绑定：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意修改了父组件的状态——这会让应用的数据流难以理解。不过，也可以使用 .sync 或 .once 绑定修饰符显式地强制双向或单次绑定：

  ``` HTML
    <!-- 默认为单向绑定 -->
    <child :msg="parentMsg"></child>
    <!-- 双向绑定 -->
    <child :msg.sync="parentMsg"></child>
    <!-- 单次绑定 -->
    <child :msg.once="parentMsg"></child>
  ```

> ###### 注意如果 prop 是一个对象或数组，是按引用传递。在子组件内修改它会影响父组件的状态，不管是使用哪种绑定类型。

- #####  Prop 验证

  ###### 组件可以为 props 指定验证要求。当组件给其他人使用时这很有用，因为这些验证要求构成了组件的 API，确保其他人正确地使用组件。

  ``` javascript
    Vue.component('example', {
      props: {
        // 基础类型检测 （`null` 意思是任何类型都可以）
        propA: Number,
        // 多种类型 (1.0.21+)
        propM: [String, Number],
        // 必需且是字符串
        propB: {
          type: String,
          required: true
        },
        // 数字，有默认值
        propC: {
          type: Number,
          default: 100
        },
        // 对象/数组的默认值应当由一个函数返回
        propD: {
          type: Object,
          default: function () {
            return { msg: 'hello' }
          }
        },
        // 指定这个 prop 为双向绑定
        // 如果绑定类型不对将抛出一条警告
        propE: {
          twoWay: true
        },
        // 自定义验证函数
        propF: {
          validator: function (value) {
            return value > 10
          }
        },
        // 转换函数（1.0.12 新增）
        // 在设置值之前转换值
        propG: {
          coerce: function (val) {
            return val + '' // 将值转换为字符串
          }
        },
        propH: {
          coerce: function (val) {
            return JSON.parse(val) // 将 JSON 字符串转换为对象
          }
        }
      }
    })
  ```
###### `type` 可以是下面原生构造器：
  - ###### String
  - ###### Number
  - ###### Boolean
  - ###### Function
  - ###### Object
  - ###### Array
  
###### 当 prop 验证失败了，Vue 将拒绝在子组件上设置此值，如果使用的是开发版本会抛出一条警告。

#### # 父子组件通信

- #####  父链

  ###### 子组件可以用 `this.$parent` 访问它的父组件。根实例的后代可以用 `this.$root` 访问它。父组件有一个数组 `this.$children`，包含它所有的子元素。

  ###### 尽管可以访问父链上任意的实例，不过子组件应当避免直接依赖父组件的数据，尽量显式地使用 `props` 传递数据。另外，在子组件中修改父组件的状态是非常糟糕的做法，因为：

      1. 这让父组件与子组件紧密地耦合；

      2. 只看父组件，很难理解父组件的状态。因为它可能被任意子组件修改！理想情况下，只有组件自己能修改它的状态。
     
- #####  自定义事件

  ###### Vue 实例实现了一个自定义事件接口，用于在组件树中通信。这个事件系统独立于原生 DOM 事件，用法也不同。

  ###### 每个 Vue 实例都是一个事件触发器：

      使用 `$on()` 监听事件；

      使用 `$emit()` 在它上面触发事件；

      使用 `$dispatch()` 派发事件，事件沿着父链冒泡；

      使用 `$broadcast()` 广播事件，事件向下传导给所有的后代。
      
      ``` HTML
      <!-- 子组件模板 -->
        <template id="child-template">
          <input v-model="msg">
          <button v-on:click="notify">Dispatch Event</button>
        </template>
        <!-- 父组件模板 -->
        <div id="events-example">
          <p>Messages: {{ messages | json }}</p>
          <child></child>
        </div>
      ```
      ```
        // 注册子组件
        // 将当前消息派发出去
        Vue.component('child', {
          template: '#child-template',
          data: function () {
            return { msg: 'hello' }
          },
          methods: {
            notify: function () {
              if (this.msg.trim()) {
                this.$dispatch('child-msg', this.msg)
                this.msg = ''
              }
            }
          }
        })
        // 初始化父组件
        // 将收到消息时将事件推入一个数组
        var parent = new Vue({
          el: '#events-example',
          data: {
            messages: []
          },
          // 在创建实例时 `events` 选项简单地调用 `$on`
          events: {
            'child-msg': function (msg) {
              // 事件回调内的 `this` 自动绑定到注册它的实例上
              this.messages.push(msg)
            }
          }
        })
      ```
      
- #####  使用-v-on-绑定自定义事件

  ###### 上例非常好，不过从父组件的代码中不能直观的看到 `"child-msg"` 事件来自哪里。如果我们在模板中子组件用到的地方声明事件处理器会更好。为此子组件可以用 `v-on` 监听自定义事件：
  
  ``` HTML
    <child v-on:child-msg="handleIt"></child>
  ```
  ###### 这样就很清楚了：当子组件触发了 `"child-msg"` 事件，父组件的 `handleIt` 方法将被调用。所有影响父组件状态的代码放到父组件的 `handleIt` 方法中；子组件只关注触发事件。
  
  
  
