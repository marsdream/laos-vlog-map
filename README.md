# 琅勃拉邦行旅图 / Laos Vlog Map

老挝三城 vlog 漫游地图 — Day 1 琅勃拉邦古城 · Day 2 万荣户外 · Day 3 万象。

Fork 自 [dracohu2025-cloud/China_pins](https://github.com/dracohu2025-cloud/China_pins) 的「东坡行旅图」，复用 MapLibre GL + 自烘 relief + DOM marker 范式，改造为 vlog POI 叙事。

## 在线版

**https://laos-vlog-map.vercel.app/**

## 数据

- **19 个真实 POI**（数据源：Lonely Planet + Wikipedia + 维基常识）：
  - **Day 1 琅勃拉邦 (9)**: 香通寺 / 普西山 / 皇宫博物 / TAEC / Phosi 早市 / 光西瀑布 / Living Land / 巴乌石窟 / LP 夜市
  - **Day 2 万荣 (4)**: 长廊石窟 / 蓝泻湖 / Pha Ngern 观景台 / 南松河
  - **Day 3 万象 (6)**: 塔銮 / 凯旋门 / 西刹吉寺 / 玉佛寺 / 佛像公园 / COPE 中心 / 万象夜市
- **6 国边界 GeoJSON**（老挝/中国/越南/泰国/缅甸/柬埔寨），194KB，Douglas-Peucker 简化
- **relief 瓦片复用** China_pins 原 z0-z3 全球 + z4-z6 中国中纬度（含老挝大部分）

## 技术改动（相对 China_pins）

1. **数据** — `data/laos-journey.json` 19 POI，bounds `[[100, 14], [108, 22]]`
2. **边界** — `geo/100000_full.json` + `geo/china-outline.json` 替换为中南半岛 6 国
3. **relief bounds** — `REGIONAL_RELIEF_TILE_BOUNDS` / `DEM_BOUNDS` 调整为 `[95, 25, 110, 13]`
4. **app.js** —
   - `addChinaLayers` 改为 6 国 MultiPolygon 合并 fill；移除 prov-line（不需要省级细节）
   - 6 国国名 label 写在固定中心点（不依赖 feature center）
5. **types 分类**：heritage / temple / nature / outdoor / night / morning / museum / landmark

## Roadmap

- [ ] 烤 z=6 (49-51, 29) 老挝南端 3 个缺瓦片（跑 `bake:relief` 改 bounds）
- [ ] gadm41 老挝省级边界（万荣省/琅勃拉邦省/万象市分隔线）
- [ ] 老挝河湖（湄公河主流/南乌河/南松河，目前仍是 ne_50m_rivers_cn 中国河）
- [ ] B 站真实 cid 替换占位 `BV1xxxxxx`
- [ ] 替换仿古纸纹理 → 现代暗色主题（vlog 风格）

## 本地预览

```bash
python3 -m http.server 5173
# 打开 http://127.0.0.1:5173/
```

## 部署

Vercel（继承 China_pins 范式）：
```bash
npx vercel@latest deploy --prod --yes --token $(cat ~/.openclaw/credentials/vercel_token.json | python3 -c 'import json,sys; print(json.load(sys.stdin)["vercel_token"])')
```

## 致谢

- 原始范式：[dracohu2025-cloud/China_pins](https://github.com/dracohu2025-cloud/China_pins) — MapLibre + 自烘 relief + DOM marker 的开源范式
- 地形数据：[AWS Open Data Terrain Tiles / Terrarium](https://registry.opendata.aws/terrain-tiles/)
- 国境边界：[Natural Earth](https://www.naturalearthdata.com/) + [datasets/geo-countries](https://github.com/datasets/geo-countries)
- POI 数据：Lonely Planet + Wikipedia
