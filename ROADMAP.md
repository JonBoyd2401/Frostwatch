# Player-first release programme

Authorised 17 September 2026: complete the production recommendations economically, with no purchases. Reuse existing art, animation, audio, authoring and diagnostics. Prioritise a convincing complete journey over expanding scope. Do not label this programme complete solely because automated checks pass.

## Work and acceptance ledger

| Workstream | Required result | Current status |
| --- | --- | --- |
| First hour and guidance | Arrival, Rowan, first combat, discovery and meaningful reward understandable without coaching | Existing opening/story; uncoached player test outstanding |
| Complete campaign | Fresh save reaches ending; older saves continue; objectives/rewards/world agree | Automated campaign coverage exists; full ordinary-play acceptance outstanding |
| Combat motion | Continuous locomotion/action/reaction transitions, unchanged contact timing, recognisable openings | 0.5.2 short pose transitions passed 78 packaged checks and a live parry/counter sequence; broader enemy/animation review remains |
| Enemy encounters | Distinct tactics, fair group pressure, readable commitment and recovery | Existing two-attacker limit/committed swing; further encounter review outstanding |
| Sustained performance | Moving travel, riding, combat, loading and saving measured for spikes and streaming | 0.5.2 records whole-capture p95/p99/stalls; 91.5-second woodland/northern-road run measured; 0.5.3 also verifies 16 MiB temporary streaming batches with zero recorded demotion in the fight and moving route; 0.5.4 adds static supply rendering, a 1152-pixel Balanced lighting cache and 8 MiB temporary batches, with a verified moving-route regression; mounted travel and longer campaign profiles remain |
| Castle and prison | Believable architecture, readable route, secure prison, meaningful exploration | 0.5.5 verifies barred prison/gate save behaviour and gatehouse gallery; keep, connected walkways and wider architectural acceptance remain |
| Terrain and water | Grounded scenery, road shoulders, upstream/downstream continuity, regional ground identity | 0.5.6 verifies softer roads and wider shoulders across the existing network, plus focused castle-approach winter verges; wider regional composition and water continuity remain |
| World consequences | Rescued people relocate, deliveries appear, restored places react consistently | 0.5.4 verifies collected/delivered supply props, Edrin returning, collision-aware inn travel and old/new-save reconstruction; further aftermath changes remain |
| Save reliability | New/old saves, interrupted update, death/checkpoint, boss persistence and ordinary respawn tested | 0.5.3 packaged checks verify writes, previous-generation recovery, simulated storage failures and real diagnostic-slot I/O; full ordinary-play and interruption scenarios remain |
| Interface/accessibility | Text size, reduced motion, shake/bob controls, subtitles, separate audio levels, clear failed-action feedback | 0.5.2 adds 100/125/150% story body text and reduced page/dialogue motion, verified at 960×540; audio/general-HUD controls remain |
| Input | Keyboard/mouse complete; controller only advertised after full navigation/gameplay verification | Controller acceptance outstanding |
| Audio | Recurring actions and major dialogue reviewed for matching contact, pronunciation and level | Recorded combat and synthetic dialogue exist; complete listening review outstanding |
| Compatibility and external playtest | Uncoached new players and several real PCs tested | Requires real testers/hardware; cannot be certified on this laptop alone |
| Publication | Verified runtime, matching screenshots/docs, credits, checksums and honest known issues on GitHub | 0.5.6 roads/castle-surroundings candidate verified and installed on 18 September; publication and anonymous checksum checks must complete before this batch is closed |

## Cost and verification rules

- No asset purchases, paid services, new hardware or paid testers without explicit financial approval.
- Use D: for working assets/builds. Preserve saves and settings. Move obsolete output to DELETE-ME for manual removal.
- Compile/test focused code changes before expensive cooking. Combine verified changes into release candidates to reduce repeated packaging and uploads.
- Capture real gameplay evidence; keep stationary/frozen diagnostic measurements clearly labelled. Never claim whole-game FPS from one scene.
- Keep the installed verified release playable until a replacement passes verification. Publish completed candidates using PUBLIC-RELEASE-WORKFLOW.md.
- External playtesting is an acceptance dependency, not something to fabricate or replace with AI-generated opinions. Prepare a reproducible test brief and record actual observations when available.
