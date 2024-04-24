## Promise 处理异步操作
Promise 有两个重要方法：Executor 和 then
### Executor 函数

```ts
/**
 * Creates a new Promise.
 */
 new <T>(executor: (resolve: (value: T | PromiseLike<T>) => void, reject: (reason?: any) => void) => void): Promise<T>;
```
executor 是创建 Promise 对象时的参数。这个函数是同步执行的，即在 Promise 构造函数返回 Promise 对象之前执行。
executor 接收两个函数式参数：resolve reject

resolve：当异步操作成功完成时，你应该调用这个函数，并将操作的结果值作为参数传递。这会将 Promise 的状态从 "pending"（进行中）更改为 "fulfilled"（已完成）。

reject：如果异步操作失败，你应该调用这个函数，并将错误或失败的原因作为参数传递。这会将 Promise 的状态从 "pending"（进行中）更改为 "rejected"（已失败）。

### then 函数
then 方法是 Promise 对象上的一个方法，用于指定当 Promise 完成（fulfilled）或失败（rejected）时应该执行的操作。then 方法接收两个可选参数，都是函数：第一个是 Promise 完成时的回调函数，第二个（可选的）是 Promise 失败时的回调函数。

完成回调：当 Promise 的状态变为 "fulfilled" 时，这个函数会被调用，其参数是 resolve 函数传递的值。

失败回调：当 Promise 的状态变为 "rejected" 时，这个函数会被调用，其参数是 reject 函数传递的值。
