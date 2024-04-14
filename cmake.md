### cmake 配置的一些细节差异

#### set 文件路径
``` ts
// 只能设置相对当前 cmake 文件的相对路径，根目录识别不到

// 错误方式：
// SOURCE_ROOT_DIR: cpp 代码根目录
set (SOURCE_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(base_src_dir ${SOURCE_ROOT_DIR}/base/)

// 正确方式：
set(base_src_dir base/)
set(util_src_dir util/)
```

#### 引用字符串，不要加双引号
```ts
set(SRC_UTIL
    ${util_src_dir}/format_helper.cpp
    ${util_src_dir}/log.cpp
    ${util_src_dir}/napi_util.cpp
)
```
