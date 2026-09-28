# 舆图集 · 通用库数据 / Yutuji Historical Atlas — Open Data

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23010865.svg)](https://doi.org/10.5281/zenodo.23010865)

704 处地点、155 位人物、393 件事、263 部所引之书。每一条年份、地点、事件都注明出处，按 A—D 分级。数据来自 [舆图集](https://yutuji.com/)（手绘历史地图的中文刊物，by COZLABS），与站上 [/data/](https://yutuji.com/data/) 同一份。

704 places, 155 people, 393 events and 263 cited works from the Yutuji historical atlas (https://yutuji.com/). Every date, place and event carries its source and a reliability grade (A–D). Field names are English; values are Chinese, with English names for places and people (`name_en`). English notes: https://yutuji.com/data/en/

## 文件 / Files

| 文件 | 内容 |
|---|---|
| `data/places.json` `data/places.csv` | 地点：名、今名、经纬度、精度、所属、别名、外部库对照（维基数据、法鼓地名规范） |
| `data/people.json` `data/people.csv` | 人物：生卒、身分、小传、逐条带出处的行迹 |
| `data/events.json` `data/events.csv` | 事件：年、地、一句话、出处与分级 |
| `data/works.json` `data/works.csv` | 所引之书：书名、别称、著者、成书年代 |

要全的以 JSON 为准；CSV 里嵌套的字段用竖线分隔，复杂字段原样写成 JSON。
JSON is authoritative; CSV flattens nested fields.

## 等级 / Grades

| 等级 | 含义 |
|---|---|
| A | 正史与同时代文献原文 |
| B | 后代正史、类书、笔记与今人整理本 |
| C | 今人研究与今地比定 |
| D | 后世附会与推测——本册照录并注明出处 |

转用时请把等级一并带上。 Please keep the grade when reusing a record.

## id

每条记录的 `id` 是永久的：不改，不让给别的条目；条目下线时 id 不回收。站上的地址就是 id：`https://yutuji.com/place/<id>/`、`https://yutuji.com/person/<id>/`。
Record ids are permanent and map to stable URLs on the site.

## 已刊各期 / Issues

| 期 | 题 | id | 地址 |
|---|---|---|---|
| 1 | 江南六朝寺迹：南朝四百八十寺 | `liuchao` | https://yutuji.com/liuchao/ |
| 2 | 临安城记：州城、行在、省城 | `linan` | https://yutuji.com/linan/ |
| 3 | 大运河：一条河的三条路 | `yunhe` | https://yutuji.com/yunhe/ |
| 16 | 坤舆万国全图：一张地图怎样被翻译 | `kunyu` | https://yutuji.com/kunyu/ |
| 26 | 海国图志：一部世界地理怎样译进中文、又渡到日本 | `haiguo` | https://yutuji.com/haiguo/ |
| 27 | 玄奘：西行求法十七年 | `xuanzang` | https://yutuji.com/xuanzang/ |
| 29 | 丝绸之路：一条路名与路上往来的东西 | `silkroad` | https://yutuji.com/silkroad/ |
| 72 | 天工开物：物出何地 | `tiangong` | https://yutuji.com/tiangong/ |
| 74 | 湖畔百年：西湖边的房子 | `hupan` | https://yutuji.com/hupan/ |

`topics` 字段写的是这些 id。

## 字段 / Fields

### places.json（704）

| 字段 | 说明 |
|---|---|
| `id` | 永久编号，一经指定不改、不让给别的条目 |
| `name` | 本册采用的名字（多为当时的名字，如「大兴城」） |
| `name_now` | 今名（如「西安」）；与 name 相同时不填 |
| `admin_now` | 今属何地，到县一级 |
| `kind` | 类别：city 城 / temple 寺 / pass 关 / river 水 / mountain 山 等 |
| `ll` | 经纬度 [东经, 北纬]，小数度；无考者不填 |
| `precision` | 定位精度：exact 确址 / county 到县 / region 到片区 / unknown 无考 |
| `within` | 所属地点的 id（如坊属于城） |
| `dynasty` | 这个名字通行的年代 |
| `topics` | 出现在哪几期（期的 id） |
| `alias` | 各期原文里的其他写法（如涿郡又作「北京」「燕京」） |
| `name_en` | 英文名：维基数据英文标签，或按汉语拼音拼写 |
| `now_en` | 今地英文名 |
| `sameas` | 同一实体在外部库的地址：维基数据、法鼓文理学院地名规范库 |
| `now_wd` | 今地（不是同一实体、而是今天所在的行政区或遗址）在维基数据的地址 |

### people.json（155）

| 字段 | 说明 |
|---|---|
| `id` | 永久编号 |
| `name` | 名 |
| `dates` | 生卒：text 原样写法、from / to 数字年（公元前为负） |
| `role` | 身分，一句话 |
| `summary` | 小传 |
| `route` | 行迹：逐条记某年在某地做了什么，每条自带 cite |
| `cite` | 此人基本信息的出处 |
| `topics` | 出现在哪几期 |
| `name_en` | 英文名 |
| `sameas` | 维基数据地址（按中文名与生年对上） |

### events.json（393）

| 字段 | 说明 |
|---|---|
| `id` | 永久编号，形如 e317-00 |
| `year` | 年（公元前为负） |
| `to` | 止于某年，跨年的事才有 |
| `title` | 一句话说清这件事 |
| `type` | 类别：政治 / 营建 / 佛教 / 交通 等 |
| `place` | 地名原文 |
| `place_id` | 落到通用库的地点 id |
| `ll` | 单独给的经纬度，place_id 之外的补充 |
| `person_ids` | 牵涉到的人物 id |
| `cite` | 出处：grade 为 A—D，source 为书名篇卷，可带 quote 原文与 plain 白话 |
| `note` | 补注 |
| `unverified` | 本册尚未核实的，标 true |
| `topics` | 出现在哪几期 |

### works.json（263）

| 字段 | 说明 |
|---|---|
| `title` | 书名 |
| `aliases` | 别称 |
| `kind` | 类别：正史 / 行记 / 方志 / 类书 等 |
| `author` | 著者 |
| `era` | 成书年代 |
| `prefixes` | cite.source 里以什么开头算作此书 |
| `note` | 补注 |

## 引用 / Citation

COZLABS. 舆图集 · 通用库数据（Yutuji Historical Atlas — Open Data）, 版本 2026.09.28. Zenodo. https://doi.org/10.5281/zenodo.23010865

每个版本由 Zenodo 存档。上面这个 DOI 指「所有版本」，总解析到最新一版；要引某一版，用 Zenodo 页上那一版自己的 DOI。
Each release is archived on Zenodo. The DOI above covers all versions and resolves to the latest; each version also has its own DOI on Zenodo.

## 许可 / License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)：可以复制、改动、商用，署名并给出出处链接即可。
