---
name: uk-events-hub-digest
description: Curate UK local offline events (music festivals, gigs, markets, walks, club nights, subculture meetups, etc.) and match each one to the right interest-based community (e.g. Live Music Crew, Outdoor Adventure Club, Page Turners Club) or university-based community (e.g. University of St Andrews, King's College London), with heat rating and reasoning. Use this whenever the user asks to collect/整理/汇总近期英国本地活动, wants an activity list for their communities, asks "which community does this event fit", or mentions Eventbrite/Skiddle/Meetup/Fatsoma/Songkick-style UK event sourcing for their community network. Always run this instead of a generic web search when the request is about populating or refreshing this event pipeline.
---

# UK Events → Community Digest

Turns scattered UK event listings into one table: deduped, categorized by why someone would go (not by format), heat-rated with real evidence, and matched to the correct community/communities — with an address precise enough to judge relevance. **This skill is collection/curation only** — posting cadence and timing are decided and executed by the user separately; don't assume or plan around any particular posting schedule.

**Structure note**: this pipeline previously matched events to 14 geographic "Student Hub" cities. That structure has been fully retired — matching is now by **interest/community fit**, not city/distance. Do not revive the old city-Hub mapping, Leeds dual-push rule, or 40km radius logic; none of it applies anymore.

## Communities (65 total — 22 interest-based + 43 university-based; treated uniformly, no special-casing by type)

```
Birdwatch Brigade        — birdwatching, nature spotting, wildlife walks
The Gaming Corner         — general gaming meetups, arcade/retro gaming, gaming bars/cafes
Coffee Shop Hopping        — new cafe openings, coffee festivals, cafe crawls
CS2 Frag Hub               — Counter-Strike 2 esports: LAN events, tournament viewing parties, gaming cafes hosting CS2
Day Trip Buddies           — day trips/short excursions outside the city, city-break-adjacent outings
Study Break Crew           — casual near-campus social hangouts, study-break socials, pub quiz
Fitness Check-ins          — group fitness classes, run clubs, gym events, sports meetups
Girls' Corner              — general women-focused social events
Green Thumb Circle         — gardening, plant markets/sales, allotment events, gardening workshops
IC Collective              — school-specific: **Imperial College London** — events should be in/near London (same treatment as UCL Hub)
Live Music Crew            — gigs, concerts, live music of any genre
Page Turners Club          — book clubs, author talks, literary festivals, bookshop events
Paws UK                    — dog/pet meetups, dog-friendly events, pet expos
Premier Fan Zone           — football (Premier League focus) — viewing parties, fan events
Reel Talk Club             — film screenings, cinema events, film festivals/club nights
Snack Finds & Picks        — food/snack tastings, pop-up food markets
Outdoor Adventure Club     — hiking, climbing, camping, more intense outdoor activity than Walking Buddies
Swim Wave Tribe            — swimming events, open-water swim meetups, pool sessions
Tennis Rally Crew          — tennis meetups/social hits
UCL Hub                    — school-specific: University College London — events should be in/near London
UK Food Lovers             — food festivals, restaurant events, general food-focused markets
Valorant Riot Crew         — Valorant esports: LAN events, tournament viewing parties
Vintage Vibe Crew          — vintage/thrift markets, vintage fairs, charity-shop-crawl-style events
Walking Buddies            — casual walking groups, city walking tours (gentler than Outdoor Adventure Club)
University of St Andrews   — school-specific: events in/near St Andrews
Glasgow City College       — school-specific: events in/near Glasgow
University of West of Scotland — school-specific: events in/near its campuses (Paisley/Ayr/Lanarkshire/Dumfries)
Glasgow Caledonian University — school-specific: events in/near Glasgow
Heriot-Watt University     — school-specific: events in/near Edinburgh (Riccarton campus)
Royal College of Art       — school-specific: events in/near London (Kensington/Battersea campuses)
Coventry Fresher Hub 2026  — school-specific: **Coventry University** — events in/near Coventry
University of Stirling     — school-specific: events in/near Stirling
BCU Fresher Hub 2026       — school-specific: **Birmingham City University** — events in/near Birmingham
Aston Fresher Hub 2026     — school-specific: **Aston University** — events in/near Birmingham
Wolverhampton Freshers Hub 2026 — school-specific: **University of Wolverhampton** — events in/near Wolverhampton
Walsall Freshers Hub 2026  — school-specific: **University of Wolverhampton's Walsall campus** — events in/near Walsall
Sheffield Hallam University — school-specific: events in/near Sheffield
University of Sheffield    — school-specific: events in/near Sheffield
St Mary's University, Twickenham — school-specific: events in/near Twickenham / south-west London (Richmond, Kingston); central London only if easy to reach
King's College London      — school-specific: events in/near central London (Strand/Waterloo/Guy's campuses)
London School of Economics — school-specific: events in/near central London (Holborn/Aldwych)
Queen Mary University of London — school-specific: events in/near east London (Mile End/Whitechapel)
University of Lancashire   — school-specific: formerly UCLan, main campus Preston — events in/near Preston
University of Lancaster    — school-specific: **Lancaster University** — events in/near Lancaster (different town from Preston — don't merge with University of Lancashire)
University of Chester      — school-specific: events in/near Chester
University of Strathclyde  — school-specific: events in/near Glasgow city centre
The University of Manchester — school-specific: events in/near Manchester
Newcastle university       — school-specific: events in/near Newcastle upon Tyne
Newcastle university 2     — school-specific: second group of the same Newcastle University audience — same matches as Newcastle university
Northumbria university     — school-specific: events in/near Newcastle upon Tyne
Durham university          — school-specific: events in/near Durham
university of york student hub — school-specific: **University of York** — events in/near York
Leeds Uni Student Hub      — school-specific: **University of Leeds** — events in/near Leeds
Leeds University group 2   — school-specific: second group of the same University of Leeds audience — same matches as Leeds Uni Student Hub
Huddersfield Uni Student Hub — school-specific: **University of Huddersfield** — events in/near Huddersfield
Hull Uni Student Hub       — school-specific: **University of Hull** — events in/near Hull
University of Leicester    — school-specific: events in/near Leicester
Staffs Student Life | Stoke — school-specific: **Staffordshire University** — events in/near Stoke-on-Trent
Keele Campus Life          — school-specific: **Keele University** — events on campus / in Newcastle-under-Lyme / Stoke-on-Trent
Harper Adams Campus Life   — school-specific: **Harper Adams University** (rural, Newport, Shropshire) — events in/near Newport/Telford; rural campus, so countryside/agri/day-trip events fit well
SCCB| Birmingham Student Life — school-specific: **South & City College Birmingham** (FE college, campuses incl. Digbeth/Hall Green/Bournville) — events in/near Birmingham
University of Cardiff      — school-specific: **Cardiff University** — events in/near Cardiff
Cardiff Metropolitan University — school-specific: events in/near Cardiff (Llandaff/Cyncoed)
University of Edinburgh Freshers 2026 — school-specific: events in/near Edinburgh
University of Aberdeen Freshers 2026 — school-specific: events in/near Aberdeen
```

Removed from this pipeline — do not add back or match events to them: Campus Confessions, Reality TV Rants and ZYMIX Deal Hunters (not an offline-event audience), and **all society groups (社团群) and student-residence groups (公寓群)** (e.g. LSE 0926 fresher picnic, UOM TWSOC 26/27, UOL BCS 26/27, Birmingham Chinatown | Food &Events, University of Strathclyde Chinese Students and Scholars, Kensington House Social, 88 Bromsgrove Social Hub, true Birmingham Social Hub, Bristol Rd Food & Drinks, Straits Manor). Only interest communities and university communities stay in scope. IC Collective = Imperial College London. Everything from UCL Hub / IC Collective / University of St Andrews down is a **university community** (43 total, one per university/college, plus two "group 2" duplicates). For all of these, location (near that institution's campus) decides the match.

**Shared-city groups — search the city once, then match the same event to every relevant community in it, rather than re-searching per school:**
- **London**: UCL Hub, IC Collective, Royal College of Art, King's College London, London School of Economics, Queen Mary University of London (St Mary's Twickenham is outer south-west London — only pull central-London events that are easy to reach)
- **Birmingham**: BCU Fresher Hub 2026, Aston Fresher Hub 2026, SCCB| Birmingham Student Life
- **Glasgow**: Glasgow City College, Glasgow Caledonian University, University of Strathclyde
- **Edinburgh**: Heriot-Watt University, University of Edinburgh Freshers 2026
- **Newcastle upon Tyne**: Newcastle university, Newcastle university 2, Northumbria university
- **Leeds**: Leeds Uni Student Hub, Leeds University group 2
- **Sheffield**: Sheffield Hallam University, University of Sheffield
- **Cardiff**: University of Cardiff, Cardiff Metropolitan University
- **Stoke-on-Trent area**: Staffs Student Life | Stoke, Keele Campus Life

"Group 2" communities (Newcastle university 2, Leeds University group 2) are the same audience as their first group — they always get exactly the same matches. Wolverhampton and Walsall are both University of Wolverhampton campuses in different towns — a Wolverhampton-area event and a Walsall-area event are usually distinct, but check both if a source describes an event as serving "both campuses." Likewise University of Lancashire (Preston) and University of Lancaster (Lancaster), and Durham vs Newcastle, are different towns — don't merge them.

### 社群中文名对照(大学类,用户提供)

输出表里给用户看时可附中文名;搜索与匹配仍以英文社群名为准。

| 社群 | 中文名 / 类型 |
|---|---|
| University of St Andrews | 圣安德鲁大学 |
| Glasgow City College | 格拉斯哥城市大学 |
| Glasgow Caledonian University | 格拉斯哥卡利多尼安大学 |
| University of West of Scotland | 西苏格兰大学 |
| Heriot-Watt University | 赫瑞瓦特大学 |
| Royal College of Art | 皇家艺术学院 |
| Coventry Fresher Hub 2026 | 考文垂大学 |
| University of Stirling | 斯特林大学 |
| BCU Fresher Hub 2026 | 伯明翰城市大学 |
| Aston Fresher Hub 2026 | 阿斯顿大学 |
| Wolverhampton Freshers Hub 2026 | 伍尔弗汉普顿大学 |
| Sheffield Hallam University | 谢菲尔德哈勒姆大学 |
| St Mary's University, Twickenham | 圣玛丽大学 |
| University of Lancashire | 兰开夏大学 |
| University of Chester | 切斯特大学 |
| University of Lancaster | 兰卡斯特大学 |
| University of Strathclyde | 思克莱德大学 |
| SCCB\| Birmingham Student Life | South & City College Birmingham |
| Staffs Student Life \| Stoke | 斯塔福德郡大学(斯托克) |
| Keele Campus Life | 基尔大学 |
| Newcastle university | 纽卡斯尔大学 |
| Newcastle university 2 | 纽卡斯尔大学 2 群 |
| Northumbria university | 诺桑比亚大学 |
| Huddersfield Uni Student Hub | 哈德斯菲尔德大学 |
| King's College London | KCL(伦敦国王学院) |
| University of Cardiff | 卡迪夫大学 |
| Hull Uni Student Hub | 赫尔大学 |
| London School of Economics | LSE(伦敦政经) |
| Leeds Uni Student Hub | 利兹大学 |
| Leeds University group 2 | 利兹大学 2 群 |
| University of Sheffield | 谢菲尔德大学 |
| University of Leicester | 莱斯特大学 |
| Harper Adams Campus Life | 哈珀亚当斯大学 |
| University of Edinburgh Freshers 2026 | 爱丁堡大学 |
| Queen Mary University of London | 伦敦玛丽女王大学 |
| University of Aberdeen Freshers 2026 | 阿伯丁大学 |
| Cardiff Metropolitan University | 卡迪夫城市大学 |
| The University of Manchester | 曼彻斯特大学 |
| university of york student hub | 约克大学 |
| Durham university | 杜伦大学 |

## Workflow

1. **Before searching, lay out a Community coverage checklist** — all 65 communities down one side. This is the task list for the run; don't skip straight to searching without it. Given 65 communities is a large surface and each event now also needs an image (see Event imagery below), **cap each round at 3-5 communities** rather than trying more — agree scope with the user up front and split the full sweep across multiple rounds rather than silently doing a shallow pass on everything.
2. **Search by interest/keyword, not by city** — for the 22 interest communities, search nationally for the relevant interest (e.g. `UK book club events this week`, `open water swimming events UK`), since these communities aren't tied to one location. For the 43 university communities, search near that specific institution's city instead (e.g. `St Andrews events this week`) — and remember many share a city (see the shared-city groups above: London, Birmingham, Glasgow, Edinburgh, Newcastle, Leeds, Sheffield, Cardiff, Stoke), so one city search can feed multiple communities. Never combine multiple unrelated communities into a single query — this was tried once with cities and silently tanked coverage; the same risk applies here.
3. **Pull from sources** (list below) for the requested time window (**7 days** for a near-term digest, **30 days** for a "what's hot coming up" digest — confirm which the user wants; don't default silently).
4. **Curate, don't dump**: aim for **3-5 well-chosen candidates per community**, not an exhaustive list. Apply these filters before a candidate counts as a real pick:
   - Genuinely fits the community's interest (not just loosely adjacent).
   - Ticket/entry price not high — this is for students, flag anything that reads as expensive.
   - Reflects current youth/pop-culture relevance, not generic filler.
   - Prefer events with **real institutional/official backing** (venue, ticketing platform, students' union, established promoter with track record) — since this pipeline only aggregates other people's events (no in-house events of its own), that backing is the main protection against sending people to something that turns out empty. **Exclude private gatherings, religious events, and very small/informal meetups** from this pipeline for now.
5. **Extract fields per event**: title, **full venue address** (street-level; if a source only gives city-level location, record it anyway but tag `address_quality: city_only` rather than inventing a street address), date/time, category tag(s), source platform, and whatever raw popularity signal the source exposes. **Verify the actual date from a specific event/ticketing page, not just a festival-listing or "coming up" summary page** — promotional listing pages describe a recurring brand ("10th anniversary", "returns this October") without necessarily giving *this* year's date, and it's easy to mistake a different year's edition (already past, or a year+ away) for the current one. This already caused a real error once — cross-check against at least one direct ticketing source before treating a date as confirmed, and never present an approximate date as if it were confirmed. **When a "this weekend"/monthly-overview page isn't returning a confirmed date, search by the exact date string instead** (e.g. `"19 September 2026" <city>`) — Songkick in particular sorts by venue and exact date and finds events that vaguer listing pages miss.
6. **Dedup** on title + date + venue. When the same event appears across multiple sources, merge into one record and keep every source URL — don't merge two events just because titles look similar.
7. **Categorize** using the interest taxonomy below — this now maps close to directly onto the community list itself.
8. **Heat-rate**: 高热度 / 中热度 / 潜在价值 — always attach the concrete evidence, never a bare label (see Heat Rating below). Followers/members ≠ attendees; never present platform reach or search ranking as popularity evidence.
9. **Match to community/communities** — an event can fit more than one (e.g. an outdoor swim meetup could hit both Swim Wave Tribe and Outdoor Adventure Club; an event near a campus can hit both an interest community and a school community — don't restrict school-community matches to official student-society events only, any real event near enough to the campus counts). list all genuine fits, don't force a single pick. For the 43 university communities, location is the deciding factor same as before; for the 22 interest communities, interest-fit is the deciding factor, not geography.
10. **Output** as an Excel workbook in the per-community post-block layout — see **Output format** at the end of this file.
11. **Always attach the coverage checklist from step 1, filled in** — mark each community as searched/found, searched/nothing found, or not searched (and why). A run that only covers some communities is fine — an unlabeled one that looks complete but isn't, is not.

Do not call any LLM/API mid-pipeline to do the tagging "automatically" — the categorizing/heat/community judgment in steps 7-9 IS the job Claude does directly in this conversation when the user pastes in raw scraped data. Never fabricate popularity numbers — if a source gives no real signal, say so and rate it 潜在价值 at most.

## Sources

### 结构化票务类（有真实人数/票量信号，热度证据优先来自这里）
- Eventbrite — city listing pages (`eventbrite.co.uk/d/united-kingdom--<city>/events/`). No public search API anymore (deprecated 2020) — scrape listing pages or fetch directly.
- Skiddle — `skiddle.com/whats-on/<city>/`
- Meetup — **known-group whitelist only**, not search (Meetup's search API is paywalled/OAuth-gated). Maintain a list of known active groups per interest area; read each group's public page (`__NEXT_DATA__` JSON gives member count/rating; regex fallback on "X members" text).
- **Fatsoma** — UK's dedicated student nightlife ticketing platform (18-25 demographic). **Credibility caveat (confirmed via a Student Room thread): treat Fatsoma's own marketing copy with real skepticism.** Phrases like "Sold Out 10 Years Running", "Sold Out 15 Years Running", "OFFICIAL" appear verbatim, word-for-word, across many different cities and events from third-party freshers-ticket promoters — this is templated marketing copy, not an independently verified achievement. **Never accept a phrase as heat evidence if it also appears verbatim on other cities'/events' pages.** Genuine evidence from Fatsoma looks like a live numeric ticket figure (e.g. "95% sold") or a claim that can be cross-checked against the actual institution's own channel.
- FIXR — Fatsoma's direct competitor, same use case and same credibility caveat applies.
- Ticketmaster UK / AXS UK / See Tickets / Gigantic — for bigger concerts/festivals outside the student-specific platforms' reach.
- Songkick — best used for exact-date lookups (`"<date>" <city>` queries return venue-sorted, precisely-dated listings); more reliable than weekend/monthly overview pages when a specific date needs confirming.

### 媒体资讯类（专职团队维护，含"What's On"独立栏目/独立活动网站——不是综合新闻夹带）
These are prose/article-style, not structured cards — pull the article's clean text and extract events from it manually/in this conversation rather than trying to regex-parse it.
- Manchester Evening News, Leeds-List, Leeds Inspired, Liverpool Echo What's On, Bristol24/7, WalesOnline, BirminghamLive, ChronicleLive, WhatsOnLive — all `/whats-on/`-style sections confirmed active and professionally maintained.

### 学联官网技术平台判断(通用技巧,非唯一验证手段)
英国大学学联官网主要用两套后台系统,抓取前先判断用哪套,能省大量无效尝试:
- **MSL**(页脚标注 `Powered by MSL`,URL含 `/ents/eventlist/?month=X&year=Y`)— 服务端渲染,`web_fetch` 可直接拿到完整的、真实带日期地点的活动列表,信噪比高,几乎不需要额外筛选。已验证走这套系统的:Heriot-Watt(hwunion.com)、Stirling(stirlingstudentsunion.com)、Coventry(yoursu.org)、BCU(bcusu.com)、Wolverhampton(wolvesunion.org,City和Walsall两校区共用一个"What's On"页并按校区打标签)。
- **native.fm**(页脚标注 `Powered by native.`)— 纯JS客户端渲染,`web_fetch` 只能拿到空壳HTML,拿不到活动内容,只能退而求其次靠搜索引擎快照零散拼凑,信息不完整、日期不齐。已踩坑:RCA(rcasu.org.uk)、Aston(astonsu.com)。
遇到新学校时,先看学联官网页脚标注哪个平台,能预判这条路好不好走,但**不能当成唯一的活动真实性验证依据**——同一所学校仍应尽量交叉核实(如该校官方新闻页、Eventbrite、本地媒体),尤其在native.fm平台拿不到完整列表、只能靠零散搜索结果拼凑时,更要对单条信息保持怀疑,不要因为"搜到了"就当真。
- **The Tab** (`thetab.com/university/<uni>`) — NOT an event-listing source (it's Gen-Z news/culture/gossip). Use only as a secondary signal for whether a category of event is genuinely something students are talking about — supporting evidence for a 潜在价值 rating, never the primary extraction source.

### 垂类信息源（按社群，已核实为活跃/官方来源）
- **National Student Esports (NSE)** (`nse.gg`) — self-describes as "the official body of university esports in the UK", operates the British University Esports Championship. Use for **CS2 Frag Hub / Valorant Riot Crew**. **Note on NUEL**: the older National University Esports League (NUEL, founded 2010) was acquired by GGTech and rebranded "University Esports UK & Ireland" — it still runs tournaments (e.g. Amazon University Esports) but has shown scheduling instability (a Spring season was reportedly skipped one year per Esports News UK). Prefer NSE as the more current/stable primary source; NUEL/University Esports UK & Ireland is usable as a secondary cross-check, not the sole source.
- **Outdoor Swimming Society (OSS)** (`outdoorswimmingsociety.com`) — established 2006, the UK's leading wild-swimming community; runs its own events, maintains a UK-wide list of active local swim groups (`/uk-wild-swimming-groups/`) with real meet times/contacts, and hosts a crowd-sourced wild swim map. Use for **Swim Wave Tribe**.
- **British Long Distance Swimming Association (BLDSA)** (`bldsa.org.uk`) — official governing body for long-distance/open-water swimming in the UK, publishes a real dated events calendar (entries open/close, prize info). Use for **Swim Wave Tribe** alongside OSS.
- **Girl Gang** (city-specific chapters, e.g. `girlgangmcr.com` for Manchester; also active in Sheffield, Leeds, Edinburgh) — real community collective (Manchester chapter running since 2016), publishes a genuine "Regular Events" page with recurring dated activities (book club, quiz nights, wellbeing sessions). Use for **Girls' Corner**, but note the audience skews slightly broader/older than a pure student community (16-80 per their own materials) — flag this when using, and confirm which city chapter is actually active/updated before citing it.
- **National Trust** (`nationaltrust.org.uk/visit/whats-on` + each property's own `/events` subpage) — official heritage body, actively maintained, real dated exhibitions/events at properties nationwide (not just static site info). Use for **Day Trip Buddies** — properties near a given city/campus are a good fit for a low-cost, real day out.
- **EPIC.LAN** (`epiclan.co.uk`, tournaments at `tournaments.epiclan.co.uk`) — long-running UK BYOC LAN series at Kettering Leisure Village, two editions a year (summer + late Oct/Nov). CS2 and VALORANT tournaments run alongside StarCraft II and osu!. It is the most reliable in-person source for **CS2 Frag Hub / Valorant Riot Crew / The Gaming Corner**. Always confirm which edition number matches your window (see Verification lessons).
- **Rejected — do not use**: **Multiplay** (the old UK LAN-event organiser brand) — confirmed defunct as an events business: sold to GAME in 2015, digital arm sold to Unity in 2017, community servers shut down 2019. Its Insomnia Gaming Festival legacy is not a live source for this pipeline.

**Deliberately excluded** (checked and rejected — don't re-add without new evidence): generic "What's On [City]" fan-run Facebook pages (chronically abandoned), PlaceCal/WhereCanWeGo/EventsList/Funcheap UK (low-traffic aggregators), Facebook Events generally (can't access), Local Council pages as a primary source (too slow-updating), university Students' Union main social accounts (governance/campaign-focused, not event listings), Multiplay (defunct, see above).

**Still unresolved — flagged, not yet solved**: Coffee Shop Hopping has no reliable dated-event source found so far (coffee festivals/new-openings/workshops are either off-window, wrong audience, or not truly event-shaped) — treat as an open problem, not a solved one; don't assume the sources above cover it.

## Interest taxonomy (maps closely to the community list itself)

| 类目 | 覆盖内容 | 对应社群举例 |
|---|---|---|
| 社交类 | Dating/Singles/Networking/交友 | Girls' Corner, Study Break Crew |
| 兴趣类 | Gaming/摄影/读书会/D&D/手工/园艺/观鸟 | The Gaming Corner, Page Turners Club, Green Thumb Circle, Birdwatch Brigade |
| 本地生活类 | 集市/农夫市场/美食节/咖啡/复古市集 | Coffee Shop Hopping, UK Food Lovers, Snack Finds & Picks, Vintage Vibe Crew |
| 年轻人娱乐 | Pub Quiz/Comedy/Club/沉浸式/电竞 | Live Music Crew, CS2 Frag Hub, Valorant Riot Crew, Premier Fan Zone |
| 运动户外 | 徒步/游泳/网球/健身/远足 | Walking Buddies, Outdoor Adventure Club, Swim Wave Tribe, Tennis Rally Crew, Fitness Check-ins, Day Trip Buddies |
| 电影/媒体 | 观影/放映/影展 | Reel Talk Club |
| 宠物 | 遛狗/宠物聚会 | Paws UK |

An event can carry more than one tag/community. Content format (concert/film/exhibition) is a secondary tag only.

## Heat rating — always with real evidence, calibrated per platform

| 来源类型 | 真实热度信号 |
|---|---|
| Meetup | 成员数、RSVP数、历史场次数、评分 |
| Eventbrite/Skiddle | 票量/剩余票数/销售速度、真正独立于其他活动页面的官方宣传 |
| Fatsoma/FIXR | **只信实时数字类信号**（如"95% sold"），**不信"Sold Out N Years Running"/"OFFICIAL"这类模板文案** |
| 媒体资讯类 | 是否被列入本地媒体"本周精选"/"best of"榜单 |
| The Tab (辅助信号) | 是否被学生反复提及/讨论——只作为潜在价值的佐证，不单独定级 |

Rating bands:
- **高热度** — concrete, strong evidence (large established member base + long track record; explicit "sold out" claims with real corroboration; verified official partnership; multi-year recurring event)
- **中热度** — some real exposure but weaker signal (local media pick, moderate ticket sales, first-year event)
- **潜在价值** — niche/small but fits a genuine interest area, or is new/emerging; also the default when a source gives no usable popularity signal at all

## Event imagery (every row needs one — three-tier fallback, never skip silently)

Every event row must carry an image. Use `image_search` (query: event name + venue/city) once the event's core facts (name/venue/date) are otherwise settled — this search doubles as a **verification pass**: if no image or corroborating page turns up at all for an event supposedly this real, that's a signal to double-check the event itself before including it, not just a missing-image problem.

Three-tier fallback, in order — never leave a row imageless, and never silently substitute a mismatched image without saying so:
1. **活动专属图** — official poster/key visual or venue photo specifically tied to this event (venue's own site, official ticketing page listing, organiser's social post). Highest confidence — use this whenever found.
2. **场馆通用图** — if no event-specific image exists, fall back to a generic photo of the venue itself (exterior/interior), labelled as such — not passed off as an event photo.
3. **类目通用图** — if even the venue has no usable photo, fall back to a generic image representing the event's 类目 (e.g. a generic live-music-crowd photo for a Live Music Crew gig), clearly labelled as generic/stock, not this specific event.

Every row states which tier it used — never present a tier-2 or tier-3 image as if it were tier-1. Store the image as a URL (don't download/embed the binary into the spreadsheet — keeps file size sane and avoids format issues).

## Quality checks before output

Flag rather than silently drop: missing date, missing venue/address, event outside the time window, a heat rating with no attached evidence, an event that doesn't genuinely fit any community, a community that couldn't reach 3-5 real candidates at the required bar, or an event for which no image at any of the three tiers could be found. Report these gaps explicitly rather than quietly omitting the row or padding with weak/private/religious/tiny events to hit a count.

## Verification lessons (real mistakes from past runs — check every row against these)

Each of these actually happened in a run. Run the check that catches each one before you output.

- **Edition / 届数 mix-ups.** A recurring series has several editions a year, and the ticketing pages for different editions look almost the same. The Oct–Nov 2026 run first recorded "EPIC48 CS2, 30 Oct–1 Nov", but EPIC48 actually ran 16–19 Jul 2026; the autumn event was EPIC49. Confirm the edition number and the dates from the same page (the organiser's page for that edition, or Liquipedia). A registration deadline that falls before the event you're looking at is a red flag.
- **Weekday check catches stale pages.** For every date, check the stated weekday against the target year. "Sat 23 / Fri 29 / Sat 30 Oct" only fits 2021, so that Black Country Living Museum page was an old one. "Mon 5 Nov" (Glasgow Green) fits 2018. "Sat 22 Nov" (Preston lights) fits 2025. A mismatch means the page is from another year: drop the row, or flag it as unconfirmed.
- **Search-summary conflation.** Search-result summaries merge nearby facts. Skindred playing the Barrowland on the same weekend got written up as "part of Core. festival", but it wasn't in the Core. lineup. Check that the lineup or programme actually names the act before you say it is part of a festival.
- **Wrong place with the same name.** "Lancaster" results from Lancaster, Pennsylvania (a Halloween bar crawl, The Woman in Black). "Leeds Castle fireworks" is in Kent, not Leeds. Check the postcode or county.
- **Cancelled or ended events still rank in search.** Durham Lumiere ended after 2025. Edinburgh's Meadowbank fireworks ended in 2017. Leeds council stopped its six park bonfires, Roundhay included. Search "<event> <year> cancelled/final/returns" before you trust a recurring event.
- **Post copy must match the community.** When CS2 Frag Hub and Valorant Riot Crew were merged into one block, the Valorant group got a line about a "CS2 tournament". Fireworks nights with a DJ set were put under Live Music Crew. Each line in a community's copy has to be about that community's own interest. An event that is only loosely adjacent goes to the school/city block, not the interest block.
- **Sold out = don't push.** Leave out events whose official box office shows sold out (Samhuinn Fire Festival, Moseley fireworks). List them in the gaps sheet instead.
- **Fatsoma template copy.** "Biggest Halloween Event / 10,000 People" (Project Halloween) appeared word-for-word for several cities. Never use it as heat evidence.
- **Addresses must be researched, never guessed.** Briarlands Farm was first written as "Cambusbarron / Craigforth area" from a guess; it is actually at Blairdrummond, FK9 4UP. Search `<venue> address postcode` for every venue. Tag `address_quality` by these rules:
  - `exact`: named venue + street and/or postcode. For public spaces a street/square name is enough.
  - `venue_only`: named venue(s) without a full street address. For multi-venue festivals, list the main venues by name (+ street if known), and for parades and trails give the route or the named hubs (e.g. Paisley parade route, Light Night info hub at Millennium Square), rather than writing "多个场地".
  - `city_only`: only when the organiser genuinely hasn't published a venue (e.g. Lonely Girls Club reveals the venue only after booking). Say why in the address cell.
  - Anything still unknown goes in `待核实与缺口` as `地址未明`.
- **Unique event keys.** If you build the table from code, give every event a unique key and assert on duplicates. A reused key silently overwrote one event with another (Richmond Fireworks got replaced by Rich Hall).

## Environment note (claude.ai/code cloud sessions)

In cloud sessions only `WebSearch` works. `WebFetch` and `curl` to event or ticketing sites are blocked by the egress proxy (`EGRESS_BLOCKED` / 403). So students' union (SU) pages (MSL or native.fm), Eventbrite and Skiddle cannot be fetched directly. Rely on search results and cross-check them against at least one official/ticketing result. The image step cannot run in the cloud. Leave `图片链接` as "未取图" and `图片来源分级` as "未完成", and say so. LibreOffice may also fail to open files, so formulas can't be recalculated. Set `fullCalcOnLoad` so Excel recalculates on open, and verify the expected values in Python.

## Output format

Deliver one Excel workbook per run (e.g. `data/UK_Events_TrackB_<window>.xlsx`), font Arial, with these sheets:

### 1. `Track B 30天活动` — per-community post blocks (main sheet)

**The unit is the community you post to.** Each community gets one block. The block lists all the events that go to that community, one per row, and columns A–C are **merged vertically across the block's rows**:

`社群 | 图文 | 发布文案 | 活动名称 | 详细地址 | 地址质量(exact/venue_only/city_only) | 日期 | 类目 | 热度 | 热度依据 | 来源链接 | 推荐理由 | 同一活动也推给 | 图片链接 | 图片来源分级(活动专属图/场馆通用图/类目通用图)`

- **Merging communities into one block.** Merge **university communities only**, and only when their event lists are exactly the same (e.g. the six London schools, Newcastle ×2 + Northumbria, Cardiff + Cardiff Met). Join the names with ` / ` in `社群`, e.g. `Glasgow City College / Glasgow Caledonian University / University of Strathclyde`. **Never merge interest communities**, even when their event lists match (e.g. CS2 Frag Hub and Valorant Riot Crew): each needs its own theme and wording.
- **`图文`** holds the image filename for the post, one per block. Put `待制作：<community>.png` until the user supplies one.
- **`发布文案`** is ready-to-post English copy for the whole block, in this template:
  ```
  🔍 Event Radar (UK) — what's worth doing this month.
  This month: <THEME IN CAPS> 👇
  <emoji> <Event name>, <place> — <one-line hook>, <date>.
  <emoji> <Event name>, <place> — <one-line hook>, <date>.
  ```
  Themes: interest blocks use their interest (FILM, MUSIC, CS2 & LAN, VALORANT & LAN, GIRLS' NIGHTS OUT…); school blocks use the city (LONDON & CAMPUS, GLASGOW NIGHTS, CARDIFF…). Every line must fit **this** community (see Verification lessons). For unconfirmed dates write "TBC" / "late Oct"; never state a guessed date as fact.
- **Row order** inside a block: 高热度 → 中热度 → 潜在价值. Colour-code `热度` (高 = light red, 中 = light yellow, 潜在价值 = light grey).
- **`同一活动也推给`** names the other blocks that also carry this event, so the user can post in sync.
- **Block order**: interest communities first, then university communities, both in community-list order. Freeze the header row only (freezing columns has broken merged-cell display in some viewers). Add an autofilter.
- Target 3–5 events per community. Fewer is fine if it's flagged in the coverage sheet.

### 2. `汇总`
Counts as formulas pointing at the main sheet: number of blocks, event rows, rows per heat level, and rows whose date carries ⚠️.

### 3. `社群覆盖清单`
One row for every community in the list: 社群 | 类型(兴趣类/大学类) | 状态 (第N轮 已搜/有结果 · 已搜/无结果 · 顺带匹配 · 未搜 + reason) | 条数 | 说明 (why it's short, what was excluded).

### 4. `待核实与缺口`
One row per issue: 类型 | 内容. Types include dates to verify, date mismatch → not included, sold out, discontinued, template marketing copy, price too high, not included (religious), corrected (log every fix to a previously delivered row here), and window reminders (events that only partly overlap the window).
