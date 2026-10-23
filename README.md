# Ambition

A Claude skill that pushes work past "did what was asked" toward the outcome the work is for.

Without it, an agent usually finishes the literal task and stops, because nothing in the request says what the task is for. This skill makes Claude set the outcome first, work like the best practitioner in the field, and prove the result with something other than its own opinion.

## Credit

This skill is based on the article [How to be more ambitious: a tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) by Felix Rieseberg (13 Oct 2026). The ideas and the four kinds of ambition come from his article. Please read the original.

This is an unofficial adaptation. It is not affiliated with or endorsed by the author.

## What it does

The article names four kinds of ambition: Speed, Altitude, Depth and Range. Speed is already Claude's default, so the skill covers the other three plus an outside judge.

| Part | What Claude does |
|------|------------------|
| Altitude | Writes down the outcome the task serves and what done looks like at that level |
| Depth | Answers four questions about how a top professional would approach it, then works from a deeper version of the task |
| Outside judge | Checks the work with a test, benchmark or a separate review instead of grading itself |
| Range | Brings in fields you would not normally use (only when you ask for it) |

It also checks up front whether Claude can actually see the result of its work. If it cannot, it says so instead of guessing.

## Install

### Claude (web or desktop app)

1. Download `ambition.zip` from the latest release, or zip the `SKILL.md` file yourself.
2. Open **Settings**, then **Capabilities**.
3. Upload the zip file under Skills.

### Claude Code

1. Create the folder `~/.claude/skills/ambition/`.
2. Copy `SKILL.md` into it.
3. Start a new Claude Code session.

## How to use it

Say one of these in your request:

- "be ambitious"
- "go deeper"
- "ambition"
- "depth prompt" (Claude outputs only a rewritten, deeper prompt you can paste into a fresh session)
- "range review" (Claude brings in extra fields, and asks you to confirm the cost first)

Claude also loads it when you ask for a build or report to be "actually good".

## Notes

- The skill is general. It uses "the user" and has no company or tool specific content.
- The fresh-eyes review step uses Claude Code. In the regular chat apps, Claude will give you a review packet to run elsewhere.
- Skip it for quick one-off edits. It is meant for work that matters.

## License

MIT. See `LICENSE`.
