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

Or download [`skills/wavread/SKILL.md`](skills/wavread/SKILL.md) and drop it into
your agent's skills directory.

## Use it

Run an analysis in WavRead, export the Track Document and Feedback Report, and hand
them to your agent. The skill loads on its own when it sees a `.wavread.md`,
`.report.md` or `.wavread.json`, or when someone asks for mix feedback from WavRead
data.

Your audio never leaves your machine. The exports are text.

## Version

This skill is versioned to the WavRead build it was verified against — currently
**1.4.47**. If your app is newer and its screens disagree with the skill, believe
the app.

## Licence

MIT. See [LICENSE](LICENSE).
