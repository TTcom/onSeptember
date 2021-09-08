-  Vue 创建实例过程中，会去处理各种选项，如果选项中包含computed则会通过initComputed来处理
### initComputed
```js
function initComputed(vm, computed) {    

    var watchers = vm._computedWatchers = 

            Object.create(null);    

    for (var key in computed) {        

        var userDef = computed[key];        

        var getter = 

            typeof userDef === 'function' ? 

                userDef: userDef.get;      

        // 每个 computed 都创建一个 watcher

        // watcher 用来存储计算值，判断是否需要重新计算

        watchers[key] = 

        new Watcher(vm, getter, { 

             lazy: true 

        });        
        // 判断是否有重名的属性

        if (! (key in vm)) {
            defineComputed(vm, key, userDef);
        }
    }
}
```
### initComputed 这段代码做了几件事

- 1、每个 computed 配发 watcher

- 2、defineComputed 处理

- 3、收集所有 computed 的 watcher
computed 创建watcher对象是传递的参数
- new Watcher(vm, getter, { lazy: true })
- computed 新建 watcher 的时候，传入 lazy，并把lazy 赋值给了 dirty，lazy 表示一种固定描述，不可改变，表示这个 watcher 需要缓存
### 缓存控制
```js
if (watcher.dirty) {       
    watcher.evaluate()
} 
```
- watcher.evaluate 用来重新计算，更新缓存值，并重置 dirty 为false，表示缓存已更新
```js 
Watcher.prototype.evaluate = function() {    
    this.value = this.get();    
    // 执行完更新函数之后，立即重置标志位
    this.dirty = false;
};
```
- 所有说通过 控制 dirty 从而控制缓存，但是怎么控制dirty 呢？

- 先说一个设定，computed数据A 引用了 data数据B，即A 依赖 B，所以B 会收集到 A 的 watcher

- 当 B 改变的时候，会通知 A 进行更新，即调用 A-watcher.update，看下源码
```js
Watcher.prototype.update = function() {    
    if (this.lazy)  this.dirty = true;
};
```
- 当通知 computed 更新的时候，就只是 把 dirty 设置为 true，从而 读取 comptued 时，便会调用 evalute 重新计算








