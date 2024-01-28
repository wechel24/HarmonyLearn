## sdk开发遇到问题汇总
### 1. ArkTS:ERROR Failed to get an resolved OhmUrl by filepath
#### 因为在hsp的ts代码中import c++代码路径不正确导致
在hsp中，包含了 c++ 和 ts 代码，ts 引用 c++ 代码时，必须是以 so 名称引入，而不能直接以 c++ 所在文件路径引入，
否则就会报错。
```java
import { sub, add } from '../../cpp/types/libqimei' // error
import { sub, add } from 'libqimei.so'  // correct
```
