# WavRead agent skill

An agent skill for reading [WavRead](https://wavread.com) analyses (Track
Documents, Feedback Reports and the JSON behind them) and for helping someone
operate the app.

WavRead measures audio on your own computer (Mac or Windows) and writes down technical measurements of a mix, such as loudness, frequency balance and stereo, in a report. It does not
decide what any of it means. This skill is the other half: it teaches an agent the
reading order, which numbers are measured and which are estimated, the app's known
failure modes, and the cross-table findings WavRead's own rule engine cannot produce.

## Install

```
npx skills add EZmannBuilds/wavread-skill
```

Or copy [`skills/wavread/`](skills/wavread) into your agent's skills directory.

## What is in it

| File | Loaded |
|---|---|
| `SKILL.md` | Always. Every rule and every prohibition is here, so it works on its own |
| `references/reading-sections.md` | When the agent reads a specific section of a document closely |
| `references/operating-wavread.md` | When you ask how to *run* WavRead rather than what your document means |

## Use it

Run an analysis in WavRead, export the Track Document and Feedback Report, and hand
them to your agent. The skill loads on its own when it sees a `.wavread.md`,
`.report.md` or `.wavread.json`, or when someone asks for mix feedback from WavRead
data.

Your audio never leaves your machine. The exports are text.

## Version

This skill is versioned to the WavRead build it was verified against, currently
**1.5.6**. The version tracks the build; the revision counts changes to
the skill itself between builds. If your app is newer and its screens disagree with
the skill, believe the app.

**Revision 2** adds the context WavRead already records and an agent was ignoring:
the genre preset, stage and mix type that decide which findings matter at all, and
the reader's experience level, which decides whether the answer is a step-by-step or
a set of numbers. It also splits the per-section detail and the operating guide into
the two reference files above, so a conversation only pays for what it uses.

## WavRead MCP (1.5.6 and later)

WavRead 1.5.6 ships a local stdio MCP helper, `wavread-mcp`, inside the app. There
is no hosted API and no API key. It opens WavRead if it is closed, talks only to
`127.0.0.1:8765`, and audio stays on your computer. The skill prefers its tools
when installed and falls back to the Track Document flow when they are not.

| OS | Path |
|---|---|
| macOS | `/Applications/WavRead.app/Contents/Helpers/WavRead MCP.app/Contents/MacOS/wavread-mcp` |
| Windows | `%LOCALAPPDATA%\Programs\WavRead\mcp\wavread-mcp.exe` |

```
claude mcp add --scope user wavread -- "<path>"
codex mcp add wavread -- "<path>"
```

Claude Desktop: add `{"mcpServers": {"wavread": {"command": "<path>", "args": []}}}`
to the config. Any other MCP client (Cursor and others) runs it as a local stdio
server with that command and no arguments. Details: <https://wavread.com/agent#mcp>
and <https://wavread.com/MCP.md>.

## Licence

MIT. See [LICENSE](LICENSE).
