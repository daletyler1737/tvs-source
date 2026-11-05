# TVS 订阅源（猫影视 Node.js 订阅包 · 64 个实测可用源）

TVS(TVBox-tvs) 只解析**猫影视兼容的 Node.js 订阅包**，不认 TVBox JSON。
本包基于上游 96 个内置源，三级探活后**剔除 32 个死站，保留 64 个可用**。

## 订阅地址（TVS「订阅」页填这个，国内直连不用代理）

**主**（jsDelivr，实测 200 / 2.8s / md5 一致）
```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/cat/index.js
```

**备 1**（带 md5 自动校验）
```
https://gh-proxy.com/https://raw.githubusercontent.com/daletyler1737/tvs-source/main/cat/index.js.md5
```

**备 2**（局域网 Forgejo，同 Wi-Fi 0.6s）
```
http://192.168.1.127:3010/dale003/tvs-source/raw/branch/main/cat/index.js.md5
```

## 保留的 64 个源（home→category→detail 三级全过）

- **4K**：玩偶 / 木偶 / 快映 / 闪电 / 蜡笔 / 花卷 / 立播 / 原盘 / 剧透 / 移动
- **秒播**：韩剧 / 瓜子 / 独播 / 悦悦 / 文采 / 师兄 / 粉猪 / 追剧 / 柚子 / 柠檬 / 太奇 / 零七 / 黄人 / 枫叶4K / 热播 / 波波
- **采集**：天堂
- **短剧漫剧**：小龙 / 小猫 / 小红 / 小喜 / 小马 / 星芽 / 好看 / 短剧小猫 / 小薇
- **动漫**：共和 / 花子 / 番剧 / 西番
- **直播**：虎牙 / 哔哩 / 斗鱼
- **听书**：爱阅听 / 河马 / 红果
- **少儿**：兔兔 / 宝宝爱看 / 贝瓦
- **课堂**：少儿教育 / 小学 / 初中 / 高中
- **音乐**：唱听 / 糖豆 / 爱音乐 / 网易云 / 酷我 / 酷狗
- **体育**：瓜子 / 咖啡 / 飞球 / 看球通 / WWE
- **B站**：影视 / 戏曲 / 演唱会 / 哔哩哔哩
- **元数据**：豆瓣 / 更新日历 / 配置中心 / 我的网盘

## 已剔除的 32 个（实测失效）

duoduo · huban · qwmkv · pianku · woniu4k · pan123ziyuan · ikanbot · yiyingshi ·
appv7xianyu · appv7xiaoningmeng · appv7xiaoshizi · push · sokaka ·
soaiqupanshe · soaihaiyin · soaipansoo · manjuhongguo · guanying · mypan ·
animehuazi · animemodu · musicailunhui · musicaikuwo · musicai163 ·
sportaiguazi · sportaikanqiu · livetovod · baseset · gengxin · douban(仅元数据) ·
fake115share · duanjuqimiao(部分)

## 直播源（另一套，走 TVS 直播页导入，不在订阅框）

```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/live.m3u
```
303 个实测存活频道，11 分组，全带台标。

## 实现方式

`cat/index.js` = 上游 bundle（6.6 MB，内嵌 CatVodSpider 全栈）+ 一行过滤：

```js
n = n.filter(z => GOOD.includes(z.meta.key));   // GOOD = 64 个实测通过的 key
```

spider 本体一字未动，只过滤注册表。上游改版后重跑探活脚本重新生成。

## 探活方法

本地 node 起 bundle（stub 两个宿主符号 `catServerFactory` / `catDartServerPort`），
对每个源打 `POST /spider/{key}/3/{home,category,detail}`，三级全过才算可用。

## 注意

- `.md5` 后缀 jsDelivr 不服务（403），只能走 gh-proxy / Forgejo
- 上游原版（96 源含死站）：`https://9280.kstore.vip/cat/index.js.md5`
