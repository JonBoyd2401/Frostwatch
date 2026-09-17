# Technical notes — Frostwatch preview 0.5.2

Frostwatch is an offline, single-player Windows fantasy adventure and an AI-led development experiment. This document describes the implemented preview, not a promise that every feature has production-game polish. See [AI development and measured resource use](AI-DEVELOPMENT.md), [performance](PERFORMANCE.md), [credits](CREDITS.md) and [distribution terms](DISTRIBUTION.md).

## Platform, architecture and development tools

- Current engine: Unreal Engine 5.8.2; Windows x64 Development build, DirectX 12 / Shader Model 6. Unreal Editor is not required by players. The predecessor used Godot 4.7.2; Godot rendering settings do not describe this Unreal build.
- Native C++ game module with engine input, JSON data, procedural mesh support, AI/navigation modules and RHI diagnostics. Editor-only authoring uses Unreal Python, editor scripting, asset import and generated static meshes.
- Data-driven world, quest/item/enemy definitions and terrain height samples accompany the authored Hearthmere map. Runtime systems cover character control, combat, quests, dialogue, settlements, travel, weather, menus and saves.
- Development automation uses Python and PowerShell; UnrealBuildTool builds the game/editor and AutomationTool cooks/stages packages. Iterative cooking, limited build parallelism and working caches on the development HDD reduce redundant work and SSD pressure.
- Git tracks source, configuration templates and authoring scripts locally. The public repository publishes the player documentation, screenshots and downloadable runtime. It does not expose the complete licensed source-asset library or Unreal Engine source.

## Rendering and memory

- Balanced retains Lumen lighting while using conventional shadows to reduce cost on the GTX 1060. High and Epic retain virtual shadow maps. This is deliberate per-preset selection, not an assertion that newer rendering features are always faster.
- Performance/Balanced use temporal anti-aliasing; higher presets use temporal super resolution. Resolution, fullscreen/window mode, render scale, frame cap and quality are player settings. The 0.4 tests used 720p; they are not 1080p performance claims.
- Explicit texture and Nanite geometry streaming budgets, temporary streaming allocations and lighting/render-target limits prevent the 3 GB GPU from being overcommitted. Runtime code overrides some scalability defaults; Balanced's effective texture budget is 384 MiB.
- Balanced permits finer texture mip levels than the prior version, with anisotropic filtering. Larger source textures do not mean all full-resolution texture data is resident at once.
- Instanced foliage, distance culling, terrain tiles and reduced distant wind deformation bound outdoor rendering work. Nearby foliage remains animated; Performance/Balanced stop foliage wind deformation beyond 80 metres.
- A 256 MiB packaged-asset read cache and 32 MiB read buffers use system RAM. The game already uses system RAM for CPU-side world/assets. This is not a RAM disk or an expansion of equally fast VRAM; GPU spill into shared memory can hurt performance. No isolated FPS gain is claimed for the cache.
- Diagnostics record mean/p95 frame times, graphics-memory usage/budget, texture streaming pressure, process RAM, live-world status and render errors. The memory budget is supplied by Windows and can vary with other applications.

## World, scenery and weather

- Authored terrain and regional dressing distinguish southern woodland, damp Glasswater, the snowy north and darker dragon territory. Some transitions and repeating surfaces remain visibly unfinished.
- Scenery combines owned Fab resources, credited CC0 assets and project-authored geometry/materials. Imported source art is converted to runtime assets and selectively cooked.
- The waterfall uses tharlevfx Water Materials base/arc meshes, tuned translucent water materials, foam/splash particles, a headwater surface, scanned rock surrounds, an irregular receiving pool and a basin carved into the terrain. It is an animated visual effect, not a fluid simulation. Demonstration walls/platforms are excluded.
- Sky, sun/moon and weather use a project controller and selected licensed sky/cloud resources. Fountains, local lights and night-time castle lighting are integrated, with screenshot checks in the courtyard and hall.
- Quest locations include towns, inns, caves, castles and travel camps. Procedural/authored collision, road clearance and interaction reachability are validated automatically; that is not a substitute for testing every possible player route.

## Character movement, NPCs and travel

- First-person movement includes walking, sprinting and jumping. Horse mounting, galloping and cart travel are available through world interactions.
- Townspeople use daily routines, walking routes and work interactions. This approximates village activity; it is not a fully simulated economy or autonomous generative-agent society.
- Character rigs and animations include licensed/retargeted clips. Civilian locomotion uses the credited Quaternius animation library. Some rigs, clips and procedural behaviours are reused.
- The two dragons use the owned PROTOFACTOR Mountain Dragon rig and original animation clips with separate material colours. Fire uses animated effects with softened billboard edges and depth fading, not volumetric combustion.

## Combat, death and respawn

- Light/heavy attacks, blocks, timed parries, dodge/recovery timing, attack buffering and chained directional cuts form the melee system. Recorded swing, metal contact and impact samples replace earlier synthetic combat tones.
- Selected finishing blows can sever prebuilt head/arm pieces. Blood/wound effects and animation/ragdoll responses do not constitute arbitrary mesh slicing or fully cinematic executions.
- Ordinary guards/orcs respawn after 24 campaign hours only when sufficiently distant from the player and outside visible arrival conditions. Checks include 80 metres from home and 25 metres from the corpse. Named bosses remain defeated, and quest defeat history is preserved.
- Settled corpses update less frequently to reduce unnecessary work. Save migration preserves older progression data.

## Campaign, interface and persistence

- Ten journal chapters, a guided opening, world map, interaction prompts, inventory/rewards and menus provide the adventure structure. The Last Ember story connects Edrin, supplies, the three oaths, Ste, Stu and the returned watchfire. Progress-aware dialogue and aftermath preserve existing save IDs and completion gates.
- A Canvas-rendered animated book presents the opening, found texts and journal; NPC dialogue slides up on parchment. A bundled Cormorant-derived serif face has its full SIL Open Font License and creator credit included. Long passages paginate with keyboard/mouse page controls; animations use real time while gameplay is paused.
- Castle detailing uses seven instanced groups for paving, vault ribs, standards and the Crown ward, plus eleven bounded spotlights, two with shadows. The lantern directs a bounded, wall-aware spotlight toward the path and reduces close-range glare. Castle architecture remains unfinished.
- Keyboard/mouse controls, rebinding, fullscreen/lower resolutions and quality settings are exposed in the interface. See README and the in-game controls screen for bindings.
- Saves reside in Frostwatch/Saved/SaveGames; settings are under Frostwatch/Saved/Config. Release ZIPs contain no personal save or settings files. Back up Saved before manually upgrading.
- Verification captures restore settings byte-for-byte and check save hashes. Local installation retains the previous executable/content packs for manual rollback.

## Audio and AI boundary

- Water/stream ambience is positional; music, footsteps, horse hoof sounds, combat contact, pain/death sounds and character dialogue use their credited sources and runtime playback/mixing.
- Current dialogue is pre-rendered, subtitle-matched Kokoro v1.0 neural speech with seven selected voice profiles/blends. It is synthetic speech, not hired actors. The model and authoring tools are not shipped.
- The game does not call a language model to generate NPC conversation during play. Dialogue and quests are authored; the player needs no AI account, API key or internet connection.
- Historical Piper narration and Godot-era notices are retained as provenance in the credits, but the old Piper tale recordings are absent from the 0.4 cooked asset inventory.

## Testing and publication

- The 0.5.1 package passed 71 campaign, 50 runtime and 72 combat/contact checks (193 total). The installed version repeated all 121 campaign/runtime checks. Both existing saves and settings remained byte-identical during installation.
- Current castle/lantern captures passed memory/render-error acceptance. Performance results and screenshots are in PERFORMANCE.md. These captures use stationary cameras, controlled weather and frozen NPC simulation. Long-session travel and active castle combat measurements remain outstanding. Book/page animation and text fit were checked separately, including a diagnostic second page and three viewport resolutions.
- Packaged content uses Unreal Pak/IoStore files. Runtime payload hashes match the verified local installation. ZIP integrity is checked and SHA-256 checksums accompany the download; GitHub upload digests are verified before publication.
- The download includes the runtime, launcher, Visual C++ redistributable and player/technical/credit documents. Editor tools, source art, personal saves/settings, debug symbols and build logs are excluded. Cooked configuration checks confirm private editor settings are absent.
- This is an unsigned development preview. It has been measured on one laptop; broad GPU/driver/platform compatibility, long-session stability and exhaustive playthrough coverage are not established. No multiplayer, console, Mac, Linux, mobile or browser build is supplied.

## Known limitations and interpretation

Landscape repetition, some shoreline geometry, grove roots/branches, reused animation and general composition still need work. A passing automated test establishes its specific assertions, not that the game is bug-free, balanced or AAA quality. The human review repeatedly exposed visible problems that automated checks missed. Frame rates vary with location, action, temperature, drivers and competing workloads. All third-party creators retain the rights stated in their licences.

## 0.5.2 readiness batch

Humanoids use a native single-sequence animation proxy with short blends from the last displayed local-bone pose. The incoming clip advances immediately; there is no second sequence evaluation. Compact-pose snapshots are invalidated when the required-bone mapping changes. Locomotion transitions use 180 ms and actions/reactions 90 ms. Dragons retain their previous animation player. This improves pose continuity; it is not a complete motion-matching system or a replacement for authored contact review.

Reading settings persist in GameUserSettings.ini. Story-body sizes of 100/125/150 percent rewrap and paginate; reduced motion removes the page and dialogue-slide animation. Headings, chapter-selection controls and the general HUD are not globally resized by this option. Separate audio-volume and full controller work remain on the roadmap.

Capture diagnostics additionally retain up to 120,000 post-warmup frame samples and report p99, worst frame, counts above 50/100 ms and peak dedicated-memory demotion. These metrics remain diagnostic-only. See PERFORMANCE.md for the actual moving test and its limits.
