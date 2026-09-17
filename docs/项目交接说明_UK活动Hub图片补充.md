# UK活动Hub Digest 项目交接说明

## 一、我们在做什么

给 Chizy 的英国社群网络(学生公寓/兴趣社群)做**offline活动情报收集与分发**的skill化流程,把散乱的英国本地活动信息整理成结构化表格,按"为什么有人会去"匹配到对应社群,而不是按活动格式分类。

流程分两条track:
- **Track A**:近7天周末活动digest
- **Track B**:未来30天"近期热门"活动digest(本轮主要工作)

## 二、用的skill

**`/mnt/skills/plugins/uk-events-hub-digest/SKILL.md`**(插件类skill,存在Claude的插件目录里,不是public内置skill)

Skill核心内容:
1. **39个社群清单**——25个"兴趣类"社群(全国范围搜索,如 Live Music Crew、Birdwatch Brigade、Page Turners Club)+ 14个"学校专属"社群(按院校所在城市搜索,如 UCL Hub、University of St Andrews、Aston Fresher Hub 2026)
2. **信息源清单**——Fatsoma/FIXR(学生票务平台,注意"Sold Out N Years Running"这类模板文案不可信)、Eventbrite/Skiddle、Ticketmaster系、地方媒体What's On栏目、垂类信源(National Student Esports电竞、Outdoor Swimming Society游泳、Girl Gang女性社群、National Trust一日游等)
3. **学联网站技术判断**——MSL系统(`/ents/eventlist/`,服务端渲染,能直接抓)vs native.fm系统(纯JS渲染,抓不到内容),遇到新学校先判断走哪条路
4. **热度分级规则**——高热度/中热度/潜在价值,必须附真实依据,不能瞎定级
5. **每轮3-5个社群**的节奏限制(这是今天新加的,因为工作量已经cover不了)
6. **活动配图规则**(今天新加,尚未真正跑通)——三层兜底:活动专属图 > 场馆通用图 > 类目通用图,图片搜索同时兼作真实性核验

## 三、目前进度

- ✅ Track A(周末digest)已完成
- ✅ Track B(9/20-10/20窗口)在原31个社群 + 新增8个学校社群上,分多轮跑完,共整理出 **76条活动**,已产出Excel主表(见下方文件)
- ✅ 你上传的另一份手工核验表(TrackA+B_核查.xlsx)里的Track B部分已核对去重、合并进主表,并标记了"人工核验✔"列以区分AI搜索核实 vs 你人工核实过的内容
- ✅ 主表里加了"热度排行"(仅Live Music Crew 10条内部排序)和"跨社群同步备注"(一条活动匹配多个社群时,提示该同步发到哪个群)
- ❌ **活动配图这一步卡住了**——见下方"卡住的原因"

### 主表文件位置
`/mnt/user-data/outputs/UK_Events_TrackB_9.20-10.20.xlsx`(76行,14列,已在对话里发给你过)

## 四、配图卡在哪、为什么

尝试了三条路,在**当前claude.ai网页对话环境**里全部走不通:

| 方法 | 结果 | 原因 |
|---|---|---|
| `image_search`工具 | 能在对话里展示图片,但拿不到可复制的URL | 图片是客户端直接从源站拉取渲染的,没经过我这边,我拿不到文件或链接文本 |
| `bash_tool`容器内`curl`下载 | 403 `host_not_allowed` | 容器网络是平台级白名单,只放行npm/pypi/github等开发相关域名,图片所在的RSPB/Ticketmaster等域名都不在名单内 |
| `web_fetch`抓取网页里解析出的图片直链 | Permissions Error | 该工具只允许fetch"已经是搜索/抓取结果里的正式链接",从页面HTML里手动摘出的图片URL不算,会被拒绝 |

上网搜了一圈,也确认了社区里现成的"image-fetcher"类skill(如`interstellar-code-image-fetcher`、`kazuph/mcp-fetch`)本质都是Python脚本调用`requests`库直连下载,这些skill假设的运行环境是**本地不受限网络**(Claude Code、Claude Desktop),不是这个网页版容器,装了也没用。

## 五、下一步准备怎么试

**核心判断:去Claude Code里跑,大概率能绕开这层网络限制**——因为Claude Code是在你自己电脑上执行命令,用的是你电脑本身的网络环境,不经过claude.ai这边的容器白名单。但不是100%保证,还要看:
1. 你电脑/公司网络本身有没有额外的防火墙拦截
2. 目标网站(尤其票务/图库类网站)自己的反爬虫机制,即使网络通了也可能被拦

### 具体尝试计划

1. **把这个skill带过去**:把 `/mnt/skills/plugins/uk-events-hub-digest/SKILL.md` 的内容复制到Claude Code项目里(建一个`.claude/skills/uk-events-hub-digest/SKILL.md`,或者直接开一个新会话把内容贴给它,让它先读完整个流程规则)
2. **把当前76行的主表也带过去**,作为已有数据基础,不用重新跑一遍社群搜索,只针对"配图"这一个新增步骤补充
3. **在Claude Code里先小范围测试**,不要一上来就冲76行:
   - 建议先挑1个社群(比如 Birdwatch Brigade,4条,信源都是RSPB官网,图片URL相对好找)试跑,验证"搜图片直链 → requests下载 → 本地图片文件"这条链路真的通
   - 用类似 `interstellar-code-image-fetcher` 或直接写一个简单的 `requests.get(url).content` 脚本,按"活动专属图→场馆通用图→类目通用图"三层兜底逻辑取图
   - 下载成功后,用`openpyxl`的`Image`功能把图片直接嵌入Excel对应行,而不是存链接
4. **验证成功后再批量跑剩下的72条**,遇到反爬/403的网站就按skill里写的兜底逻辑降级(场馆通用图/类目通用图),并标注清楚分级
5. 如果Claude Code那边同样卡住(网站反爬拦截),备选方案还是回到"方案1(对话内展示,手动截图保存)"这条路

## 六、需要你带走的东西

- 本Excel主表文件(76行数据)
- Skill文件内容(见上方路径,或者需要我把完整SKILL.md内容也导出成一个文件一起打包?)

## 七、云端Claude Code(claude.ai/code)会话的验证结果——第五节的判断没有成立

这份交接文档连同Excel主表、SKILL.md被带到了**云端**Claude Code会话(claude.ai/code,不是本地终端/桌面版),在该会话里实测了三条路,结论是:**配图这一步在云端Claude Code里同样被拦,和网页版是同一类限制**。

| 方法 | 结果 | 原因 |
|---|---|---|
| 容器内`curl`直连(如`www.rspb.org.uk`、`eventbrite.co.uk`、`ticketmaster.co.uk`、`skiddle.com`,甚至`google.com`) | 全部 `403`(`CONNECT tunnel failed`) | 云端会话的出站流量走一层平台级代理白名单(`__agentproxy`),默认只放行 npm/pypi/github/anaconda 等开发相关域名,和网页版容器的白名单是同一套思路,只是实现不同 |
| `WebFetch`工具抓取网页(如事件详情页,想解析`og:image`) | `EGRESS_BLOCKED` | 这个工具的抓取请求同样要经过上面那层代理白名单,不是走Anthropic自己的后端,所以域名不在名单里一样被拦 |
| `WebSearch`工具 | **唯一能用的**——能搜到活动信息、确认日期,返回的是搜索结果的标题+页面链接 | 这个工具走的是Anthropic自己的搜索后端,不经过容器的出站代理,所以不受白名单限制;但它只给页面URL,给不了图片直链,也没法进一步抓取页面HTML去解析`og:image` |

**关键结论,推翻了第五节"去Claude Code能绕开限制"的判断**:这个判断是对的,但只对**本地**运行的Claude Code(桌面版/终端CLI,跑在你自己电脑上)成立——那种情况下出站流量是你电脑自己的网络,不经过Anthropic的容器代理。但**云端Claude Code会话(claude.ai/code,包括从网页/App/`claude --cloud`发起的)仍然跑在Anthropic托管的沙盒VM里,默认网络策略是同一类白名单代理**,所以配图这步在云端会话里一样卡住,不是"换个入口就能绕开"。

### 如果还想在云端环境试

云端环境(cloud environment)的网络访问级别是可配置的(参考 Claude Code 文档 "Cloud environments" → "Network access"),默认是较受限的级别。如果有权限,理论上可以把该环境的网络策略调宽,放行图片所在的具体域名后重新尝试"搜图片直链→下载→openpyxl嵌入Excel"这条链路——但没有验证过放宽之后目标网站自己的反爬虫机制是否还会拦(第五节提到的第二个风险依然存在)。

### 目前的决定

用户选择:**先把现有76行数据+skill文件+交接文档提交进代码仓库,配图这一步留到真正的本地(非云端)Claude Code环境里再跑**——即第五节原计划描述的路径,不是本次云端会话。
