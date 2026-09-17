# Performance — preview 0.5.2

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
