# Village livestock — 0.5.8 preview

Hearthmere, Brackenford and Eastmere now each have two cows, two pigs and two sheep near their village herder's workplace. The existing horses, carts and stable hands remain. Cattle and pigs use textured 0 A.D. models by Wildfire Games contributors; the sheep uses p0ss's rigged, textured sheep. These are modest game models with natural animal proportions, not photogrammetry scans or a claim of AAA animal fidelity.

Animals use separate skeletal idle, walk and feeding animations. They graze between short, bounded walks, turn before moving and trace the terrain before taking a step. Collision stops them at obstacles. Herder work routes visit the clear pasture areas; tending causes nearby animals to stop and feed. Villagers retain their existing evening and home routines. This adds ambient farming behaviour, not an animal husbandry economy, harvesting or new quests.

Herds are limited to 18 animals across the map. Beyond 90 metres their movement pauses and logic updates once a second; animation poses update only when rendered. Textures are capped at 1024 pixels, and existing scene lighting is reused.

279 packaged regression checks passed, including the three-species population, compatible animation clips and repeated tending behaviour. Four packaged game captures were inspected. The first moving-route run recorded a brief 3.84 MiB GPU-memory demotion and a 302.9 ms worst frame. A repeat of the same route ran for 91.5 seconds with 2.91 MiB peak demotion and a 295.6 ms worst frame. Both ended without an over-budget state, but brief traversal hitches remain unresolved. Both runs and their limits are documented in PERFORMANCE.md. Installation preserved 4 player save/settings files byte-for-byte. These automated checks do not establish a full ordinary-play campaign or all farmer routes over a complete day.

No assets were purchased. See [creator credits](CREDITS.md), [animal licence notice](Licenses/Livestock-Attribution.md), and the [adapted reusable animal assets](Assets/Livestock/README.md). The animals and their adaptations retain CC BY-SA 3.0; unrelated Fab assets keep their existing restrictions.
