
订阅管理 https://github.com/gooaclok819/sublinkX

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


1. clash_bohan.yaml（兼容简洁版）

特点：

核心配置最简洁，注释清晰，便于初学者理解。

支持 机场订阅自动更新、测速、故障转移、手动选择三类代理分组。

规则引用较为基础，覆盖直连 / 国外流量 / 国内流量 / 流媒体 / 游戏。

适合人群：

新手入门，想快速上手，先跑起来。

对 DNS、嗅探等高级功能要求不高。

2. clash_bohan1.yaml（标准进阶版）

特点：

在简洁版基础上，增加了 DNS 设置（DoH、国内 DNS、nameserver-policy）和 嗅探器（自动识别流媒体域名）。

增加 Geo 数据库自动更新，提升规则精确度。

默认端口更多（mixed/socks/redir/tproxy），适配多种场景。

适合人群：

已经理解基础 Clash 配置，想要 更稳定和更精准的分流。

需要国内/国际 DNS 区分，避免 DNS 污染。

3. clash_bohan2.yaml（高级优化版）

特点：

配置最复杂，几乎开启了 所有 Clash 高级功能：

sniffer 全面嗅探（TLS/HTTP 强化）。

DNS 策略更精细（针对淘宝、京东、QQ 等域名单独分配 DNS）。

lazy 检测、tolerance 容差 → 减少频繁测速带来的资源消耗。

unified-delay / tcp-concurrent → 提高延迟体验。

注重性能和兼容性，适合对网络体验要求高的人。

适合人群：

熟悉 Clash 机制，希望获得 接近生产环境级别的优化。

对 DNS 分流、低延迟和多设备兼容有高要求。

对比总结
模板	               复杂度	        功能覆盖	             稳定性	       适合人群
clash_bohan.yaml	   ★☆☆（简单）	基础分流	             一般	         入门学习、先跑通
clash_bohan1.yaml	   ★★☆（中等）	分流 + DNS + 嗅探	   较高	         进阶使用，追求稳定
clash_bohan2.yaml	   ★★★（高级）	全功能优化	           最高	         老手/对性能和精细化有要求
