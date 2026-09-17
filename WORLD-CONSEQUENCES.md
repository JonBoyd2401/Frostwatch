# Visible quest consequences — 0.5.4 preview

This verified, locally installed pass connects the existing supply-delivery and Edrin rescue flags to the visible world. It reuses existing assets and continues the release programme; broader acceptance remains open.

## Player changes

- Collecting a supply crate hides its scenery and interaction target. After Captain Rowan accepts both deliveries, the two crates appear near him in Hearthmere. Inspecting them explains that they stock the kitchens and stables.
- Edrin remains for the rescue conversation. After the player leaves the prison area and closes menus, he returns to Hearthmere and a notice explains where to find him.
- He follows a daytime routine by the stables and travels to the inn in the evening, retaining his existing model, animations and recorded dialogue.
- Existing save flags reconstruct the changes; a fresh expedition restores the original locations. A rescued Edrin remains available for conversation when an older save lacks the jailer defeat record. No save schema migration is needed.
- Supply actors keep static rendering. Transform updates happen only when their quest state requires a move, with mesh bounds used to ground their bases.

## Verification

245 packaged checks passed: 104 combat/save reliability, 91 campaign and 50 runtime. The campaign suite includes 20 new consequence checks covering collection/delivery visibility, repeated updates, rescue timing, occupied-arrival waiting and retry, route clearance, save reconstruction, fresh-game reset and static prop rendering. All test processes exited cleanly.

The final before/after delivery views, daytime mentor capture and evening inn capture passed their resource/render checks and were inspected. The live evening test reached the inn's resting state. The route is calculated from actual static collision in a bounded 61 × 49 Hearthmere grid, with 55 cm clearance for the 34 cm capsule, then simplified and cached. The planner is scoped to this settlement's shared floor height; wider NPC navigation remains separate work.

The live combat benchmark completed 2 parries and defeated its opponent with player health 100. It retains 24 gameplay samples and a final screenshot, with the 24 mid-fight PNG exports disabled to avoid distorting frame-time measurements. Gameplay is unchanged by that diagnostic option.

On the Omen, the scripted moving route used Balanced, 1280 × 720, 85% render scale, uncapped, live NPCs and controlled daylight with both deliveries completed and Edrin returned. After eight seconds of warmup it recorded 91.5 seconds: mean 73.0 FPS, p95 19.09 ms, p99 21.86 ms and worst 80.58 ms. There were 2 frames above 50 ms and 0 above 100 ms, with zero recorded GPU-memory demotion. This is one route, not whole-game or thermal-endurance acceptance. Capture mode disables normal autosaving.

Installation preserved 3 existing save/settings files byte-for-byte. Previous executable/packs are retained in DELETE-ME for manual rollback or removal.

## Memory changes and retained failures

Balanced uses a 1152-pixel Lumen surface-lighting cache instead of 1280. Lumen and the 384 MiB material texture pool remain enabled; Performance/Balanced temporary streaming batches are now 8 MiB instead of 16 MiB. High/Epic remain unchanged. The courtyard experiment retained visible lighting without a cache-capacity warning.

Earlier capture failures remain recorded. An editor run passed its campaign assertions but exceeded its shutdown timeout; clean packaged runs are the acceptance evidence. Initial cameras were obstructed, and the first evening capture changed only the sky clock. Those diagnostics were corrected. The live inn test then exposed a blocked legacy route, and a proposed shortcut failed collision clearance at a fence; the final collision-aware route completed the journey.

The first clear village capture spilled 44.95 MiB of GPU memory. Smaller streaming batches alone were insufficient. Further checks also found that removing PNG exports alone did not solve combat memory pressure. The final combination preserves static supply rendering, reduces the Balanced lighting cache and uses smaller streaming batches. Intermediate combat and route spills, including a 7.94 MiB route peak, are retained separately. GPU budgets varied between runs, so these are verification results rather than a controlled claim of a fixed memory saving or FPS uplift.

## Remaining work and cost

No new art downloads, purchases, paid services or voice recordings were required. Existing creator credits remain applicable. Castle/prison architecture, terrain and water authoring, further aftermath changes, broader NPC/prop interaction, controller and audio coverage, full fresh/old-save playthroughs and external player testing remain in RELEASE-READINESS.md.
