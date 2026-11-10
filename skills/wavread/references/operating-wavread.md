# Operating WavRead 1.5.6

The app is a loopback Flask service, normally port 8765. Start with
`GET /api/v1/capabilities`: it reports version, routes, methods and settings. `GET /api/v1/forms?path=/settings-page/analysis` returns the rendered
form controls and HTML. This is also the fallback for options outside JSON settings.
No cloud account is required to analyze local files.

## Settings and context

`GET /api/v1/settings` returns values, effective defaults and validation schema.
`PATCH /api/v1/settings` accepts a JSON object of only the fields to change.
Examples: `{"analysis_lyrics":false}`, `{"daw":"Logic Pro","imagery":"A railway station after midnight"}`.
Boolean values must be JSON booleans; enums must match the advertised choices.
Reading, performance, accessibility, update checks, analysis passes and creative
context are editable. External separation command, privacy consent, storage and
other specialist controls use their existing forms: inspect the relevant Settings
page rather than guessing fields or overwriting the settings file.

## Tracks and versions

`GET /api/v1/tracks` lists saved readings. `GET /api/v1/tracks/<name>` provides raw JSON data (`/json/<name>` is an HTML page).
`POST /rename/<name>` with form field `new` renames the track and related records.
Read the redirect destination and re-list the library to confirm the new name.
Inspect `/track/<name>` for history, identity, markers, references, stage, material
and export controls. Quote/encode route segments. Never rename a running analysis.
`POST /analyze` accepts `path` (local file/folder) and `mode` (`batch` or `stems`).
`GET /jobs/status` reports queued/running/done/failed/cancelled; do not call queued work complete.

## Stems

Import aligned files through `/import` multipart form (`file` repeated, `mode=stems`,
`name`, `genre`, `stage`, `mix_type`). Optional `stem_manifest` is a JSON array in
file order: `[{"name":"Piano","role":"individual","enabled":true}, ...]`.
Roles: master, individual, reverb, delay. Names are instrument-first, unique and editable.
Keep a master separate from the summed instruments. No automatic separation or
reliable audio-based instrument identification is promised.

On `/track/<name>?view=stems`, edit include/name/type controls. Posting to
`/track/<name>/stems` creates a fresh analysis with selected audio and a matching
report. Excluded parts are omitted from summed playback and stem findings; their
manifest records remain to explain the selection. A supplied master is measured
separately and never added to its instruments. If any part is excluded, listening
uses a fresh sum rather than a master that still contains the excluded part.
Each enabled part has `/track/<name>/stem/<stem>` and a `/data` JSON endpoint.

## Availability

WavRead does not capture from a DAW. Export aligned stems from the DAW and
import them. WavRead can
compare references/versions; use the available reference workspace and both readings.
From 1.5.6 (Mac Apple Silicon, macOS 14+; Windows 10/11 64-bit) the app ships
its own local stdio MCP helper, `wavread-mcp`. There is no hosted API and no API
key. The helper opens WavRead if it is closed and talks only to loopback
`127.0.0.1:8765`. The app does not mention it anywhere, so do not send the user
looking for an AI setting: add the helper to the client by its path.

| OS | Path |
|---|---|
| macOS | `/Applications/WavRead.app/Contents/Helpers/WavRead MCP.app/Contents/MacOS/wavread-mcp` |
| Windows | `%LOCALAPPDATA%\Programs\WavRead\mcp\wavread-mcp.exe` |

- Claude Code: `claude mcp add --scope user wavread -- "<path>"`
- Codex: `codex mcp add wavread -- "<path>"`
- Claude Desktop: add to `mcpServers` in the config JSON, with that command and
  no args: `{"mcpServers": {"wavread": {"command": "<path>", "args": []}}}`
- Any other MCP client (Cursor and others): run it as a local stdio server with
  that command and no arguments.

Twelve tools: `start_wavread`, `capabilities`, `settings`, `list_tracks`,
`read_track`, `analyze_files`, `jobs`, `select_stems`, `rename_track`,
`inspect_page`, `app_request` and `save_app_file`. `app_request` reaches every
implemented route and `inspect_page` shows current forms. Prefer these tools when
installed; otherwise use the Track Document flow. The Markdown skill is guidance,
not the executable server. Earlier builds have no helper, and a source checkout
runs `integrations/wavread_mcp/server.py` instead.
Audio stays on the computer; returned measurements and text enter the assistant
conversation. Guides: <https://wavread.com/agent#mcp> and <https://wavread.com/MCP.md>.
