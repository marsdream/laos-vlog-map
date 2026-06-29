# 琅勃拉邦行旅图 / Laos Vlog Map

老挝三城 vlog 漫游地图 — Day 1 古城、Day 2 万荣户外、Day 3 万象。

Fork 自 [dracohu2025-cloud/China_pins](https://github.com/dracohu2025-cloud/China_pins) 的「东坡行旅图」，复用其 MapLibre GL + 自烘 relief + DOM marker 范式，改造为 vlog POI 叙事。

## 试跑版

边界 GeoJSON 仍是中国（先跑通 POI 布局、marker 形态、点击交互）。
老挝边界 + 老挝 relief 重烘在 Roadmap。

## 数据

- `data/laos-journey.json` — 8 个 POI：琅勃拉邦 3 / 万荣 2 / 波罗芬 1 / 万象 2
- `data/people/index.json` — 章节索引（已加 laos-vlog 默认）

## 本地预览

```bash
python3 -m http.server 5173
# 打开 http://127.0.0.1:5173/
```

## 部署

Vercel（继承 China_pins 范式）：
```bash
npx vercel@44.0.0 --prod --yes
```
