# Roads and castle surroundings — 0.5.6 preview

The existing road network now fades into wider worn-ground shoulders. Its rocky-soil texture mixes two scales and orientations, with subtle wheel tracks and larger tonal variation to reduce the obvious repeated strip. The thin road surface no longer casts a separate shadow onto the terrain underneath. Ground heights and route data are unchanged.

The castle approach gains 200 small grass, dead-shrub and rock instances in 4 shared mesh groups. These are clustered winter verges using existing library assets, with bases fitted against multiple ground samples and protected road/building clearances. Decorative planting has no collision, culls at distance, and adds no lights. This is a focused environmental pass; it does not rebuild the whole map, finish the castle, add terrain displacement, or revise the waterfall.

252 packaged campaign, runtime, combat and save checks passed. Actual before/after village-road and castle captures, an aerial view and a nighttime view were inspected. Balanced captures use 1280 × 720 at 85% render scale; a separate Performance village view uses 100%. Resource and render checks passed. The moving-route regression recorded 287.6 metres and 91.5 measured seconds after warmup, with zero recorded GPU-memory demotion. See PERFORMANCE.md for frame times and limitations.

Installation preserved 4 player save/settings files byte-for-byte. Existing creator assets/materials and their credits are retained; no asset purchases, new downloads or paid services were used. The previous payload is retained in DELETE-ME for manual removal. Automated coverage and AI visual inspection do not replace an ordinary full campaign playthrough or external player testing.
