# Performance — preview 0.5.9

## New moving and combat checks

The packaged build passed 78 combat/contact/pose checks, 71 campaign checks and 50 runtime checks (199 total). Its live parry/counter encounter passed with 2 parries and the enemy defeated. These checks remain distinct from a human playthrough.

A controlled movement capture through woodland and the northern road toward the castle on the same Omen used Balanced, 1280×720, 85% render scale, live NPC simulation, no frame cap and benchmark invulnerability. The player was 273.6 metres from the scripted starting point when graphics were sampled. The complete measured interval below discards the first eight seconds of frame tracking; it is longer than the previous final-600-frame samples but does not cover the whole campaign or mounted travel. The walk log continues briefly after the graphics snapshot, so its final distance is not used as the measured endpoint here.

| Moving capture measurement | Result |
| --- | ---: |
| Measured duration | 91.5 seconds |
| Mean FPS | 69.8 |
| p95 frame time | 19.19 ms |
| p99 frame time | 23.01 ms |
| Worst frame | 74.87 ms |
| Frames over 50 ms | 3 |
| Frames over 100 ms | 0 |

This is measurement coverage, not a claimed performance improvement. No matching old-build moving-session baseline was recorded. Review slow frames separately from average FPS. Larger-text/reduced-motion UI captures were also checked at 960×540; those are layout checks, not gameplay benchmarks.

## Historical 0.5.1 castle and night-path samples

The following measurements remain explicitly historical; they have not been relabelled as a new 0.5.2 benchmark.

Measured on GTX 1060 3 GB, Core i7-8750H and 32 GB RAM. These historical captures use Balanced, 1280 × 720 output, 85% render scale, no frame cap and VSync off. Cameras are stationary, NPC simulation is frozen, weather is controlled, and each sample reports the final 600 frames. These are rendering regression checks, not moving-gameplay or minimum-FPS guarantees.

| Scene | Mean FPS | p95 frame time |
| --- | ---: | ---: |
| Castle approach | 87.5 | 13.38 ms |
| Castle gate | 85.4 | 13.82 ms |
| Castle courtyard | 79.0 | 15.69 ms |
| Castle great hall | 77.1 | 15.52 ms |
| Woodland night path, lantern off | 40.9 | 30.62 ms |
| Woodland night path, lantern on | 40.3 | 30.45 ms |
| Close-character lantern check | 37.5 | 30.48 ms |

The previous local courtyard sample was 91.0 FPS and the hall was 105.3 FPS under matching conditions. The richer castle costs performance. The woodland remains below 60 FPS and needs further work. Lantern on/off samples do not establish a performance gain from the lighting change. All listed checks passed graphics-memory acceptance; the accepted captures reported no render errors.

Balanced retains Lumen lighting and uses conventional shadows, a 384 MiB texture streaming budget, finer permitted texture mips and reduced distant foliage wind work. High and Epic retain virtual shadows. A 256 MiB asset-read cache and 32 MiB read buffers use system RAM; no isolated FPS gain is attributed to caching.

193 packaged gameplay checks passed: 72 combat/contact, 71 campaign and 50 runtime. The installed build then repeated the 71 campaign and 50 runtime checks successfully. These assertions do not replace a full fresh-save playthrough, sustained travel/combat profiling or testing on other hardware. Book/parchment layouts were checked at 960×540, 1280×720 and 1920×1080; these UI checks are not gameplay performance benchmarks.

Architecture, terrain/road repetition, shoreline transitions, abrupt enemy animation changes and sustained performance remain open work. This is a development preview, not a finished AAA release. The older 0.4 measurements in repository history used different live-world conditions and must not be presented as current 0.5.1 results.

![Castle approach](Screenshots/castle-approach.png)
![Castle courtyard](Screenshots/castle-courtyard.png)
![Great hall](Screenshots/castle-hall.png)
![Daylight aerial view showing remaining architecture work](Screenshots/castle-aerial.png)

## 0.5.3 scope

The first combat review recorded 9.293 MiB of transient GPU-memory demotion and failed resource acceptance. Reducing temporary texture replacement memory from 32 to 16 MiB passed the same review with no demotion under a nearly identical roughly 2,009 MiB GPU budget. The texture pool and quality settings are unchanged. The smaller batch is now the Performance/Balanced default. The 24 screenshot captures in the combat review create blocking stalls and are not a gameplay FPS benchmark.

A final moving-route test on the Omen i7-8750H / GTX 1060 3 GB / 32 GB RAM used Balanced, 1280 × 720, 85% render scale, uncapped, live NPCs, controlled daylight and scripted benchmark-invulnerable movement. After eight seconds of warmup it recorded 91.4 seconds and approximately 274 metres to the graphics snapshot. Mean 67.7 FPS; p95 19.40 ms; p99 22.66 ms; worst 95.46 ms; 1 frames above 50 ms and 0 above 100 ms. Peak recorded demotion was zero. This is one route, not an entire-game or thermal-endurance guarantee, and not a controlled claim of improved FPS against a previous release.

Save writes now include backup and readback I/O. Capture mode disables normal autosaving, so this moving test does not measure save latency. Packaged storage regression tests separately exercised real diagnostic-slot I/O and simulated failures. Older figures above remain dated 0.5.2/0.5.1 measurements.

## 0.5.4 regression scope

This update reuses two scenery actors and one existing NPC. Balanced reduces the Lumen surface-lighting cache from 1280 to 1152 pixels per side. Lumen remains enabled and the 384 MiB material texture pool is retained. Performance/Balanced temporary streaming batches are reduced from 16 to 8 MiB; High/Epic settings are retained. On the Omen, the same scripted moving route used Balanced, 1280 × 720, 85% render scale, uncapped, live NPCs and controlled daylight, with deliveries completed and Edrin returned. After eight seconds of warmup: 91.5 seconds, mean 73.0 FPS, p95 19.09 ms, p99 21.86 ms, worst 80.58 ms, 2 frames over 50 ms and 0 over 100 ms. Peak recorded GPU-memory demotion was zero. This is a route regression check, not a whole-game or thermal-endurance guarantee. Diagnostic capture mode disables normal autosaving.

The live combat benchmark retained 24 gameplay samples but disabled the 24 mid-fight PNG exports; it still captured a final image. Two parries and an enemy defeat passed with player health 100. Its post-warmup interval recorded mean 56.9 FPS with the 60 FPS cap, p95 20.01 ms and worst 35.63 ms, with no frames above 50 ms. Peak recorded GPU-memory demotion in this final run was 0.00 MiB. Initial failing memory captures are documented in WORLD-CONSEQUENCES.md. Supply actors now preserve static rendering instead of unnecessarily rebuilding both as movable objects at startup.

## 0.5.5 castle regression

Six added actors total 1,164 triangles and add no lights. Day/night castle views passed the recent-window texture/GPU-memory guards at Balanced, 1280 × 720 and 85% render scale on the Omen. These are stationary capture checks. The separate live combat regression, with a 60 FPS cap and no intermediate PNG exports, recorded 21.5 seconds after warmup: mean 56.9 FPS, p95 20.11 ms, worst 31.39 ms, 0 frames above 50 ms and peak recorded GPU-memory demotion 0.00 MiB. This does not measure a full castle battle, moving-route endurance or save latency. The earlier 0.5.4 moving-route results remain dated evidence, not a new 0.5.5 route test.

## 0.5.6 world regression

The road material adds two texture samples using existing textures; 200 decorative instances share four mesh groups with 55–90 metre culling. No new lights. On this Omen at Balanced, 1280 × 720, 85% render scale, uncapped and with the live world enabled, the moving woodland/northern-road regression recorded 91.5 seconds after warmup and 287.6 metres of travel: mean 68.9 FPS, p95 19.50 ms, worst 67.58 ms, 2 frames above 50 ms, and peak recorded GPU-memory demotion 0.00 MiB. Whole-capture measurements are used rather than the final short window. This route does not cover the entire map or castle battle, mounted travel, save latency or other PCs. Stationary castle/day/night and village captures passed memory guards; they are not evidence of a whole-game FPS improvement.

## 0.5.7 exploration regression

On the development Omen, Balanced, 1280 × 720, 85% render scale, uncapped with the live world enabled: the woodland/northern-road run covered 287.9 metres and recorded 91.5 seconds after warmup. Mean 71.0 FPS, p95 18.83 ms, p99 21.86 ms, worst 109.13 ms; 2 frames above 50 ms, 1 above 100 ms, peak recorded GPU-memory demotion 0.00 MiB. These are whole-capture results. Separate stationary cave/water views passed resource guards. The route is not a moving cave endurance test, full-world benchmark or other-hardware guarantee.

The close view directly beneath the waterfall averaged 44.7 FPS (p95 24.26 ms), with no recorded over-budget state in that capture. The water layers are a heavier local view than the cave interiors. An earlier rejected candidate recorded 230.46 MiB of peak GPU-memory demotion on the moving route. The accepted run above follows bounded cave draw distances and reduced per-section Lumen card counts; the initial failure is retained locally rather than treated as a passing run.

## 0.5.8 livestock regression

On the same Omen (i7-8750H, GTX 1060 3 GB, 32 GB RAM), Balanced, 1280 × 720, 85% render scale, uncapped, controlled daylight and live NPC simulation, the same stationary farm camera was measured before and after the herd addition. Measurements exclude the first eight seconds. No asset builds ran during these captures.

| Whole-capture measurement | Installed 0.5.7 | Livestock 0.5.8 |
| --- | ---: | ---: |
| Measured seconds | 51.5 | 51.5 |
| Mean FPS | 39.9 | 39.8 |
| p95 frame time, ms | 28.10 | 27.91 |
| p99 frame time, ms | 31.08 | 30.41 |
| Peak GPU-memory demotion, MiB | 0.00 | 0.00 |

The farm is a dense local view; the herd and NPC poses vary between runs. These single runs do not establish a statistically reliable FPS improvement.

Two woodland/northern-road moving runs used the same settings and scripted route. The repeat used the installed identical payload, following the first candidate-package run. No rendering settings or assets changed between these runs.

| Whole-route measurement | First run | Repeat |
| --- | ---: | ---: |
| Measured seconds | 91.5 | 91.5 |
| Mean FPS | 70.1 | 66.0 |
| p95 frame time, ms | 18.93 | 19.94 |
| p99 frame time, ms | 22.33 | 23.09 |
| Worst frame, ms | 302.86 | 295.61 |
| Frames above 50 ms | 3 | 2 |
| Frames above 100 ms | 1 | 2 |
| Peak GPU-memory demotion, MiB | 3.84 | 2.91 |

Both runs contain brief demotion and hitches; these remain unresolved preview limitations. Neither ended in an over-budget state. The final-window GPU budgets were 1990.3 and 2017.9 MiB respectively, so these are not identical resource conditions. No specific cause or performance improvement is inferred. These are limited regression routes, not whole-map, mounted-travel, saving, thermal-endurance or other-hardware acceptance. Diagnostic capture mode disables normal autosaves.

## 0.5.9 cave and outdoor traversal

On the development Omen (i7-8750H, GTX 1060 3 GB, 32 GB RAM), Balanced, 1280 × 720, 85% render scale, uncapped with live NPC simulation and controlled daylight. The cave run uses the lantern. No builds or asset imports ran during either capture. Whole-capture figures exclude the first eight seconds; normal autosaves are disabled in diagnostic capture mode.

| Whole-capture measurement | Woodland/northern road | Hollow descent |
| --- | ---: | ---: |
| Measured seconds | 91.5 | 101.5 |
| Mean FPS | 70.6 | 62.6 |
| p95 frame time, ms | 19.31 | 27.86 |
| p99 frame time, ms | 22.44 | 39.75 |
| Worst frame, ms | 61.65 | 654.46 |
| Frames above 50 ms | 1 | 4 |
| Frames above 100 ms | 0 | 1 |
| Peak GPU-memory demotion, MiB | 0.00 | 0.00 |

Neither capture ended in an over-budget state. Whole-session demotion and slow frames are reported above even when the final resource check passes. An earlier candidate failed the outdoor memory guard with 29.58 MiB peak demotion, 8.83 MiB recent demotion and a 669.95 ms worst frame. A subsequent run still failed with 15.07 MiB peak and 12.78 MiB recent demotion despite the coarser tunnel distance fields. The final revision also reduced the Performance/Balanced Nanite streaming pool from 64 to 32 MiB before repeating the measurements above; texture pools and the verified Lumen atlas size were retained. These are observed revisions and measurements, not an isolated attribution of every change in frame time. These are two limited regression routes, not whole-map, mounted travel, saving, thermal-endurance or other-hardware acceptance. There is no matched earlier cave-walking baseline, so no measured FPS improvement is claimed. Earlier 0.5.8 hitches remain part of the historical evidence. Seven separate stationary views checked the cave exteriors, passages and waterfall pool; stationary camera results are not walking performance guarantees.
