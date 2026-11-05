# TVS 订阅源 / TVS (TVBox-tvs) subscription

## 订阅地址（TVS 订阅页填这个）
```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/tvs.json
```
备用（jsdelivr 挂时）：
```
https://gh-proxy.com/https://raw.githubusercontent.com/daletyler1737/tvs-source/main/tvs.json
```

## 内容
- 点播：8 个实测可播的 CMS 采集站 + 227 个 drpy JS 脚本站（需 TVS 内嵌 spider，已指向 gao 的 drpy2.min.js）
- 直播：303 个实测存活频道（M3U 格式，含分组与台标）

## 直播源单独地址
```
https://cdn.jsdelivr.net/gh/daletyler1737/tvs-source@main/live.m3u
```
（TVS 直播页填这个，和点播订阅是两套）

## 说明
- TVS 是空壳，只解析羊壳(PeekPeek)结构：sites/spider/lives/parses/flags
- JS 站依赖 drpy2.min.js（已托管在 gao 仓库的 jsdelivr），不依赖本地 jar
- 源会腐烂，失效后重跑 `probe_tvs2.py` + `build_tvs2.py`
