# TVS 订阅源（猫影视 Node.js 订阅包）

TVS(TVBox-tvs) 只解析**猫影视兼容的 Node.js 订阅包**。本仓库提供一份裁剪过的：
从上游 96 个内置源里实测剔除 32 个死站，保留 **64 个可用源**。

## 订阅地址（TVS「订阅」页填这个）

```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/cat/index.js.md5
```

局域网备用（同一 Wi-Fi 下最稳，不走公网）：
```
http://192.168.1.127:3010/dale003/tvs-source/raw/branch/main/cat/index.js.md5
```

## 内容
- 64 个点播源，全部实测通过 home/category/detail 三级（能出片单、能拿播放地址）
- 覆盖：4K 影视 / 秒播 / 采集 / 短剧 / 漫剧 / 动漫 / 听书 / 少儿 / 中小学课堂 / 音乐 / 体育 / 虎牙斗鱼B站直播
- 已剔除：duoduo、huban、qwmkv、pianku、woniu4k、pan123ziyuan、ikanbot、yiyangshi、appv7xianyu、
  appv7xiaoningmeng、appv7xiaoshizi、push、sokaka、soaiqupanshe、soaihaiyin、soaipansoo

## 直播源（另一套，走直播页导入）
```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/live.m3u
```

## 维护
上游改版后重跑：`probe2.js`（三级探活）→ `build` → 生成 md5 → push
md5 必须与实际 index.js 完全一致，否则 App 拒绝加载。
