## Context 解析

### Stage模式和FA模式下获取Context
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

在 ets 文件（非页面）中获取 Contex
```ts
    // getContext 获取的是当前 hap 的，一个app 可能存在多个 hap，取决于当前执行逻辑在哪个 hap 里 
    let context = getContext();

    // applicationContext 只有一个
    let appContext = getContext().getApplicationContext();
```
