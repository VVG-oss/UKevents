---
name: uk-events-hub-digest
description: Curate UK local offline events (music festivals, gigs, markets, walks, club nights, subculture meetups, etc.) and match each one to the right interest-based community (e.g. Live Music Crew, Outdoor Adventure Club, Page Turners Club) or location-based community (a university, student residence or local area group, e.g. University of St Andrews, 88 Bromsgrove Social Hub), with heat rating and reasoning. Use this whenever the user asks to collect/整理/汇总近期英国本地活动, wants an activity list for their communities, asks "which community does this event fit", or mentions Eventbrite/Skiddle/Meetup/Fatsoma/Songkick-style UK event sourcing for their community network. Always run this instead of a generic web search when the request is about populating or refreshing this event pipeline.
---

# UK Events → Community Digest

Turns scattered UK event listings into one table: deduped, categorized by why someone would go (not by format), heat-rated with real evidence, and matched to the correct community/communities — with an address precise enough to judge relevance. **This skill is collection/curation only** — posting cadence and timing are decided and executed by the user separately; don't assume or plan around any particular posting schedule.

**Structure note**: this pipeline previously matched events to 14 geographic "Student Hub" cities. That structure has been fully retired — matching is now by **interest/community fit**, not city/distance. Do not revive the old city-Hub mapping, Leeds dual-push rule, or 40km radius logic; none of it applies anymore.

## Communities (78 total — 25 interest-based + 53 location-based; treated uniformly, no special-casing by type)

```
Birdwatch Brigade        — birdwatching, nature spotting, wildlife walks
The Gaming Corner         — general gaming meetups, arcade/retro gaming, gaming bars/cafes
Coffee Shop Hopping        — new cafe openings, coffee festivals, cafe crawls
Campus Confessions         — ❌ anonymous campus confession/gossip board — not an offline-event audience, skip in this pipeline
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
Reality TV Rants           — ❌ reality TV show discussion/watch-party content — not an offline-event fit, skip in this pipeline
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
ZYMIX Deal Hunters         — deal/coupon-hunting focused, not offline-event centric — **user has deprioritized this one, low/no priority for this pipeline**
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
LSE 0926 fresher picnic    — ⚠️ LSE freshers group built around a one-off picnic (0926 read as 26 Sep — already past as of 29 Sep 2026); treat as LSE audience, events in/near central London; confirm with user whether still active
Queen Mary University of London — school-specific: events in/near east London (Mile End/Whitechapel)
Kensington House Social    — ⚠️ location-based, assumed a student residence in Kensington, London — events in/near Kensington/west London; confirm exact building/city with user
University of Lancashire   — school-specific: formerly UCLan, main campus Preston — events in/near Preston
University of Lancaster    — school-specific: **Lancaster University** — events in/near Lancaster (different town from Preston — don't merge with University of Lancashire)
University of Chester      — school-specific: events in/near Chester
University of Strathclyde  — school-specific: events in/near Glasgow city centre
University of Strathclyde Chinese Students and Scholars — school + affinity: Strathclyde Chinese students (CSSA) — Glasgow events, favour ones with Chinese/East Asian or international-student appeal
The University of Manchester — school-specific: events in/near Manchester
UOM TWSOC 26/27            — school + affinity: University of Manchester Taiwanese Society 2026/27 — Manchester events, favour Taiwanese/East Asian or international-student appeal
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
SCCB| Birmingham Student Life — location-based: Birmingham student community (SCCB assumed to be a Birmingham student group/residence — ⚠️ confirm with user) — events in/near Birmingham
88 Bromsgrove Social Hub   — location-based: residents of 88 Bromsgrove Street student accommodation, Birmingham (Southside/Chinatown) — events in/near Birmingham city centre
true Birmingham Social Hub — location-based: residents of "true Birmingham" student accommodation — events in/near Birmingham city centre
Birmingham Chinatown | Food &Events — location + interest: food and events in/near Birmingham's Chinatown/Southside (Arcadian, Hurst St) — food openings, Asian food markets, Chinese festivals (e.g. Mid-Autumn, Lunar New Year)
Bristol Rd Food & Drinks   — location + interest: food/drink along **Bristol Road, Birmingham** (Selly Oak/Edgbaston, next to University of Birmingham) — new openings, food deals, bar/café events on or near that strip. Not Bristol the city.
University of Cardiff      — school-specific: **Cardiff University** — events in/near Cardiff
Cardiff Metropolitan University — school-specific: events in/near Cardiff (Llandaff/Cyncoed)
University of Edinburgh Freshers 2026 — school-specific: events in/near Edinburgh
University of Aberdeen Freshers 2026 — school-specific: events in/near Aberdeen
UOL BCS 26/27              — ⚠️ school + affinity, identity unconfirmed: "UOL" could be University of Liverpool / Leicester / London, "BCS" unclear (e.g. a society name) — ask user before searching for this one
Straits Manor              — ⚠️ identity unconfirmed (possibly a student residence) — ask user for city/audience before searching for this one
```

Campus Confessions and Reality TV Rants are excluded from this pipeline entirely (not an offline-event audience). ZYMIX Deal Hunters is deprioritized (low priority). IC Collective = Imperial College London. Everything from UCL Hub / IC Collective / University of St Andrews down is a **location-based community** (53 total): mostly one per university, plus a few student-residence groups (Kensington House Social, 88 Bromsgrove, true Birmingham, SCCB), area food groups (Bristol Rd Food & Drinks, Birmingham Chinatown) and affinity societies (Strathclyde CSSA, UOM TWSOC). For all of these, location decides the match; for the area-food and affinity ones, also check the interest/affinity fit. Communities marked ⚠️ have an unconfirmed identity or city — confirm with the user before spending a search round on them.

**Shared-city groups — search the city once, then match the same event to every relevant community in it, rather than re-searching per school:**
- **London**: UCL Hub, IC Collective, Royal College of Art, King's College London, London School of Economics, LSE 0926 fresher picnic, Queen Mary University of London, Kensington House Social (St Mary's Twickenham is outer south-west London — only pull central-London events that are easy to reach)
- **Birmingham**: BCU Fresher Hub 2026, Aston Fresher Hub 2026, SCCB| Birmingham Student Life, 88 Bromsgrove Social Hub, true Birmingham Social Hub, Birmingham Chinatown | Food &Events, Bristol Rd Food & Drinks (the last two need the food/area fit as well)
- **Glasgow**: Glasgow City College, Glasgow Caledonian University, University of Strathclyde, University of Strathclyde Chinese Students and Scholars
- **Edinburgh**: Heriot-Watt University, University of Edinburgh Freshers 2026
- **Manchester**: The University of Manchester, UOM TWSOC 26/27
- **Newcastle upon Tyne**: Newcastle university, Newcastle university 2, Northumbria university
- **Leeds**: Leeds Uni Student Hub, Leeds University group 2
- **Sheffield**: Sheffield Hallam University, University of Sheffield
- **Cardiff**: University of Cardiff, Cardiff Metropolitan University
- **Stoke-on-Trent area**: Staffs Student Life | Stoke, Keele Campus Life

"Group 2" communities (Newcastle university 2, Leeds University group 2) are the same audience as their first group — they always get exactly the same matches. Wolverhampton and Walsall are both University of Wolverhampton campuses in different towns — a Wolverhampton-area event and a Walsall-area event are usually distinct, but check both if a source describes an event as serving "both campuses." Likewise University of Lancashire (Preston) and University of Lancaster (Lancaster), and Durham vs Newcastle, are different towns — don't merge them.

## Workflow

1. **Before searching, lay out a Community coverage checklist** — all 78 communities down one side. This is the task list for the run; don't skip straight to searching without it. Given 78 communities is a large surface and each event now also needs an image (see Event imagery below), **cap each round at 3-5 communities** rather than trying more — agree scope with the user up front and split the full sweep across multiple rounds rather than silently doing a shallow pass on everything.
2. **Search by interest/keyword, not by city** — for the 25 interest communities, search nationally for the relevant interest (e.g. `UK book club events this week`, `open water swimming events UK`), since these communities aren't tied to one location. For the 53 location-based communities, search near that specific institution's/residence's city instead (e.g. `St Andrews events this week`) — and remember many share a city (see the shared-city groups above: London, Birmingham, Glasgow, Edinburgh, Manchester, Newcastle, Leeds, Sheffield, Cardiff, Stoke), so one city search can feed multiple communities. Never combine multiple unrelated communities into a single query — this was tried once with cities and silently tanked coverage; the same risk applies here.
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
9. **Match to community/communities** — an event can fit more than one (e.g. an outdoor swim meetup could hit both Swim Wave Tribe and Outdoor Adventure Club; an event near a campus can hit both an interest community and a school community — don't restrict school-community matches to official student-society events only, any real event near enough to the campus counts). list all genuine fits, don't force a single pick. For the 53 location-based communities, location is the deciding factor same as before; for the 25 interest communities, interest-fit is the deciding factor, not geography.
10. **Output** as a table: 活动名称 | 详细地址 | 地址质量 | 日期 | 类目 | 匹配社群 | 热度 | 热度依据 | 来源 | 推荐理由.
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

## Output format

One table per run, columns: `活动名称 | 详细地址 | 地址质量(exact/venue_only/city_only) | 日期 | 类目 | 匹配社群 | 热度 | 热度依据 | 来源 | 推荐理由 | 图片链接 | 图片来源分级(活动专属图/场馆通用图/类目通用图)`. Group by community. 3-5 curated rows per community is the target.
