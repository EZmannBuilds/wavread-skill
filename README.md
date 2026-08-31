# WavRead agent skill

An agent skill for reading [WavRead](https://wavread.com) analyses — Track
Documents, Feedback Reports, and the JSON behind them — and for helping someone
operate the app.

WavRead measures audio on your own Mac and writes down what it found. It does not
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

This skill is versioned to the WavRead build it was verified against — currently
**1.4.47, revision 2**. The version tracks the build; the revision counts changes to
the skill itself between builds. If your app is newer and its screens disagree with
the skill, believe the app.

**Revision 2** adds the context WavRead already records and an agent was ignoring:
the genre preset, stage and mix type that decide which findings matter at all, and
the reader's experience level, which decides whether the answer is a step-by-step or
a set of numbers. It also splits the per-section detail and the operating guide into
the two reference files above, so a conversation only pays for what it uses.

## Licence

MIT. See [LICENSE](LICENSE).
