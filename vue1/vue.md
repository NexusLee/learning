
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

### vue的生命周期

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

![image](https://v1-cn.vuejs.org/images/lifecycle.png)
