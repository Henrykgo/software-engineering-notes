A Claude Code skill is a reusable Markdown file of instructions that Claude loads when needed to perform a task consistently.
### What is a skill?
A Claude Code skill is a Markdown file stored at .`claude/skills/<name>/SKILL.md` that defines reusable instructions for a task.
## How I used them: six skills for the restaurant pipeline

| Skill                | Role                                                                                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `onboard-restaurant` | Discovery and extraction: find the site, pick a model by quota, fix blockers like dead menu links                                       |
| `verify-restaurant`  | Blind-draft the menu from the live site, diff it against the extraction, prepare the golden draft. The only place correctness is judged |
| `verify-queue`       | Driver: one fresh subagent per restaurant running verify, collects one report                                                           |
| `fill-gaps`          | Metadata only (hours, socials, cuisines), written through the provenance-aware setter                                                   |
| `make-publishable`   | Router: reads why a row is blocked, sends it to fill-gaps or human review                                                               |
| `add-restaurants`    | Orchestrator: runs the stages in order, then hands back                                                                                 |

### Example: Chaining Skills
The `add-restaurants` skill coordinates the workflow. No arguments it will push what already is in the pipeline to as ready, with a number N it first onboards N  new restaurants.

1. Runs `/onboard-restaurant` (only when given N or names) to discover and extract restaurant data. This is the only stage that uses Gemini quota.
2. Runs `verfify-queue`, which launches one fresh subagent per restaurant to blind-draft the menu from the live site, diff it against the extraction, and import the golden.
3. Runs `/make-publishable`, which routes each blocked restaurant to '\fill-gaps' or human review, then marks ready what qualifies.
4. Between stages, it checks the actual data files to see which restaurants still need work, instead of trusting what the previous stage claimed it had done.
5. Stops before publish and produces one report: which restaurants became publishable, what needs human eyes.



