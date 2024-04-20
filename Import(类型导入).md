## TS 中关于 import 遇到的问题
### 案例
### 1. ArkTS:ERROR Failed to get an resolved OhmUrl by filepath
#### 因为在har的ts代码中import c++代码路径不正确导致
在 har 中，包含了 c++ 和 ts 代码，ts 引用 c++ 代码时，必须是以 so 名称引入，而不能直接以 c++ 所在文件路径引入，
否则就会报错。
```ts
import { sub, add } from '../../cpp/types/libqimei' // error
import { sub, add } from 'libqimei.so'  // correct
```
### 2. 导入类识别不到
```ts
import HashMap from '@ohos.util.HashMap' // 正确
// import {HashMap} from '@ohos.util.HashMap' // 错误
```
#### import {xxx} 和 import xxx 区别
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

### export 和 export default 区别
1. 一个文件中，export default 只能出现一次，但是 export 可以多次
2. export default 好处就是在 import 时可以自定义名称并且无需使用 {} 进行接收
   而 export 则必须使用 {} 严格按照导出时候的名称按需接收

**export default示例**
```ts
// 导出
export default class DeviceInfo {
  private static instance: DeviceInfo = new DeviceInfo();
  private isInited: boolean = false;
  private _aaid: string = "";

  public static getInstance(): DeviceInfo {
    return DeviceInfo.instance;
  }

  public getOaid(): string {
    return this._oaid;
  }
}

// 导入
import X from '../systemInfo/DeviceId'
X.getInstance().getOaid();
```
**export 示例**
```ts
// 导出
export class DeviceB {
  public static getBId(){
    // ...
  }
}

// 导入
import {DeviceB} from '../systemInfo/DeviceId'
DeviceB.getBId();
```
