## TS 中关于 import 遇到的问题
### 案例
```ts
import HashMap from '@ohos.util.HashMap' // 正确
// import {HashMap} from '@ohos.util.HashMap' // 错误
```
### import {xxx} 和 import xxx 区别
import {xxx} 用于导入命名导出(named export)成员。当一个模块有多个导出对象时使用
```ts
// moduleB.ts
export const name = "John";
export const age = 30;

// main.ts
import { name, age } from "./moduleB";
```
import xxx 用于导入默认导出(default export)成员。当一个模块只有一个导出对象，通常使用默认导出
```ts
export default HashMap;
```
因为 HashMap 使用默认导出，因此使用时需要 import xxx 方式导入。
