# 2026 Gemini 4 Hydrogen 国内怎么用上：免费额度怎么吃、三档订阅谁有手动选择权

> 📍 本文首发于 **[AI与流媒体会员指南](https://ai.fanqiangdao.com/hot/gemini-4-hydrogen/)**，持续更新以原站为准。


11 月 12 日，Google 把 Gemini 4 一次性推到了所有人面前，代号 Hydrogen。名字换了，定位也换了：它不是又一个旗舰模型，而是把旗舰的脑子装进执行层——官方给的数字是默认档智能指数 51，比 Argon 的 50 还高一点，最高档 xhigh 到 54；跑 Terminal-Bench 4.1 拿到 57%，而它替掉的那代 Flash 只有 18.2%，速度快 2.5 倍。

对国内用户来说，真正要弄清的是两件事：哪里能白用，哪里必须付费才能在模型选择器里点名它。这两件事经常被混成一件，结果就是一篇文章读完，人以为「免费就能用上」，装好 App 才发现选择器里根本没这个选项。

下面的顺序照着走：先看它是什么、再看各档位的真实差别、然后算 12 月 1 日之前该把哪一层换掉、最后才是账号与网络这两道硬门槛。

## Gemini 4 Hydrogen 的定位：执行层，不是主力脑子

Google 这一代把命名改了，Hydrogen 直接接的 3.8 Flash，但官方说法里它不再是「轻量版」，而是「日常工作和 agent 工作流的快速执行模型」。翻译成人话：规划、架构判断、疑难 bug 归 Carbon 和 Argon，写代码、跑测试、验证改动这些高频动作归 Hydrogen。

几个能拿来判断的硬指标：

- 上下文 100 万 token，输出最长也给到 100 万 token，长文档、整仓代码、会议录音这类输入不用先切片。
- 四档思考深度：low、medium、high（默认）、xhigh。xhigh 是新加的一档，官方在它上面报了 54 分。
- 官方口径里，「编造性表述」比 3.8 Flash 少了 5 倍以上，工具调用失败时会改路子而不是硬编。
- 在 Antigravity 里还有一个叫 Orchestrator 的组合档：Carbon 负责规划和返工，Hydrogen 负责执行，同一个会话里自动来回切。官方在 Terminal-Bench 4.0 上报的是接近纯 Carbon 的成功率，同时省 24% 配额、快 19%。

从 3.8 Flash 迁过来的人会撞上两个变化：模型 ID 换成 gemini-4-hydrogen，思考深度从原来的单一档变成四档可选（low、medium、high、xhigh）。官方文档里给了一份迁移清单，代码侧要改的就这两处，真正要重新调的是 prompt——同一句提示词在 high 和 xhigh 下的等待时间差得明显，批量任务里建议先按 medium 跑一轮，把必须深想的几步单独提到 xhigh。

我认为这个组合档才是这一代最有意思的部分。过去想省钱只能整条任务走小模型，一旦卡住就得人手动换；现在切换交给它自己判断，省下来的不是单价，是来回折腾的时间。

## 谁能拿到 Hydrogen：一张表看清档位

这是最容易搞错的地方。同一句「Hydrogen 已上线」，在不同入口的含义完全不同。

| 入口 | 免费用户 | AI Plus | AI Pro | Ultra |
| --- | --- | --- | --- | --- |
| Gemini 应用 | 只在 Auto 自动路由命中时用上，选择器里没有这一项 | 可手动选择，额度约为免费档 2 倍 | 可手动选择，额度约 4 倍，另有 Argon | 最高额度，含 Carbon |
| Google 搜索 | 全体用户，作为默认模型之一 | 同左 | 同左 | 同左 |
| Gemini in Sheets | 无 | 无 | 有 | 有 |
| Antigravity | 无 | 无 | 有 Hydrogen；Orchestrator 只有 Argon 版 | 有 Hydrogen；Orchestrator 有 Carbon 版与 Argon 版 |
| Gemini API / AI Studio | 有，免费但限速 | — | — | — |
| Google Antigravity 内的 Carbon | 无 | 无 | 无 | 有 |

表里有两处细节值得单独说。

一是 Gemini 应用那条。官方博客的脚注写得很明确：免费用户在应用里是通过 auto 模型选择「在合适的时候」拿到 Hydrogen，模型选择器里不会出现它。免费档在选择器里能看到的是 Flash-Lite 这一档。所以「Google 说对所有人开放」这句话没错，但对免费号来说，开放的是「被分配」，不是「被选择」。

二是 Orchestrator 的档位。Antigravity 官方博客的原话是：Hydrogen 向付费的 AI Pro 与 Ultra 订阅者开放；Orchestrator 以 Orchestrator (Carbon) 和 Orchestrator (Argon) 两种形式上 Ultra，付费 AI Pro 只拿到 Orchestrator (Argon)。想要「Carbon 规划 + Hydrogen 执行」这个组合，Pro 是不够的。

## 12 月 1 日之前，该把哪一层换掉

Google 这次把价目表摊得很平：Hydrogen 在整条 100 万上下文里都是同一个价，每百万输入 $1.50、输出 $7.50，缓存命中再打 95 折（以官网价页为准）。也就是说，长上下文不再按长度加价，这一条对长文档类工作流的成本影响比单价本身更大。

Carbon 那边是另一套写法：每百万输入 $2、输出 $10，但这是介绍价，官网价页写明 11 月 30 日截止，12 月 1 日起变成 $4 和 $20，缓存从 $0.10 涨到 $0.20（以官网价页为准）。Argon 同价同节奏。另外 Carbon 不在免费层里，每一个 token 都计费，思考 token 也算输出。

把这三组数字代进一个具体任务就很清楚。假设一次 agent 任务输入 20 万 token、输出 4 万 token：

- 全走 Carbon 介绍价：0.2 × 2 + 0.04 × 10 = $0.8，单价以官网价页为准。
- 全走 Hydrogen：0.2 × 1.5 + 0.04 × 7.5 = $0.6，单价以官网价页为准。
- 12 月 1 日之后全走 Carbon：0.2 × 4 + 0.04 × 20 = $1.6，单价以官网价页为准。

同一个任务，钱翻了一倍，而执行质量并不需要每次都上旗舰。所以我的建议很直接：把流水线拆成「规划层 + 执行层」，规划层留给 Carbon 或 Argon，执行层换 Hydrogen。省下来的比例取决于你的 token 结构，执行占比越高省得越多，跑批量测试、批量改文件的场景差距最大。

反过来说，如果你的活是「一次想清楚，输出一份长报告」，全流程都是规划，那 Hydrogen 的性价比就没那么突出，不必为了省钱硬换。

## 第一步：账号和网络，这道关比订阅难

Gemini 的地区口径跟 ChatGPT 那套不一样，但同样硬。三条经验值得先记住。

香港、澳门不在服务范围内，节点挂过去打开 Gemini 会直接提示地区不可用，这不是风控误判，是名单问题，没有变通空间。账号的订阅资格跟 Google Play 的国家绑定，注册时选了哪个区、历史支付在哪个区，决定你能在哪个区下单，改区有 12 个月冷却期，比换号贵。支付那一刻风控最紧，节点在你的订阅周期内漂到另一个国家，支付页报错、订阅被暂停都出现过。

所以节点只按三个词挑：原生、固定、干净。原生指 IP 注册地就是使用地，不是别处的段广播过来；固定指锁一两个节点别天天漂；干净指这条出口没有滥用历史，这一项自己验不了，只能靠线路质量兜底。机房 IP 段是最容易被判定异常的那一类，这类服务对 IP 挑剔程度不低。

预算紧的按这个顺序试：

[一枝红杏](https://tochick.xyz/16?site=12hao)走年付锁价，Trojan Lite 年付 99 元、每月 100G、限 5 台设备，1000 Mbps，全球多线路可选。文本对话和代码补全的流量消耗很低，一天几小时也吃不满 100G。设备多、想一步到位看 Trojan Pro，年付 499 元、每月 500G、不限设备数。

对出口质量有要求的看 [SS-ID](https://tochick.xyz/19?site=12hao)，IEPL 专线加速，1000 Mbps，套餐页明确标了 ChatGPT 等 AI 服务的解锁保证，100G 月付 20 元起。专线出口的 IP 质量通常比普通中转稳，对这类按 IP 归属做判断的服务，先买一个月验证比一上来年付稳妥。

只想花一杯奶茶钱先确认能不能连上的，[瑶瑶领先](https://tochick.xyz/18?site=12hao) 月付 9.9 元给 384G、3 台设备，线路的实时在用人数是公开的，挑人少的线固定挂着就行。

再往上一档是 [扬帆云](https://tochick.xyz/59?site=12hao)，LV2 29.99 元 200GB、LV3 39.99 元 400GB 起走部分 IEPL，LV4 49.99 元 700GB 全专线，适合白天要开视频会、晚上还要跑 agent 的人。

验收标准很具体：挂上节点，打开 Gemini 能正常登录、能选中模型、不弹地区提示，再谈付款。连登录都过不去，先换线路，别急着怀疑账号。

## 第二步：订阅怎么买，三条路线摆在一起

| 路线 | 价格 | 拿到什么 | 适合谁 |
| --- | --- | --- | --- |
| 官方 AI Plus | 按月订阅，价格与可用国家以官方定价页为准 | Gemini 应用里手动选 Hydrogen，额度约 2 倍 | 只在 App 里用、不上 Antigravity 的人 |
| 官方 AI Pro | 按月订阅，以官方定价页为准 | 4 倍额度 + Argon + Antigravity 里的 Hydrogen 与 Argon 版 Orchestrator + Sheets 入口 | 要跑 Antigravity 的开发者 |
| 官方 Ultra | 最贵一档，以官方定价页为准 | 加上 Carbon 与 Carbon 版 Orchestrator | 长期跑高难度 agent 的团队 |
| 银河录像局 | Gemini Advanced ¥44.1/月（券后，月付） | 代充交付的订阅，翻车包赔、独立子账户、支持同户验证 | 不想碰 Google Play 支付的人 |
| 银河录像局 | Gemini API ¥19.5（20 美元额度档） | 按额度调 API，不包月 | 写脚本、跑批处理的人 |
| 飞行派 | 无 Gemini 车位 | AI 线是 ChatGPT 拼车 ¥49.99/月、Claude ¥169/月 | 同时要配 ChatGPT 或 Claude 的人 |

这里有个必须说清的硬事实：飞行派**没有 Gemini 车位**，它家的 AI 线是 ChatGPT 和 Claude，Gemini 这条想走代充只有银河录像局。反过来，银河录像局也没有 Claude Pro 订阅车位，跟 Claude 沾边的只有 Claude Code 的 API 额度包。两边各有各的货，不要拿一家的价目去套另一家。

[银河录像局官方入口（优惠码 haiwan）](https://tochick.xyz/60)银河录像局那条「Gemini Advanced」档位，官网商品名写的是 GeminiPro，按 AI Pro 这一档理解基本不会错。¥44.1/月是券后月付价，结算时填优惠码 haiwan，最终折扣随产品不同，以结算页实示为准。独立子账户这一项在这种场景里挺值钱：你拿到的是自己的登录入口，不是几个人传一串账号密码，IP 与登录轨迹混在一起的概率低很多。

[飞行派官方入口](https://tochick.xyz/62)飞行派这边更适合「顺手配齐」的人。它没有 Gemini，但 ChatGPT 拼车 ¥49.99/月、Claude 合租 ¥169/月都是明码标价，一次下单把几个模型的预算放一个购物车，售后也只找一家。

如果你的用法是跑脚本、批量处理，API 路线往往比订阅划算。银河那个 ¥19.5 的 20 美元额度包，配合 Hydrogen 的免费层先做验证：免费层限速但额度不要钱，够你把 prompt 调到满意；调通了再充额度跑量。有一条要提前想清楚——官方价页写明免费层的调用结果会用于改进产品，付费层不会。客户数据、未公开的代码，别在免费层试。

## 避坑清单

- **「对所有人开放」不等于「免费能选」。** 免费号在 Gemini 应用里只能等 Auto 分配，选择器里没有 Hydrogen。要手动点名，最低档是 AI Plus。
- **想要 Carbon 版 Orchestrator，别买 Pro。** Pro 只给 Argon 版，Carbon 版在 Ultra。
- **免费层别放敏感数据。** 官方写明免费层结果会用于改进产品，付费层不会。这条比省几块钱重要。
- **别拿旧名当新档买。** 货架上写「Gemini Advanced」的是旧称，实际对应 AI Pro 那一档；AI Plus 更便宜但没有 Argon 和 Antigravity。
- **Ultra 别冲动。** 除非你天天跑长链路 agent，多出来的 Carbon 与配额吃不满，就是纯加钱。
- **节点别跨区漂。** 付款用哪个区，日常就固定在哪个区，订阅中途频繁换国家登录是被要求重新验证的常见诱因。
- **香港、澳门节点直接排除。** 不在服务名单里，不是风控，是硬封锁，试也没用。
- **API 额度包不是订阅。** 它买的是调用额度，不给你 App 里的会员权益，也不进 Antigravity。

## FAQ

### Gemini 4 Hydrogen 免费能用吗？

分入口看。Gemini API 和 AI Studio 的免费层能用，免费但限速；Gemini 应用里免费号只能在 Auto 自动路由命中时用上，选择器里选不到；Antigravity 里的 Hydrogen 要付费的 AI Pro 或 Ultra。所以「免费能用」这句话在三个地方有三种答案。

### 国内想用上 Gemini 4 Hydrogen，最快的方式是什么？

两条路。想省事就走代充订阅，银河录像局的 Gemini Advanced ¥44.1/月，拿到 App 里手动选模型的权限；想按量就走 API，先吃官方免费层的额度把流程跑通，不够再充额度包。两条路都要先解决网络：原生、固定、干净的出口，香港澳门节点直接排除。

### AI Plus、AI Pro、Ultra，手动选 Hydrogen 要哪一档？

AI Plus 起就能在 Gemini 应用里手动选 Hydrogen。要用 Antigravity，得 AI Pro，Pro 还给 Argon 和 Antigravity 里的 Hydrogen；Orchestrator 想用 Carbon 版，只有 Ultra。按「你在哪用」选，不按价格选。

### 12 月 1 日的涨价会影响 Hydrogen 吗？

不会。涨的是 Carbon 和 Argon：输入从每百万 $2 到 $4，输出从 $10 到 $20，缓存从 $0.10 到 $0.20（以官网价页为准），12 月 1 日起生效。Hydrogen 在 100 万上下文内保持 $1.50 与 $7.50 的平价。这也是我建议把执行层换到 Hydrogen 的现实理由。

### Antigravity 里的 Orchestrator 值得为它升档吗？

看你的活是不是「规划难、执行多」。官方给的对比是接近纯 Carbon 的任务成功率，同时省 24% 配额、快 19%。天天写新功能、改架构的，升档有意义；主要做小修小补的，Hydrogen 单模型就够，不必为了一个组合档加钱。

### 代充拿到的 Gemini Advanced，和官网订阅有差别吗？

权益上是同一条订阅线，差别在交付方式和归属。代充交付的是订阅结果，账号可能是升级你的号，也可能是给你一个新号；新号一定要问清辅助邮箱和找回方式，不然哪天密码失效，号就找不回来。下单前问三件事：交付的是升级还是新号、掉订阅怎么赔、几个工作日内完成。

## 收尾：两步闭环，按顺序走

先定档位，再配网络，最后才付钱。只在 App 里用、要手动选 Hydrogen 的，AI Plus 就够；要进 Antigravity 跑 agent 的，直接 AI Pro；要把执行层批量换成 Hydrogen 的，先走 API 免费层验证，通了再充额度。这是我一贯的顺序，因为网络和账号的问题在前两步暴露，比付完钱再排查省事得多。

网络这侧，年付锁价看[一枝红杏](https://tochick.xyz/16?site=12hao)，要专线看 [SS-ID](https://tochick.xyz/19?site=12hao)，小额验证看[瑶瑶领先](https://tochick.xyz/18?site=12hao)，要全专线又常开会的看[扬帆云](https://tochick.xyz/59?site=12hao)，四家都带 12hao 归因入口，先月付再年付是我的老规矩。会员这侧，[银河录像局](https://tochick.xyz/60)的 Gemini 档 ¥44.1/月，优惠码 haiwan，其他品类以平台实时标价为准；[飞行派](https://tochick.xyz/62)没有 Gemini，要配 ChatGPT 或 Claude 再从它走。

站内还有几篇可以接着看：[Gemini Advanced 开通教程](https://ai.fanqiangdao.com/solutions/gemini-advanced/)讲的是 Google One 那条老订阅线的支付细节，[Gemini Omni 1.2 Flash](https://ai.fanqiangdao.com/hot/gemini-omni-1-2-flash/) 是上一代多模态模型的用法，[ChatGPT Plus 国内订阅](https://ai.fanqiangdao.com/solutions/chatgpt-plus/)和 [Claude Pro 指南](https://ai.fanqiangdao.com/solutions/claude-pro/)适合做横向比较，[机场推荐聚合页](https://ai.fanqiangdao.com/proxy/)按线路类型和预算排好了。

我的判断是：这一代真正的变化不在榜单分数，而在价格结构——旗舰继续涨价，执行层保持平价，中间那条缝就是大多数人的省钱空间。趁 12 月 1 日之前把流水线拆开，比涨价之后再改要省一轮返工。
