# vue3.0-first-taste

## 第一步安装环境
(如果npm过慢可用cnpm)
```
npm i -g @vue/cli
```
```
vue create project-name
```
基于 Composition API 即 Function-based API 进行改造，配合 Vue Cli，优先体验 Vue3 特性 (直接使用vue也是可以的)
```
npm install @vue/composition-api -S
```
直接使用import { ref, provide } from 'vue'也是可以的
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
ref 处理简单的响应式数据
isRef 判断是否为ref创建 boolean
reactive 监听所有的响应式数据
toRefs 函数可以将 reactive() 创建出来的响应式对象，转换为普通的对象，只不过，这个对象上的每个属性节点，都是 ref() 类型的响应式数据。
``` javascript
import { ref, reactive, toRefs } from "vue";

export default {
  //   name: "ReactiveTest",
  //   created() {},
  //   beforeCreate() {},
  setup() {
    // 创建响应式数据对象 refNum，初始值为 0
    const refNum = ref(0);
    // 如果要访问 ref() 创建出来的响应式数据对象的值，必须通过 .value 属性才可以，只有在setup内部才需要 .value 属性
    console.log(refNum.value); // 输出 0
    // 让 refNum 的值 +1
    refNum.value++;
    // 再次打印 refNum 的值
    console.log(refNum.value); // 输出 1
    
    const refC1 = ref(0);
    console.log(isRef(refC1)); // isRef判断是否为ref创建

    // 创建响应式数据对象，得到的 state 类似于 vue 2.x 中 data() 返回的响应式对象
    const state = reactive({
      refNum, // 当把 ref() 创建出来的响应式数据对象，挂载到 reactive() 上时，会自动把响应式数据对象展开为原始的值
      count: 0,
      age: [
        {
          ageNumber: 1
        }
      ]
    });
    state.count += 1;
    console.log(state);

     // 旧的ref会被替换为新的ref
    const refC2 = ref(9);
    // state.refC1 = refC2; // 会报错 但是这里refC1会被替换为refC1
    state.refC1 = refC2.value;
    state.refC1++;
    console.log(state.refC1);
    console.log(refC2.value);
    console.log(refC1.value);



    // setup 函数中将响应式数据对象 return 出去，供 template 使用
    // 这样对象的写法就需要toRefs来转换state
    return {
      refNum,
      ...state, // 非响应式数据
      ...toRefs(state) // 响应式数据
    };
  }
};
```
####  computed 计算属性
``` javascript
 setup() {
    // 只读计算属性
    const refNum = ref(0);
    let conputedCount = computed(() => refNum.value + 1);
    return {
      refNum,
      conputedCount
    };

    // 可读可写
    const refNum = ref(0);
    let conputedCount = computed({
      // 取值函数
      get: () => refNum.value + 1,
      // 赋值函数
      set: () => {
        refNum.value = refNum.value + 1;
      }
    });
    // 为计算属性赋值
    conputedCount.value = 0;
    return {
      refNum,
      conputedCount
    };
  }
```
####  watch 监视
```javascript
 import { watch, reactive, toRefs, ref } from "vue";

 setup() {
    //watch() 函数用来监视某些数据项的变化，从而触发某些特定的操作
    //watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })

    // // 单个ref监视--------------------
    const refCount = ref(0);
    // //refCount发生变化就会触发watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })
    watch(() => console.log(refCount.value), { lazy: false });
    setInterval(() => {
      refCount.value += 1;
    }, 5000);
    return {
      refCount
    };

    // // 监视多个ref---------------------------
    const refCount1 = ref(0);
    const refCount2 = ref(0);
    // //refCount发生变化就会触发watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })
    watch(
      [refCount1, refCount2],
      ([NewrefCount1, OldrefCount1], [NewrefCount2, OldrefCount2]) => {
        console.log(NewrefCount1, OldrefCount1);
        console.log(NewrefCount2, OldrefCount2);
      },
      { lazy: false }
    );
    setInterval(() => {
      refCount1.value += 1;
      refCount2.value -= 1;
    }, 5000);
    return {
      refCount1,
      refCount2
    };

    // // 单个reactive 监视-----------------------------
    const state = reactive({
      user: {
        age: 0
      }
    });
    watch(
      () => state.user.age,
      (newVal, oldVal) => {
        console.log(newVal);
        console.log(oldVal);
      },
      { lazy: true }
    );
    setInterval(() => {
      state.user.age += 1;
    }, 2000);
    return state;

    // // 多个reactive 监视-----------------------------
    const state = reactive({
      user: {
        age: 0
      },
      getNum: {
        number: 0
      }
    });
    watch(
      [() => state.user.age, () => state.getNum.number],
      ([newVal, oldVal], [getNumNew, getNumOld]) => {
        console.log(newVal);
        console.log(oldVal);
        console.log(getNumNew);
        console.log(getNumOld);
      },
      { lazy: true }
    );
    setInterval(() => {
      state.user.age += 1;
      state.getNum.number += 1;
    }, 2000);
    return state;
  }
```
清除监视
``` javascript

<button @click="stopWatch">清除监听</button>

import { watch, reactive, toRefs } from "vue";
//在 setup() 函数内创建的 watch 监视，会在当前组件被销毁的时候自动停止。如果想要明确地停止某个监视，可以调用 watch() 函数的返回值即可
  setup() {
 // 多个reactive 监视-----------------------------
    const state = reactive({
      user: {
        age: 0
      },
      getNum: {
        number: 0
      }
    });
    const stop = watch(
      [() => state.user.age, () => state.getNum.number],
      ([newVal, oldVal], [getNumNew, getNumOld]) => {
        console.log(newVal);
        console.log(oldVal);
        console.log(getNumNew);
        console.log(getNumOld);
      },
      { lazy: false }
    );
    setInterval(() => {
      state.user.age =state.user.age+ 1;
      state.getNum.number =state.getNum.number+ 1;
    }, 2000);

    const stopWatch = () => {
      console.log("停止监听");
      stop();
    };
    return {
      stopWatch,
      ...toRefs(state)
    };
  }
```
在watch中清除无效的异步任务
``` javascript
 import { watch, ref, reactive } from "@vue/composition-api";

export default {
  setup() {
    // 定义响应式数据 keywords
    const keywords = ref("");

    // 异步任务：打印用户输入的关键词
    const asyncPrint = val => {
      // 延时 1 秒后打印
      return setTimeout(() => {
        console.log(val);
      }, 1000);
    };

    // 定义 watch 监听
    watch(
      keywords,
      (keywords, prevKeywords, onCleanup) => {
        // 执行异步任务，并得到关闭异步任务的 timerId
        const timerId = asyncPrint(keywords);
        // 如果 watch 监听被重复执行了，则会先清除上次未完成的异步任务
        onCleanup(() => clearTimeout(timerId));
      },
      // watch 刚被创建的时候不执行
      { lazy: true }
    );

    // 把 template 中需要的数据 return 出去
    return {
      keywords
    };
  }
};
```
