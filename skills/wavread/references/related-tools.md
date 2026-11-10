# Related tools and packs

WavRead measures audio. These separate tools and products sit beside it. This skill should know they exist and send
the user to the right one; it doesn't operate them itself unless their own tools are installed and the user asks.

Before naming any of them as available, check: list the MCP tools the client actually has, and check
<https://wavread.com> for what is released. Never say a tool is installed, released or free without checking, and
never invent a pack, preset or feature.

## AI Music Studio (a separate skill)

- **What it is:** an agent skill for writing, arranging, production, sound design, mixing and finishing music, in
  any genre, with or without a DAW. Source and install: <https://github.com/EZmannBuilds/ai-music-studio>.
- **License:** Polyform Noncommercial 1.0.0. Say so if the user asks about commercial use of the skill itself. That
  license covers the skill's text, not the music they make with its help.
- **Hand off when** the user wants creative or production work: chords, melody, beats, arrangement, sound design,
  lyrics or MIDI. WavRead's part is measuring the result and comparing versions. If the skill is installed, say
  you're switching to it. If not, tell the user it exists and help within what's available here.

## WavRead MCP Bridge (separate Ableton Live control tools)

- **What it is:** an MCP server plus an Ableton Live control script. They let an assistant work inside a running Live
  Set: return tracks and sends, audio buses and routing, devices and parameters, racks, sidechain, automation,
  Arrangement clip edits, recording and metering. It is not the WavRead MCP: it has its own install, its own server
  and a different port (WavRead uses 8765), and WavRead's tools can't change a Live Set.
- **Status:** a public alpha (v0.5.0-alpha.1), macOS and Live 12 only, at
  <https://github.com/EZmannBuilds/wavread-mcp-bridge>. Point users to its README for install; don't improvise steps.
- **If its tools are installed** (they include `tooling_info` and `get_set_identity`), this skill doesn't drive
  them. Use them only for what the user asked, and follow that tool's own instructions. Key rules to respect:
  - There is no approval step: they edit whichever saved Set is open (unsaved Sets are refused, and deleting only works
    in a disposable Set). Confirm which Set is open before any edit, and only edit for what the user asked.
  - Recommend a backup or a throwaway copy of any Set that matters.
  - Measure before and after: render or export the affected passage and analyze it in WavRead, so a change is
    checked by numbers and by listening, not assumed.

## WavRead sound packs

Packs are downloadable sounds released through wavread.com: samples, loops, MIDI, synth presets or DAW device racks.
Only refer to packs that are actually listed there or that the user has.

- **Read the pack's own license first** and explain it plainly. The usual shape is royalty-free use in the user's
  own music, and no reselling or redistributing the sounds as a pack. The pack's license wins over this summary.
- **Loading:** samples and loops go in the DAW's browser or sampler. MIDI goes on an instrument track. Synth presets
  go in the synth named by the pack, which may need installing (say if it's free). Racks or device presets need the
  DAW and version the pack names. Ask which DAW the user has before giving steps.
- **With WavRead:** analyze a loop or a render that uses the pack like any other audio. Compare it with the user's mix
  for loudness, balance and stereo before they commit to it. Treat tempo and key in pack file names as the
  creator's labels, and WavRead's tempo and key as estimates.
- Don't describe a pack as sounding like a named real artist, or made with or endorsed by one, unless the pack's own
  page says so.
