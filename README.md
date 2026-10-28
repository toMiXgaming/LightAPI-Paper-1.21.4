# LightAPI for Paper 1.21.4

A port of [LightAPI 5.3.0](https://github.com/BeYkeRYkt/LightAPI) by BeYkeRYkt (archived, last supported version 1.19) to **Paper 1.21.4**.
LightAPI lets plugins create invisible dynamic light sources, for example muzzle flashes in
QualityArmory.

## What changed compared to upstream

- New module `craftbukkit-nms-v1_21_R3`: a handler for Paper's built-in Starlight (Moonrise), Mojang-mapped.
- Light removal is applied synchronously and reported as `SUCCESS`, so the scheduler sends the update to players
  (otherwise the light stayed visible on clients until the next change).
- `HandlerFactory` picks the handler from the Minecraft version, because Paper no longer relocates CraftBukkit.
- bStats metrics removed. In debug mode, calls to the legacy API are logged together with their caller.
- **Paper only** (not Spigot, not other versions).

## Install

Download `releases/LightAPI-5.3.0-paper-1.21.4.jar` and put it in `plugins/`.
Plugins using the old `ru.beykerykt.lightapi` package need `force-enable-legacy: true` in `plugins/LightAPI/config.yml`;
plugins using the new API (e.g. QualityArmory 2.1.x) work without it.

## Build

Start a Paper 1.21.4 server once in some directory, then:

    PAPER_DIR=/path/to/that/server ./build.sh

Output: `build/LightAPI-5.3.0-paper-1.21.4.jar`. Needs JDK 21.

## Testing

Tested on Paper 1.21.4 build 232 with a headless client (mineflayer) reading light levels the way a real client
does, using both the new and the legacy API, including rapid create/delete cycles. Not tested with other plugins
that manipulate lighting (FAWE, etc.).

## License

MIT, see `LICENSE`. Original work by Vladimir Mikhailov (BeYkeRYkt) and contributors.
