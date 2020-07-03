# Angular初始化APP_INITIALIZER

## APP_INITIALIZER

有时候我们需要在app渲染出界面之前,处理一些加载逻辑,比如登录,加载静态资源等等.

angular为我们提供了一个token,`APP_INITIALIZER`通过他我们可以注册初始化服务.必须使用`userFactory`方式,返回一个返回promise的函数,只有当promise结束padding的状态后,angular才会初始化完成开始页面渲染等等.

```ts
// 工厂函数
export const startupFactory = () => {
    console.log('我要初始化啦!')
}

//此处注册Provider
export const startUpProvider: Provider = {
  provide: APP_INITIALIZER,
  useFactory: startupFactory,
  deps: [], // 如果工厂函数需要其他服务的依赖,需要在此传入
  multi: true // 可以有多个初始化服务 都会被执行
};
```

## 相比于Vue

同样的业务场景,Vue作为渐进式框架,框架的初始化相对于Angular不会很复杂.只要在挂载前处理好相关

```js
const vm = new Vue()

async main() {
    await domesomething()
    console.log('我要初始化啦!')
    vm.$mount('#app')
}

main()

```

## 坑

在startUp服务的依赖注入过程中可能有部分服务由于Angular没有完成初始化而无法正常使用,例如`Router`等等...
