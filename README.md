
订阅模版clash_bohan2.yaml
1. 节点管理智能化

模板里写的只是订阅 proxy-providers，实际节点由机场下发。

分组用了 url-test、fallback 等模式：

♻️ 自动选择：定时测速，自动挑延迟最低的节点。

🔁 故障转移：某个节点挂了会自动切到可用节点。

这就避免了用户频繁手动切换。

2. 规则分流智能化

模板引入了多个在线规则集（Global、China、Game、Media…）。

各类流量会自动按规则匹配走不同的分组：

国外网站 → 🌐 国外流量

国内站点 → 🏠 大陆流量

流媒体 → 🎬 国际流媒体

游戏 → 🎮 游戏平台

新域名/IP 被规则集维护者不断更新，你不用自己去维护一大堆规则。

3. DNS 智能化

开启 fake-ip 模式，保证代理转发正常。

配置了 nameserver-policy，不同域名走不同的 DNS（例如淘宝/支付宝强制走阿里 DNS）。

fallback-filter.geoip-code: CN：让境外域名优先用国外 DNS，境内域名优先用国内 DNS。

这样做能减少 DNS 污染、提升解析准确度。

4. 自动更新智能化

geo-auto-update: true → GeoIP/Geosite 数据库会自动更新。

rule-providers → 规则集每天拉取最新版本。

proxy-providers → 订阅每天自动更新节点。
→ 全套配置会自动保持最新，不用人工维护。
