## API9 升级到10及以上版本时，build.profile.json5 配置需要改动
涉及两个配置项："compileSdkVersion"、"compatibleSdkVersion"
```ts
// api9配置:
{
    "app": {
    "signingConfigs": [
      {
      //   ...
      }
    ],
      "compileSdkVersion": 9,
      "compatibleSdkVersion": 9,
      "products": [
      {
      "name": "default",
      "signingConfig": "default",
      }
    ]
  }  
}



// api10+配置：
{
    "app": {
    "signingConfigs": [
      {
      // ...   
      }
    ], 
   "products": [
    {
      "name": "default",
      "signingConfig": "default",
      "compileSdkVersion": "4.1.0(11)",
      "compatibleSdkVersion": "4.1.0(11)",
      "targetSdkVersion": "4.1.0(11)"
    }
  ]
  // ...   
  } 
}

```
## 参考
    https://cloud.tencent.com/developer/article/2373325
