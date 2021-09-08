### 判断类型有哪些方式
### vue computed的缓存机制是如何实现的
1、其缓存机制本质是通过一个dirty属性控制的，只有dirty为true时才会重新计算结果替换缓存。
2、dirty只有当其响应式数据发送变化时才会设置为true，重新计算后会再次被设置为false
- 参考网站https://blog.csdn.net/SJ1551/article/details/109804232?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control
- vue源码解读：https://zhuanlan.zhihu.com/p/62732142
### eventloop
### promise async await原理
### for in 和 for of的区别
### vue3和vue2的区别
### http缓存
- http缓存主要分为两种，一种是强缓存，一种是协商缓存
- 强缓存：如果缓存服务器存在缓存的数据的话，客户端会直接向缓存服务器读取数据来使用
- 协商缓存：又称对比缓存，客户端首先会向缓存服务器获取缓存标识，然后再携带标识向服务端发送请求获取标识是否有效，如果有效则会返回304，然后向缓存服务器获取数据，如果无效服务端则返回新的数据