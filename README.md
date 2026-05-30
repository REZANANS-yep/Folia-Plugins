<h1 align="center">Folia Plugins</h1>
<p align="center">
  A curated directory of <a href="https://github.com/PaperMC/Folia">Folia</a> plugin ports, maintained and run in
  production by the <a href="https://suzeren.org">suzeren.org</a> Minecraft network.
</p>

<p align="center">
  <a href="https://pterohost.com">
    <img src="https://pterohost.com/images/branding/logo-sm.webp" alt="Pterohost - game server hosting with Folia and Paper support" height="64">
  </a>
</p>
<p align="center">
  <b>Эти форки развиваются и тестируются на <a href="https://pterohost.com">Pterohost</a></b><br>
  Игровой хостинг с нативной поддержкой Folia и Paper, мгновенный деплой и удобная панель управления.<br>
  <i>Developed and battle tested on <a href="https://pterohost.com">Pterohost</a> - game server hosting with first class Folia and Paper support.</i>
</p>
<p align="center">
  <a href="https://discord.gg/BayzJzArBa">Pterohost Discord</a>
  &nbsp;|&nbsp;
  <a href="https://suzeren.org">suzeren.org</a>
</p>

---

## What is this

[Folia](https://github.com/PaperMC/Folia) is the regionized, multithreaded fork of Paper. It is fast, but most
plugins are written for a single main thread and break on it, and the newest Minecraft builds (26.1.x) are too fresh
for many upstream releases. This is a list of **Folia compatible plugin forks** we maintain so our network keeps
working on Folia. Every fork keeps its original license and credits its upstream author. They are run in production
on a Folia backend and updated as needed.

If you are searching for a working **Folia plugin** for homes and teleportation, NPC commands, an economy, or a
scripting engine on Minecraft 26.1.2, start here.

## Plugins

| Plugin | What it does | Upstream | License | Status |
| --- | --- | --- | --- | --- |
| [HuskHomes-Folia](https://github.com/REZANANS-yep/HuskHomes-Folia) | Homes, warps, /tpa and cross-server teleportation | [William278/HuskHomes](https://github.com/WiIIiam278/HuskHomes) | Apache-2.0 | Production |
| [CitizensCMD-Folia](https://github.com/REZANANS-yep/CitizensCMD-Folia) | Run commands when a player clicks a Citizens NPC | [HexedHero/CitizensCMD](https://github.com/HexedHero/CitizensCMD) | GPL-3.0 | Production |
| [ExcellentEconomy-Folia](https://github.com/REZANANS-yep/ExcellentEconomy-Folia) | Unlimited custom currencies and a Vault economy | [nulli0n/ExcellentEconomy](https://github.com/nulli0n/ExcellentEconomy) | GPL-3.0 | Production |
| [Denizen-Folia](https://github.com/REZANANS-yep/Denizen-Folia) | The Denizen scripting engine | [DenizenScript/Denizen](https://github.com/DenizenScript/Denizen) | MIT | Experimental |
| [Denizen-Core-Folia](https://github.com/REZANANS-yep/Denizen-Core-Folia) | DenizenCore, required to build Denizen-Folia | [DenizenScript/Denizen-Core](https://github.com/DenizenScript/Denizen-Core) | MIT | Experimental |

Each repository uses the `folia` branch and explains exactly what was changed for Folia.

## Common Folia gotchas (from porting these)

A few patterns keep coming up when porting plugins to Folia and Minecraft 26.1.2, collected here in case they help:

- **Legacy `BukkitScheduler` is gone.** Move tasks to the global region scheduler (server wide), the entity scheduler
  (per player or per entity), or the async scheduler (off-main work). Tick delays become real time on the async scheduler.
- **Bundled helper libraries misdetect new versions.** Older PaperLib falls back to a synchronous teleport that Folia
  rejects with `Must use teleportAsync`. Calling Paper's native `teleportAsync` / `getChunkAtAsync` fixes it.
- **NMS version locked plugins self-disable on 26.1.2.** Prefer version agnostic approaches (for holograms, the
  Display-entity based ones keep working across versions).
- **Shaded dependency drift.** Switching a module from spigot-api to paper-api can pull a newer adventure serializer
  while the api stays old, causing a `NoClassDefFoundError`. Pin adventure with its BOM.

## Credits

These are unofficial forks. All credit for the original plugins goes to their respective authors, linked in the
table above. Maintained by [suzeren.org](https://suzeren.org), developed on [Pterohost](https://pterohost.com).
