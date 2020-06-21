

### 宏任务与微任务
  >>> 宏任务
    script代码段、setTimeout、setInterval、Promise的构造函数、setImmediate、I/O
  >>> 微任务
    process.nextTick和Promise

  >>>>> tips: 在当前的微任务没有执行完成时，是不会执行下一个宏任务的

  ## 1. setTimeout设置为0的作用
    setTimeout为宏任务 不管设置延迟为多少 都会进入任务队列