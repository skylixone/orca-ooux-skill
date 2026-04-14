# OOUX / ORCA Facilitation Skill

An interactive facilitation skill for AI agents that runs a structured [OOUX](https://www.ooux.com/)/[ORCA](https://www.ooux.com/resources/orca) workshop with the user, producing an object map and CTA inventory for a product being designed.

The facilitation logic is model-agnostic — any agent that can follow structured instructions can run this workshop. The file format (`SKILL.md` with YAML frontmatter) is Hermes Agent's skill convention, but the process, rules, and patterns inside apply to any capable AI assistant.

---

## What it does

When loaded, the agent runs a full OOUX workshop:

- Extracts objects from a product brief
- Maps relationships and nesting
- Brainstorms CTAs (calls to action — the interactive triggers users can activate on an object, e.g. a "Buy Now" button on a product page) per object (with loops back to O when new nouns surface)
- Defines and ranks attributes (core content vs metadata)
- Fills a 6-field CTA Inventory table
- Validates the object model before any [IxD](https://www.nngroup.com/articles/interaction-design-definition/) begins
- Facilitates IxD flow-by-flow after the model is confirmed

Output: a structured `object-map.md` and `cta-inventory` in markdown, ready for the IxD phase.

---

## File inventory

| File | Description |
|---|---|
| `SKILL.md` | The skill itself — loaded by Hermes Agent at runtime |
| `hermes_conversation_20260408_153340.json` | Session 1: initial ORCA run on the_lorf |
| `hermes_conversation_20260409_145232.json` | Session 2: slot inventory + challenge loop |
| `hermes_conversation_20260409_190354.json` | Session 3: IxD phase facilitation |

The JSON files are session transcripts. They are the source of the "Facilitation Patterns" and "IxD Phase Facilitation" sections in SKILL.md — all learned patterns were extracted from real workshop sessions and written back into the skill.

---

## How the skill is structured

```
SKILL.md
  frontmatter         — name, description, tags, related skills
  Core Premise        — why objects before screens
  ORCA Process        — O / R / C / A steps with rules and agent questions
  CTA Inventory Schema — 6-field table definition
  Validation Gate     — pass/fail criteria before IxD
  Session Script      — opening, phase sequence, iteration loops
  Output Format       — markdown template for final object map
  Image Analysis      — pattern for visual brief analysis with vision_analyze
  Facilitation Patterns — learned patterns from real sessions (main body of growth)
  SlotDefinition work — challenge loop, inventory workflow, learned slot pitfalls
  IxD Phase           — flow-by-flow facilitation, shell decisions, state model discipline
  Pitfalls            — common failure modes with explicit resolutions
  Sequencing          — full 1–10 process sequence
```

---

## Trigger conditions

Load this skill when:

- Designing a product and need the [content model](https://alistapart.com/article/content-modelling-a-master-skill/) before wireframing (the way god intended)
- User says "do OOUX", "object mapping", or "ORCA"
- Has a brief, goals doc, or user stories and wants to extract structure...
- is about to jump to wireframes without a validated object model
- mentions CTAs, content types, or [IA](https://www.nngroup.com/articles/ia-vs-navigation/) as a starting point

---

## Design philosophy

Objects are the nouns users think about, not the screens you design. Every screen, nav item, and interaction is downstream of the object model. Get the objects wrong and every downstream design decision compounds the error.

OOUX was created by Sofia Quintero. References:
- https://www.ooux.com/
- https://www.ooux.com/resources/orca
- https://alistapart.com/article/ooux-a-foundation-for-interaction-design/

---

## Usage

Just point your agent to this repo — they will know what to do.

**Hermes Agent**
Skill lives at `~/.hermes/skills/creative/ooux/SKILL.md` — loaded automatically when trigger conditions match.

```
git clone https://github.com/skylixone/orca-ooux-skill ~/.hermes/skills/creative/ooux
```

---

**Claude Code**
Claude Code picks up skills placed in `.claude/skills/` inside a project directory. Clone the repo there and Claude will invoke the facilitation process automatically when the task matches.

```
git clone https://github.com/skylixone/orca-ooux-skill .claude/skills/ooux
```

Then in your session: "run an OOUX workshop on this brief: [brief]" (paste text or drop in your brief file)

> Note: `.claude/skills/` support — placeholder, verify against Claude Code docs at time of use.

---

**Any other agent**
Paste or attach `SKILL.md` as a system prompt or context document, then tell the agent: "run an OOUX workshop on this brief: [brief]". The agent has everything it needs to facilitate the full session.



---

## Changelog / growth log

The skill has been grown through several live workshop sessions on a real product (L.O.R.F, a  social media content creation tool for corporate use — for non-creatives to make social ). Key additions from those sessions:

- Adversarial validation pattern for object model completeness before IxD
- Figma-style WYSIWYG canvas with limited editability (branding is locked in)
- "Only the branding is locked" global rule
- Single-slide collapse pattern (carousel vs single-image unification)
- Template picker-as-home-screen pattern
- Gerstner-style grid sizing validation with real viewport math (see also: [programmatic design](https://www.eyeondesign.aiga.org/karl-gerstner-programmatic-design/))
- IxD phase facilitation with persistent ixd.md file pattern
- Canvas-as-workspace vs canvas-as-document distinctions
- Competitive research delegation pattern during IxD
- Person reuse vs inline entry decision pattern

All patterns are written directly into SKILL.md under the "Facilitation Patterns" section so the agent has them available in every future session without needing to re-discover them.

---

```
        oooo                    oooo   o8o                                              
        `888                    `888   `"'                                              
.oooo.o  888  oooo  oooo    ooo  888  oooo  oooo    ooo  .ooooo.  ooo. .oo.    .ooooo.  
d88(  "8  888 .8P'    `88.  .8'   888  `888   `88b..8P'  d88' `88b `888P"Y88b  d88' `88b 
`"Y88b.   888888.      `88..8'    888   888     Y888'    888   888  888   888  888ooo888 
o.  )88b  888 `88b.     `888'     888   888   .o8"'88b   888   888  888   888  888    .o 
8"888P' o888o o888o     .8'     o888o o888o o88'   888o `Y8bod8P' o888o o888o `Y8bod8P' 
                     .o..P'                                                              
                     `Y8P'
```
