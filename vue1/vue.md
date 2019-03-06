
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


### 安装

``` sh
  # 全局安装 vue-cli
  $ npm install -g vue-cli
  # 创建一个基于 "webpack" 模板的新项目
  $ vue init webpack#1.0 my-project
  # 安装依赖，走你
  $ cd my-project
  $ npm install
  $ npm run dev
```

### vue 1.x 的生命周期

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

### vue 1.x 的语法

``` javascript
var vm = new Vue({　
　　el: "选择器",  挂载到页面的那个元素里，即确定vue的作用范围  外部可通过vm.$el访问，得到的是一个原生dom元素，可进行对应操作
　　a: '',  //自定义属性  外部可通过vm.$options访问
　　data: { }, //实例属性都在这里面，外部通过实例名,即vm.$data调用
　　computed: { }, //计算属性，也是实例属性，只是以方法的形式存在，并可以有逻辑运算的属性
　　method: { }, //实例方法都在这里
　　watch: { }, //对data和computed的属性进行监听，当属性有变化时自动触发，以方法的形式存在 外部通过$.watch调用
　　//注意：以上属性和方法，实例内部都通过this调用,外部则通过对应的实例方法访问
　　//在vue的生命周期过程中，它自身还提供了一系列的钩子函数供我们使用，进行自定义逻辑的注入：　　　
　　created: function(){ 
      实例已经创建 
    },
　　beforeCompile: function(){ 
      模块编译之前 
    },
　　compiled: function(){ 
      模块编译之后；即模板占位符被是内容替换
    },
　　ready: function(){ 
      模板插入到文档中了；相当于window.onload 
    }, //Vue2.0已改为mounted
　　注意： 以上4个方法在对象被实例化后即按顺序执行，以下2个方法需通过事件触发，并通过调用 实例名.$destory() 才执行
　　beforeDestroy: function(){ 
      对象销毁之前 
    },
　　destroyed: function(){ 
      对象销毁之后 
    }
});
```
