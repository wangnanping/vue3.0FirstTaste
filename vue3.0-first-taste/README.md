# vue3.0-first-taste

## 第一步安装环境
(如果npm过慢可用cnpm)
```
npm i -g @vue/cli
```
```
vue create project-name
```
基于 Composition API 即 Function-based API 进行改造，配合 Vue Cli，优先体验 Vue3 特性
```
npm install @vue/composition-api -S
```
## start
```
npm install
```
```
npm run serve
```

## api

#### setup方法 (无法访问到 this)
setup是vue3.x中新的操作组件属性的方法，它是组件内部暴露出所有的属性和方法的统一API。<br>
看别人文章写的执行时机：beforeCreate 之后 created之前<br>
个人执行：setup -> beforeCreate -> created<br>
*prop* 参数  *context* 参数<br>
prop可以定义父组件允许传入的prop;<br>
context一个上下文对象，这个上下文对象中包含了一些有用的属性<br>
如下：
```javascript
 // 父
 <son name="值"></son>
 // 子
 props:{
     name:String
 },
 setup(props,context){
    console.log(props.name) // 值，如果props 不设置name 则获取不到父级传入值
    console.log(this) // undefined
    console.log(context)
       /*
        attrs: Object
        emit: ƒ ()
        listeners: Object
        parent: VueComponent
        refs: Object
        root: Vue
        ...
        */
 }
```
####  ref\reactive\toRefs
ref 处理简单的数据
reactive 监听所有的数据
toRefs 将reactive里面的数据state转换为ref形式的响应数据
``` javascript
import { ref, reactive, toRefs } from "vue";

export default {
  //   name: "ReactiveTest",
  //   created() {},
  //   beforeCreate() {},
  setup() {
    const refNum = ref(0);
    // 创建响应式数据对象，得到的 state 类似于 vue 2.x 中 data() 返回的响应式对象
    const state = reactive({
      count: 0,
      age: [
        {
          ageNumber: 1
        }
      ]
    });
    state.count += 1;
    console.log(state);
    // setup 函数中将响应式数据对象 return 出去，供 template 使用
    // 这样对象的写法就需要toRefs来转换state
    return {
      refNum,
      ...toRefs(state)
    };
  }
};
```
