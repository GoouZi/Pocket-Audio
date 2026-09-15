# Pocket Audio

[简体中文](README_CN.md)

**Pocket Audio** is a browser-based music ROM builder and player for the **Game Boy Advance**.

The goal is to make creating a GBA music ROM feel like using a small music-authoring tool: import ordinary audio files, prepare metadata, artwork and synchronized lyrics, preview the player, then generate a standalone `.gba` ROM that can run in an emulator or on real hardware.

> **Project status:** Active development. Functional on real GBA hardware, but not yet a stable public release.

## Real hardware

Pocket Audio is already running on a real Game Boy Advance through a flash cartridge. The current ROM player supports the core music-player interface, artwork, playback controls and track information.

<p align="center">
  <img src="docs/images/pocket-audio-player.png" alt="Pocket Audio running on a real Game Boy Advance" width="820">
</p>

<p align="center"><em>Pocket Audio player running on real GBA hardware.</em></p>

## What is already implemented

### Browser-based ROM builder

The current builder can:

- Import multiple songs.
- Accept common audio formats such as MP3, WAV, OGG, FLAC and M4A/AAC when supported by the browser.
- Read supported song metadata and embedded artwork.
- Edit title and artist information.
- Add, replace or remove cover artwork.
- Reorder or remove tracks.
- Preview the GBA player at its native **240×160** resolution.
- Estimate track size and final ROM size.
- Generate a standalone `.gba` ROM directly in the browser.
- Detect when a project would exceed the standard **32 MiB GBA ROM limit**.

The preview is intentionally designed around the ROM rather than as a generic web music player. The goal is for transitions, text movement, controls and lyric behavior in the builder to stay as close as possible to the final GBA output.

### Audio playback

Pocket Audio currently converts imported audio into data suitable for **GBA Direct Sound PCM** playback instead of attempting to decode modern desktop codecs on the console itself.

Current output presets are:

| Setting | Intended use |
| --- | --- |
| 11 kHz | Smaller ROM size |
| 16 kHz | Recommended balance |
| 22 kHz | Higher audio quality |

This keeps the runtime simple and predictable while moving the expensive conversion work to the browser.

### Synchronized lyrics

Pocket Audio can package synchronized lyrics into the generated ROM.

Current lyric inputs include:

- `.lrc`
- `.srt`
- `.txt`

The builder preprocesses lyric timing and rendering data before ROM generation. The GBA player has a dedicated lyrics screen and follows the current playback position.

<p align="center">
  <img src="docs/images/pocket-audio-lyrics.png" alt="Pocket Audio synchronized lyrics running on a real Game Boy Advance" width="820">
</p>

<p align="center"><em>Synchronized lyrics running on real GBA hardware.</em></p>

### Multi-song playback

Multi-track ROMs currently support:

- Playlist loop
- Single-track loop
- Shuffle

`SELECT` changes the playback mode when more than one song is present.

For a ROM containing only one song, Pocket Audio removes the unnecessary mode UI and mode-switching logic: the mode icon is hidden, `SELECT` does not cycle modes, and playback stops/pauses after the song finishes.

### Player behavior and UI

Current player work includes:

- Play / pause.
- Previous / next track.
- Seeking.
- Album artwork.
- Track title and artist display.
- Scrolling text for long metadata.
- Album-art-derived background presentation.
- Track-change transitions.
- Dedicated lyrics view.
- Playback-mode indication for multi-song ROMs.
- Browser preview behavior matched closely to the ROM.

## Current controls

| Control | Action |
| --- | --- |
| `A` | Play / pause |
| `B` | Open / close lyrics |
| `Left / Right` | Seek backward / forward |
| `L / R` | Previous / next track |
| `SELECT` | Change playback mode in multi-song ROMs |

Controls may still change during development.

## How it works

Pocket Audio performs most heavy work before the ROM ever reaches the GBA:

1. Import and decode the source audio in the browser.
2. Read available metadata and artwork.
3. Prepare cover, background and text assets.
4. Parse and preprocess synchronized lyrics.
5. Convert audio to a GBA-friendly PCM representation.
6. Pack songs and assets into the player data archive.
7. Build and download a ready-to-run `.gba` ROM.

The GBA runtime can therefore focus on playback, rendering, input and timing instead of decoding heavyweight source formats.

## Current development priorities

The project is currently focused more on polish, reliability and efficiency than on adding a large number of new features.

### Next

- Eliminate the remaining lyric-animation flicker and fast-scroll edge cases.
- Keep browser preview timing and ROM behavior as close as possible.
- Continue real-hardware testing with different songs and lyric densities.
- Improve playback and transition stability.
- Improve the balance between audio quality and ROM size.
- Clean and organize the source tree for the first public development release.
- Add reproducible build instructions and test material.

### Later

- More efficient audio storage so a ROM can contain more music or higher-quality audio.
- Better project save/load workflows.
- More customization while keeping the GBA runtime lightweight.
- Wider testing across emulators and flash cartridges.
- Further tooling for creating and validating Pocket Audio ROMs.

Features are considered complete only when they also behave correctly in the generated ROM.

## Project status

Pocket Audio already produces functional GBA music-player ROMs and has been tested on real hardware, but the project is still under active development.

The first public source release will be published after the builder and ROM runtime have been cleaned, documented and packaged in a reproducible form.

## License

Pocket Audio is currently **source-available**, not open-source under MIT, GPL or Apache.

You may use the official Pocket Audio tool to create GBA ROMs, including ROMs containing your own music, artwork and lyrics. The rights to content placed into a generated ROM remain governed by the rights and licenses of that content.

Modification, redistribution or commercial reuse of Pocket Audio's source code is not permitted without separate permission. See [LICENSE](LICENSE) for the repository terms.

Third-party components, if any, remain subject to their own licenses.

## Disclaimer

Pocket Audio is an independent project and is not affiliated with or endorsed by Nintendo.

Game Boy Advance and GBA are trademarks of Nintendo.
