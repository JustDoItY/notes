# vue

- 1.双向绑定
- 2.启动vue， 安装vue/cli
- 3.v-modal指令实现双向绑定
- 4.以vue为后缀的文件为组件。有且仅有一个根包含块。@事件名 为绑定事件。
- 5.导入组件。在script标签内使用import导入要引用的组件。
  在components对象中引入要使用的组件。
  data函数返回组件中的数据。都需要在data中声明数据。
  methods对象
- 6.生命周期。
   (1)created：当组件被创建的时候，初始化组件。
   (2)monuted：把组件挂载到页面上，可以获取到dom元素了。
   (3)通过watch可以监听属性变化，有两个参数，preValue,oldValue。例： 
  -   watch:{
        属性名(preValue, oldValue) {

        }
      }

   (4)computed对象，当函数依赖的属性发生变化时就会调用。
   (5) props，可以接收传入组件的属性
- 7.引用dom元素
    在标签上添加ref=“name”指令，在组件对象内可以获取这个dom，this.$refs.name就是这个dom元素了
- 8.属性绑定，组件通信。
  msg 静态字符串绑定
  :msg 属性值（表达式）绑定，可以表达式运算
   
  子组件通信父组件：
      子组件使用$emit, 子组件标签中调用父组件函数。 child: this.$emit('name', 'props'); father: @name="myfunction"