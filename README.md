# Emerald DS Edition — Milestone 0

This is a **native Nintendo DS / DSi homebrew UI prototype**, not a port of Pokémon Emerald yet. It contains original placeholder text graphics, a movable player marker, and a touch-controlled second screen. It does **not** contain a Pokemon ROM, Nintendo assets, music, story or save format.

## Build (Windows)

1. Install [devkitPro](https://devkitpro.org/wiki/Getting_Started) with **Nintendo DS development** packages (`nds-dev`).
2. Open the **devkitPro MSYS2** shell (not a generic Windows command prompt).
3. Extract the project ZIP, `cd` to this folder, and run `make`.
4. If successful, copy `EmeraldDS_Prototype.nds` to your DSi SD card, launch via TWiLight Menu++.

On Linux, install `nds-dev` through devkitPro pacman, load the devkitPro environment, then run `make`.

## Controls

- D-pad: move `@` around the top screen.
- B: toggle walk/run.
- Touch bottom-screen rows: switch between Map, Party, Bag, Pokédex placeholders.

## Next milestones

1. Verify this demo builds, boots, displays both screens, and touchscreen taps work on real DSi XL hardware.
2. Replace upper-screen console with real tile/sprite rendering and a 240x160-centered or expanded 256x192 scene.
3. Define hardware abstraction layers for input, audio, graphics, save and timing.
4. Study `pret/pokeemerald` subsystems and port one vertical slice (map movement with sprites/tiles), **not** the entire GBA hardware interface at once.
5. Add data conversion pipelines for legally sourced game assets, then battle/UI integrations.

## Notes

DS mode normally has roughly 4MB of main RAM, even on a DSi launched as a standard DS title. DSi-specific mode needs additional packaging and validation and should not be assumed here. Avoid assuming the GBA original builds as an NDS project without major changes.

Source: `https://github.com/devkitPro/nds-examples` for libnds build patterns; `https://github.com/pret/pokeemerald` is the upstream GBA decompilation, **not integrated** into this milestone.

## Build on an iPhone — GitHub Actions (no computer needed)

The repository has a workflow at `.github/workflows/build-nds.yml`.
It uses a pinned official devkitPro toolchain image and runs `make` remotely.

1. Sign in to GitHub in Safari and create a **new repository**, e.g. `emerald-ds-edition`.
2. Add the files and folders from this package to the repository **root**. Keep `.github/workflows/build-nds.yml` in exactly that path. A reliable mobile-friendly option is to use **github.dev** (open your repo, then change `github.com` to `github.dev`) to upload the extracted files and commit them; depending on the browser, uploading the hidden `.github` directory may require creating the workflow file through GitHub's normal **Add file → Create new file** screen instead.
3. On GitHub, open **Actions → Build Emerald DS prototype → Run workflow**. If Actions requires enabling workflows for the repo, enable it first. A push to `main` or `master` also builds automatically once workflows are enabled.
4. Open the successful workflow run and download **EmeraldDS_Prototype_NDS** under **Artifacts**. GitHub downloads an artifact ZIP containing `EmeraldDS_Prototype.nds`.
5. Extract it in iPhone Files, then use your usual iPhone-to-SD transfer method to place `.nds` on the DSi SD card, and launch via TWiLight Menu++.

GitHub Actions is a remote compiler, **not** a DS emulator. Passing the workflow means only that the ROM built successfully; boot, graphics, controls, and touchscreen still need testing on your hardware. If the run fails, copy the error log into ChatGPT so we can patch it.
