# TVS 订阅源（猫影视 Node.js 订阅包 · 38 个实测可播放源）

TVS 只认**猫影视兼容的 Node.js 订阅包**，不认 TVBox JSON。
上游 96 个源，逐级实测后剔除 58 个，保留 **38 个能直出播放直链的**。

## 订阅地址（TVS「订阅」页，国内直连不用代理）

**主 —— Gitee（实测 md5 200/5.4s，index.js 6.6MB/4.3s，md5 一致）**
```
https://gitee.com/dale003/tvs-source/raw/main/cat/index.js.md5
```

**备 —— GitHub 经 jsDelivr（实测 1.9s，但 jsDelivr 不服务 .md5 后缀）**
```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/cat/index.js
```

**备 —— 局域网 Forgejo（同 Wi-Fi 0.6s，最稳）**
```
http://192.168.1.127:3010/dale003/tvs-source/raw/branch/main/cat/index.js.md5
```

## 判定标准（比"首页有分类"严得多）

`home` → `category` → `detail` → **`play`**，四级全过且 play 返回 `parse:0` 的
`http` 直链（m3u8/mp4/mp3）才算可用。

上游原版 96 个源里：
- 16 个 home 就空返回
- 1 个 category 空
- 1 个 detail 空
- **24 个能出片单但 play 报错**（主要是 4K 类源走夸克网盘，未配 Cookie 就
  `还没有配置夸克 Cookie，请先去配置中心登录夸克`；B 站类需 Cookie）

## 保留的 38 个（全部实测直出直链）

| 类别 | 源 |
|---|---|
| 影视 | 立播 / 瓜子 / 天堂采集 / 文采 / 独播 / 热播 / 波波 / 韩剧秒播 / 枫叶4K / 移动4K |
| 秒播 | 大师兄 / 粉猪 / 追剧达人 / 柚子 / 太奇 / 零七 / 黄人 |
| 短剧漫剧 | 漫剧小猫 / 漫剧小喜 / 短漫小马 / 短剧星芽 / 短剧好看 / 短剧小猫 |
| 动漫 | 共和动漫 / 动漫次元城 / 动漫西番 |
| 直播 | 虎牙 / 哔哩直播 / 斗鱼 |
| 听书 | 爱阅听 / 河马听书 |
| 少儿 | 兔兔 / 宝宝爱看 |
| 音乐 | 爱梨园 / 蜻蜓FM / 糖豆 |
| 体育 | 看球通 / WWE |

## 已剔除（58 个，实测失效）

4K 类（夸克 Cookie 依赖）：玩偶/木偶/快映/闪电/蜡笔/花卷/剧透/原盘
B站类（Cookie 依赖）：B站影视/戏曲/演唱会/哔哩哔哩/番剧
其他失效：豆瓣/更新日历/配置中心/我的网盘/爱看采集/伊影/咸鱼/柠檬/柿子/
duoduo/huban/qwmkv/pianku/woniu4k/pan123ziyuan/ikanbot/manjuhongguo/guanying/
animehuazi/animemodu/musicailunhui/kuwo/163/sportaiguazi/sportaikanqiu/livetovod/
sportaikafei/sportaifeiqiu/bilixiqu/musicaiwy/musicaikg/musicaikuwoa/bookhongguo/
childrenaibeiwa/duanjuweiguan/少儿教育/小学课堂/初中课堂/高中教育

## 实现方式

上游 bundle（6.6MB，内嵌 CatVodSpider 全栈）+ 一行白名单过滤，
spider 本体一字未动，被过滤的源仍正常 init（只是不显示）：

```js
const __WL = ["libvio","guazi",...];           // 38 个实测 key
const __ok = k => __WL.indexOf(k) >= 0;
```

## 维护

`probe-play.js`（四级探活脚本）→ 改 `__WL` → 重算 md5 → 推 Gitee/GitHub/Forgejo。
md5 必须与实际 index.js 完全一致，否则 App 拒绝加载。
