## sdk开发遇到问题汇总
### 1. ArkTS:ERROR Failed to get an resolved OhmUrl by filepath
#### 因为在hsp的ts代码中import c++代码路径不正确导致
在hsp中，包含了 c++ 和 ts 代码，ts 引用 c++ 代码时，必须是以 so 名称引入，而不能直接以 c++ 所在文件路径引入，
否则就会报错。
```java
import { sub, add } from '../../cpp/types/libqimei' // error
import { sub, add } from 'libqimei.so'  // correct
```
### 2. Stage模式和FA模式下获取Context
#### FA 模式
Context模块提供了ability或application的上下文的能力，包括允许访问特定于应用程序的资源、请求和验证权限等。获取context方式如下代码所示：
```ts
import featureAbility from '@ohos.ability.featureAbility'
let context = featureAbility.getContext();
```
#### Stage 模式
在stage模型中，context提供了应用的一些基础信息，例如resourceManager（资源管理）、applicationInfo（当前应用信息）、dir（应用开发路径）、area（文件分区）等，以及应用的一些基本方法，例如createBundleContext()、getApplicationContext()等。

UIAbility组件和各种ExtensionAbility派生类组件都有各自不同的Context类。比较常用的有AbilityContext和在eTS页面中访问Context。

Stage模型下，每个Ability中都包含了一个Context属性。

在继承**Ability**的类中通过this.context就可以获取AbilityContext，从而操作Ability的方法(如startAbility、connectAbility等)
```ts
import Ability from '@ohos.application.Ability'

export default class MainAbility extends Ability {
    onCreate(want, launchParam) {
   let context = this.context;
    }
    onWindowStageCreate(windowStage) {
        let context = this.context;
    }
    ...
};
```

在 UIAbility 获取上下文，也是一样的方法。
```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        // 获取UIAbility实例的上下文
        let context = this.context;
        // ...
    }
}
```
在 eTS 页面中访问Context
```ts
import common from '@ohos.app.ability.common';

@Entry
@Component
struct Index {
  private context = getContext(this) as common.UIAbilityContext;

  startAbilityTest() {
    let want = {
      // Want参数信息
    };
    this.context.startAbility(want);
  }

  // 页面展示
  build() {
    // ...
  }
}
```
