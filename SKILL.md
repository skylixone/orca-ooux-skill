---
name: ooux
description: Interactive OOUX/ORCA facilitation tool. Agent runs a structured workshop with the user to produce an object map and CTA inventory for a product being designed. Covers the full ORCA loop (Objects, Relationships, CTAs, Attributes), CTA Inventory schema, validation gate, and sequencing rules.
tags:
  - ux
  - product-design
  - ooux
  - orca
  - object-map
  - cta-inventory
  - workshop
  - facilitation
related_skills:
  - plan
  - writing-plans
  - test-driven-development
---

# OOUX / ORCA Facilitation

## Trigger Conditions

Load this skill when the user:
- Says they want to do OOUX, object mapping, or ORCA
- Is designing a product and needs to figure out the objects/content model before wireframing
- Has a product brief, goals doc, or user stories and wants to extract structure from them
- Is about to jump to layout/wireframes without a validated object model
- Mentions CTAs, content types, or information architecture as a starting point

---

## Core Premise

Objects are the nouns users think about, not the screens you design. Every screen, nav item, and interaction is downstream of the object model. Get the objects wrong and every downstream design decision compounds the error. OOUX extracts objects from the product brief before any interaction design begins.

---

## ORCA Process — Executable Steps

### O — Extract Objects

Rules (apply in order, strictly):

1. Pull recurring nouns from the brief, goals, user stories, and stakeholder language.
2. REJECT collection-words: library, catalog, calendar, map, list, feed, directory, inbox, gallery, dashboard. These are list-views of a real object. Ask: "what is one item in this collection?" That item is the object.
3. REJECT abstract nouns that are outcomes or hopes, not things: exposure, success, engagement, growth, trust, value, impact. If you can't put it in a database row, it's not an object.
4. INFER from verbs: "users can schedule a session" → Session is an object. "artists submit a portfolio" → Portfolio, Submission are candidate objects.
5. FLAG multi-state objects: things that behave differently depending on state (e.g. Order: pending / fulfilled / cancelled). These need state-aware CTAs later.
6. Produce a candidate object list. Do not finalize — present to user for pruning/additions.

Agent questions to ask during O:
- "What is one [collection-word]? What would you call a single item in that list?"
- "Is [abstract noun] something a user can actually open, click, or own? If not, cut it."
- "What verb just appeared in the brief? What thing does that verb act on?"

---

### R — Relationships and Nesting

Rules:

1. For each object pair, ask: is one a child of the other (nesting), or are they associated peers (relationship)?
2. Nesting: a Track belongs to an Album. A Lesson belongs to a Course. The child cannot meaningfully exist without the parent context.
3. Association: a User is linked to an Order, but neither owns the other.
4. Draw the map as a flat list with indentation showing nesting. Annotate peer relationships with arrows or line notes.
5. Watch for hidden objects: if a relationship requires properties of its own (e.g. Enrollment has a start date, a status, a payment record), the relationship IS an object.

Agent questions:
- "Can [object] exist independently, or does it always belong to [other object]?"
- "When a user navigates to [object], do they come from [other object] always, or from multiple places?"
- "Does the link between [A] and [B] have its own data? If yes, name it."

---

### C — CTA Brainstorm

Rules:

1. For each object, ask: what can a user DO TO this thing? List all actions without filtering.
2. Typical CTA verbs: create, edit, delete, archive, share, follow, rate, comment on, duplicate, export, assign, schedule, publish, submit, approve, reject, flag, bookmark, download, preview.
3. Do NOT assign CTAs to screens yet. CTAs float. Placement is an IxD decision made later.
4. CRITICAL: if a CTA reveals a new noun ("assign to a Team") and Team is not in the object list — STOP. Add Team to O. Re-run R for Team. Then continue C.
5. Flag CTAs that only apply in certain states (multi-state objects).
6. Mark each CTA: primary (core to the system's purpose) or secondary (utility).

Agent questions:
- "What would the most important user type want to do with [object] right now?"
- "What does an admin/creator need to do that a viewer cannot?"
- "What happens to [object] over time — does it get approved, published, archived?"

---

### A — Attributes

Rules:

1. For each object, list every piece of data it carries.
2. Classify each attribute: CORE CONTENT (the thing itself — title, body, image, price) vs METADATA (about the thing — created date, author, status, view count, tags).
3. FORCED RANKING: rank attributes 1-N per object by user need. The #1 attribute is what the user needs to see first to orient themselves. This ranking drives content priority inside an object view — it is NOT layout order and NOT nav order. Explicitly tell the team this.
4. Watch for attributes that are actually nested objects (e.g. "ingredients list" on a Recipe → each Ingredient is its own object).

Agent questions:
- "If a user lands on [object] for the first time, what one piece of information do they need to orient?"
- "Which attributes are generated by the system vs entered by the user?"
- "Is [attribute] really a list of things? If yes, name the thing."

---

## CTA Inventory Schema

For every CTA that survives the brainstorm, record 6 fields:

| Field | Question to answer |
|---|---|
| Why | What user goal or system goal does this CTA serve? One sentence. |
| Who | Which user type(s) can trigger this? (Creator, Viewer, Admin, Guest, etc.) |
| Where | Which object view(s) or system context(s) surface this CTA? (Not a screen — an object.) |
| Complexity | Simple (one-step, instant), Moderate (form, confirm), Complex (multi-step, async, has states). |
| Priority | P1 (launch-critical), P2 (important, not blocking), P3 (nice-to-have). |
| Unknowns | Open questions, dependencies, edge cases not yet resolved. |

Agent instruction: After C step, systematically fill this table for every CTA. Gaps in Why or Who are design debt — flag them explicitly.

---

## Validation Gate

BEFORE any interaction design, wireframes, or layout work, validate the object model.

Steps:
1. Build an object-nav prototype: a bare-bones clickable prototype where each screen is just the object name and a list of its attributes. No layout, no visual design. Navigation links only follow object relationships.
2. Give it to 3-5 users (or walk through it yourself as the target user).
3. Ask: "Can you find [object]? What would you do next? Does this match how you think about [domain]?"
4. PASS criteria: users navigate without prompting, use the same nouns you used, arrive at the objects they expect.
5. FAIL criteria: users use different nouns, get confused about where things live, look for objects that don't exist.
6. On FAIL: return to O. Do not patch with navigation tricks. Fix the objects.

Agent instruction: Do not proceed to IxD phase until the user confirms validation has been done or explicitly accepts the risk of skipping it.

---

## Session Script

### Opening

Ask: "Do you have a product brief, goals doc, user stories, or any written description of what this product does? Paste it or summarize it here."

If yes: extract candidate objects from the text before asking anything else. Present the list.
If no: ask for a one-paragraph description of the product and its primary user. Then extract.

---

### Phase sequence to follow

1. Present candidate object list from O. Ask: "Are any of these the same thing? Are any missing? Are any of these collection-words or outcomes rather than real objects?" Iterate until the user confirms the list.

2. Run R. Present the nesting/relationship map. Ask: "Does this match how you think about the domain? Any surprises?" Iterate.

3. Run C for each object. Present CTA lists per object. Watch for new noun triggers — announce them and loop back to O+R before continuing. Ask: "Any CTAs missing? Any that should never exist?"

4. Run A for each object. Present attribute lists with core/metadata classification. Ask: "Is the forced ranking right? What does a user need first?"

5. Fill CTA Inventory table. Flag any row with empty Why or Who. Ask the user to resolve them or explicitly park them as unknowns.

6. Present the validation gate. Ask: "Have you tested this object model with real users or done a mental model walkthrough?" If not, push them to do it before wireframing.

7. Produce the final object map output (see Output Format below).

---

### Handling Iteration Loops

- CTA reveals new object → announce it, add it, re-run R for that object, then return to C where you left off.
- User wants to talk about screens during O/R/C → redirect: "We'll get to screens. Right now we're naming the things, not drawing the places."
- Stakeholder pushes back on forced ranking → say: "This ranking is about content priority inside the object, not about what goes in the nav or on the homepage. Those decisions come later."
- User wants to design the homepage → say: "Homepage is designed last, after all objects, nav patterns, and key flows are validated. Park it."

---

## Output Format

Produce this markdown document at the end of the session:

```markdown
# Object Map — [Product Name]
Date: [date]

---

## Objects

### [Object Name]
State(s): [if multi-state, list them]

**Core Content**
- [attribute 1] — ranked #1
- [attribute 2] — ranked #2
- ...

**Metadata**
- [attribute]
- ...

**CTAs**
- [CTA verb + object] — Primary/Secondary — [state condition if any]
- ...

**Relationships**
- Belongs to: [parent object if nested]
- Associated with: [peer objects]
- Contains: [child objects]

---
```
[Repeat block for each object]

---

## CTA Inventory

| CTA | Why | Who | Where | Complexity | Priority | Unknowns |
|---|---|---|---|---|---|---|
| [verb + object] | ... | ... | ... | Simple/Moderate/Complex | P1/P2/P3 | ... |

---

## Open Questions

- [Any unresolved items from the session]

## Validation Status

[ ] Object-nav prototype built
[ ] Mental model tested with users
[ ] PASS / FAIL — notes: ...
```

---

## Image Analysis During ORCA Sessions

When the brief includes reference images (example posts, brand assets, design references), analyze them directly using vision_analyze with local file paths. Do NOT delegate image analysis to subagents — subagents do not inherit the vision toolset and will fail on binary files.

Pattern for bulk image analysis:
1. Use search_files(target='files') to list the folder.
2. Run vision_analyze in parallel batches of 3 per turn (tool call limit).
3. Ask a focused question per image: layout type, content elements present, post type classification.
4. Compile results after all images are processed.

This is load-bearing for ORCA sessions that need to reconcile the brief's content taxonomy against real production examples — discrepancies between what the brief says and what the images actually show often surface missing post types or slot definitions.

---

## Facilitation Patterns (learned in practice)

### Check existing IxD and decisions docs before raising open questions
Before surfacing an open question to the user, check whether it was already resolved in a prior session. For the_lorf: read ixd.md and decisions.md in full before asking anything. Re-raising already-answered questions wastes the user's time and breaks trust. If a doc exists, read it first — always.

### Template gallery grouping — when to use flat grid vs categories
For internal specialized tools with a small fixed set of content types (~12), a flat visual grid with no categories is correct at MVP. Rationale: users are repeat experts, not strangers; strong preview images carry all the communication load; no taxonomy debt; additive category filter can be bolted on later without rebuilding. Validate fit with screen-size math: (viewport_width - (col-1 × gap) - (2 × gutter)) / cols = item_width. Check item_width against minimum readable size (~200px). Check row count at smallest viewport. If all items fit with minimal scroll, flat grid wins. Categories only when item count exceeds cognitive threshold (~16+) or when user base is diverse/non-expert.

### SlotDefinition / SlotInstance split
When an object has both a schema role (config-time, authored once) and an instance role (runtime, authored repeatedly), split them into two objects. The tell: "this field gets duplicated into every row" or "some columns are always null depending on which role this row plays." Classic example: a content slot that defines type/label/validation (SlotDefinition on a template) vs the filled value for a specific piece of content (SlotInstance on a record). The UI can still show a simple labeled input field — the split is a data model concern, not a UX concern. Make this explicit when stakeholders push back.

### Single-slide collapse
When a system has both single-image and multi-image (carousel) output types, model everything as "Post has N Slides" where single-image Posts have exactly one Slide. Removes polymorphic parent problems (SlotInstance belonging to either Post or Slide), simplifies export logic (N=1 → PNG, N>1 → PDF), and makes the data model uniform. The carousel vs single distinction becomes a derived property of slide count, not a structural branch.

### Reference image analysis before A step
If the client has example images, screenshots, or reference designs, analyze them visually before running A (Attributes). Images surface: actual slot types in use, which post types need Person objects vs inline fields, layout hints for SlotDefinition, and post type taxonomy gaps (e.g. a newsletter cover that doesn't fit any existing type). Run this between C and A. Use vision_analyze on each image; batch into parallel calls where possible.

### Open questions accumulation pattern
After ORCA completes, collect all open questions into a dedicated decisions file (e.g. `decisions.md`). Walk through them one by one with the user — one question per message, state your lean, get a one-line answer. Accumulate all answers. When exhausted, prompt user to trigger an object map update pass. This keeps the object map clean (v0.1 written first, updated after decisions) and gives the user a clear audit trail of what was decided and why.

### SlotDefinition challenge loop (adversarial validation)
After producing a preliminary SlotDefinition table for each PostType, run a one-by-one challenge session with the user before writing the final inventory. Pattern:
1. Present one PostType at a time: slots, slot_types, required flags, reasoning, and where you think it's vulnerable.
2. User tries to break it — edge cases, missing slots, wrong types, wrong locked/unlocked calls.
3. Resolve each attack as a confirmed correction or a confirmed hold. Record the outcome.
4. Only move to the next PostType after verdict is called.

Key things that break slot models in practice:
- Text assumed brand-locked that isn't. Global rule: only the logo is furniture. Every readable string is a slot with a default. Confirm per type, never assume.
- Single headline slots that are actually two typographic zones (bold + thin). Always ask: is this one field or a bold/regular split? If the design has two weights, it's two slots.
- Illustration/image assumed to be user upload when it's actually a folder-pick (select slot, not image slot). Ask explicitly: user upload or pre-supplied set?
- Per-item style switches (numbered vs icon) that are actually PostType-level, not per-item. One switch slot governs the whole component.
- CTA labels assumed brand-locked when they're editable with a default (e.g. "Download", "Watch on demand", "Welcome to the team!").
- Preliminary notes file: write image classification, global rules, and per-type slot tables to a -preliminary.md before the challenge session. Update it in-place as decisions land. Don't wait until end of session to write.

### SlotDefinition inventory workflow (post-ORCA phase)
After ORCA is complete and the object model is confirmed, SlotDefinition inventory is a distinct phase before IxD. Pattern:

1. Load all context files (object-map.md, decisions.md, brief.md) before touching images.
2. List all reference images with search_files(target='files'). Build a type-to-image map: brief says how many per type (e.g. "newHire ×3") — use that as the expected count.
3. Classify images using vision_analyze in batches of 3. Ask a focused classification question per batch. Resolve ambiguous types with a targeted follow-up (e.g. "is there a date/time or a Watch on demand CTA?" to distinguish eventLive from eventReplay).
4. Write a preliminary slot-inventory.md with draft SlotDefinition tables before challenging anything. Capture structural observations (layout variants, slide-role dependencies, merged vs split fields) as notes.
5. Challenge each PostType one at a time with the user (see challenge loop below). Start with the simplest types as warmup.
6. Write final slot-inventory.md only after all types are confirmed.

### SlotDefinition challenge loop (adversarial validation)
After producing a preliminary slot table for each PostType, run a one-by-one challenge session. Pattern:

1. Present one PostType at a time. State the claim explicitly: "These N slots are sufficient for any [PostType] post this product would ever need." List slots, reasoning, and where YOU think it's vulnerable.
2. User tries to break it — edge cases, missing slots, wrong types, wrong locked/unlocked calls.
3. Resolve each attack as a confirmed correction or confirmed hold. State verdict: "holds", "holds with corrections", or "needs rework."
4. Only move to the next type after verdict is called.

When a global rule surfaces mid-session, stop, name it explicitly, write it to disk immediately. Do not let global rules accumulate in your head.

Key things that break slot models in practice:
- Text assumed brand-locked that isn't. Default rule: only the logo is furniture. Every readable string is a slot with a default. Confirm exceptions explicitly per type, never assume.
- Single headline slots that are actually two typographic zones (bold + thin). If the design has two weights, it's two slots: headlineBold (required) + headlineThin (optional). Font scales to fit. Hard char limits are soft editorial guards, not hard blocks.
- Illustration/image assumed to be user upload when it's actually a folder-pick. Ask: user upload or pre-supplied library? Brand-consistency systems almost always use library picks (slot_type: select, not image).
- Per-item style switches (numbered vs icon) that are PostType-level, not per-item. One switch slot governs the whole component.
- CTA labels assumed brand-locked when they're editable with a default ("Download", "Watch on demand", etc.).
- Free text beats structured fields for MVP: datetime, citations, rankings, episode tags — all free text until localization or automation is on the roadmap.
- Carousel types need slide_role scoping on SlotDefinitions (cover / content / closing / any) — flat slot lists can't express role-dependent schemas without it.

### Picker-as-home-screen pattern
When a product's primary creation flow starts with "pick a type," evaluate whether the picker should be a persistent home screen rather than a modal trigger. The tell: if there is no meaningful "home" content to show before the user picks a type, the picker IS the home screen. Making it a modal adds a route, a trigger CTA, and a back-navigation trap for no UX benefit. Classic case: a content creation tool where the Post list is empty until a type is selected — the PostType picker grid becomes the default New Post view, always visible, mode-switched via a segmented control rather than navigation. This removes one interaction step and eliminates the browser-history trap.

### Grid sizing validation with real screen data
When a flat grid of N items is proposed and "fits on one screen" is a concern, validate with actual viewport math before accepting or rejecting it as a constraint. Pattern:
1. Get smallest widespread screen dimensions from StatCounter or similar (resolution CSV).
2. Subtract browser chrome (~100px) and UI gutters from viewport height.
3. Apply grid formula: (viewport_width - (cols-1 × gap) - (2 × gutter)) / cols = item_width.
4. Vertical: (usable_height) / item_height = rows above fold.
5. If rows × cols ≥ N: everything fits. If not: quantify the scroll (fraction of a row = acceptable for specialized tools).
This prevents overcautious constraints ("must fit on one screen") from driving unnecessary taxonomy decisions. A small scroll in a specialized internal tool is zero friction for repeat users.

### Check existing IxD docs before proposing solutions to open questions
During IxD facilitation, always read the full ixd.md (or equivalent) before presenting options on any open question. Previous sessions may have already resolved it. Re-proposing a resolved question wastes time and erodes credibility. Pattern: search for "Open:" and "Locked:" tags in the doc to quickly identify what is genuinely open vs already decided.

### "Show where you can show" principle
Any UI choice that can be represented graphically should use images instead of text labels. PostType selection, template pickers, layout options — always use example or blank images. Never describe what can be demonstrated visually. Note this explicitly in the object map and flag it during A when preview_image or thumbnail attributes appear on config objects.

### Person reuse vs inline entry
During C, when a post type requires person data (name, title, photo), ask explicitly: will the same person ever appear in more than one Post? If yes → Person is a reusable object with a roster picker. If no (e.g. a one-time new hire announcement) → inline entry only, no Person object created, just fields on the SlotInstance. A single product can have both patterns for different post types. Model them separately.

### SlotDefinition inventory workflow (post-ORCA phase)
After ORCA is complete and the object model is confirmed, SlotDefinition inventory is a distinct phase before IxD. Pattern:

1. Load all context files (object-map.md, decisions.md, brief.md) before touching images.
2. List all reference images with search_files(target='files'). Build a type-to-image map: brief says how many per type (e.g. "newHire ×3") — use that as the expected count.
3. Classify images using vision_analyze in batches of 3. Ask a focused classification question per batch. Resolve ambiguous types with a targeted follow-up (e.g. "is there a date/time or a Watch on demand CTA?" to distinguish eventLive from eventReplay).
4. Write a preliminary slot-inventory.md with draft SlotDefinition tables before challenging anything. Capture structural observations (layout variants, slide-role dependencies, merged vs split fields) as notes.
5. Challenge each PostType one at a time with the user. Present the slot schema + reasoning; user attempts to find edge cases. Iterate until confirmed.
6. Watch for: fields with highly variable length that break layout (title fields especially), free-text vs select type decisions, optional slots that change the layout (e.g. host2 on podcast), and slide-role-dependent schemas on carousel types (cover / content / closing have different slots).
7. Write final slot-inventory.md only after all 12 (or N) types are confirmed.

---

## SlotDefinition Challenge Session

Use this pattern after ORCA is complete and a preliminary slot inventory exists.
Goal: stress-test every SlotDefinition table before writing the approved inventory.

### Setup
1. Do image classification first (vision_analyze all reference images, batch 3 per turn).
   Map each image to a PostType before touching any slot tables.
2. Write a preliminary file (slot-inventory-preliminary.md) with:
   - Image classification table
   - Global design rules section (grows during the session)
   - Draft slot tables per PostType with notes and open questions
3. Start with the simplest/most constrained PostTypes as warmup (fewest slots, least ambiguity).

### Per-type challenge loop
Present one PostType at a time. State the claim explicitly:
"These N slots are sufficient for any [PostType] post Legatics would ever create."
List the slots. Give your reasoning. Name where YOU think it's vulnerable.
Then ask the user to attack it.

User attacks to watch for:
- Missing slot ("what if they want X?")
- Slot that shouldn't exist ("why would they fill Y?")
- Wrong slot_type ("that shouldn't be free text")
- Wrong required/optional
- Layout reality that breaks the model
- Global rule that should apply everywhere (extract immediately)

When a global rule surfaces, stop, name it explicitly, write it to disk before continuing.
Do not let global rules accumulate in your head — they will be forgotten.

### Verdict pattern
After each type: state "holds", "holds with corrections", or "needs rework".
List the corrections inline. Move on immediately.

### Lessons learned from Legatics session (2026-04-12)

**"Only the logo is locked" rule.**
Default assumption: every visible text is a user-editable slot with a sensible default.
No text is brand-locked except the wordmark/logomark. Confirm exceptions explicitly.
This rule surfaced mid-session and retroactively corrected several types.
Write it as Global Rule #1 at the top of any slot inventory.

**Illustration/icon picker is not an upload.**
When a design uses illustrations or icons, always ask: user upload or system library?
For brand-consistency systems (like a Deterministic Design Governor), it's always a folder
of pre-supplied images. slot_type = select, options = library keys. Not image upload.

**Headline is two slots, not one.**
Any headline that has a bold part and a regular/thin part = headlineBold + headlineThin.
headlineBold required, headlineThin optional. Renderer controls typographic treatment.
No structural colon convention — they are independent fields.
Font scales to fit. Hard char limits are editorial soft-guards, not hard blocks.

**PostType-level switches vs per-item slots.**
When items in a list can be either numbered or icon-labeled, that's a PostType-level
(or slide-level) switch: itemStyle = select: numbered | icons.
Not a per-item decision. Keeps the model uniform and the UI simple.

**Carousel slide roles need scoping.**
productFeature and whitepaperCarousel have structurally different slots per slide role
(cover / content / closing). SlotDefinitions need a slide_role scoping mechanism.
Flag this as an open question — it's a data model decision, not a UX decision.

**Free text beats structured fields for MVP datetime/citations.**
eventLive dateTime, award pillLabel, podcast episodeTag — all free text for MVP.
No date pickers, no parsers, no timezone handling. User types whatever string they want.
Renderer places it. Revisit only when localization or automation is on the roadmap.

**image vs select for visual slots.**
User-uploaded content (headshots, UI screenshots, product photos) = slot_type: image.
System-library picks (illustrations, icons, decorative graphics) = slot_type: select.
Never conflate the two. Ask explicitly for each visual slot which pattern applies.

---

## IxD Phase Facilitation (post-ORCA)

Run IxD as a structured flow-by-flow session. One flow at a time. Do not write all flows upfront — design each one interactively, lock it, then move to the next.

### Session pattern

1. Name each flow with a number AND an illustrative name: "Flow 3 — The Accordion". Names aid recall and communication.
2. Before writing steps for a flow, ask 1-2 clarifying structural questions. Surface assumptions early. Wrong assumptions caught before writing are cheaper than rewrites.
3. Write steps as a numbered code block. Use em-dashes for sub-bullets within a step. Keep it precise, not verbose.
4. End each flow with explicit open questions. Mark them clearly. Park them for proto validation rather than over-specifying.
5. Lock flows into a persistent file (ixd.md or equivalent) as you go. Do not keep state only in the conversation.
6. When a decision contradicts a previous constraint, call it out explicitly, resolve it, and update the constraints section. Do not silently patch.

### Structural decisions to resolve before writing steps

For any flow involving a picker/selector UI:
- Where does it live in the shell? (modal, new route, panel, inline)
- Does it replace or overlay the current surface?
- Is it triggered or always visible?

For any panel/sidebar UI:
- Which side? Left = navigation/selection (what you're working ON). Right = tools (what you apply TO it).
- Explicit dismiss or auto-close? Default to explicit dismiss — respects hesitation, safer for browsing.
- Does it conflict with other panels on the same side?

For any state model:
- How many states does the object actually need? Strip aggressively. Each state = more edge cases.
- Are two states mutually exclusive, or can an object be in both simultaneously?
- What triggers each transition? Is it a user action or a system event?

### IxD learnings from the_lorf session (2026-04-13)

**Canvas-as-workspace vs canvas-as-document.** When the output is a media snapshot (image, PDF), model the canvas as a persistent workspace and exports as immutable snapshots of it. No draft/archive state machine needed. Export = snapshot, canvas stays live. Simpler state model, better matches real batch-editing workflows (stamp out 5 newHires in a row).

**"Required fields" concept.** For WYSIWYG export tools, required fields add complexity with minimal benefit. Empty slot renders empty. What's on screen is what you get. Kill required field validation unless the domain explicitly demands it.

**Three-column shell rule.** For canvas-based editors: left panel = navigation/selection (what you're working on — slides, layers, pages). Center = canvas. Right panel = tools (what you apply — asset pickers, property controls). Establish this as a global shell rule early. It resolves panel placement questions for every subsequent flow automatically.

**Flat grid vs categorized template picker.** For internal tools with <~15 types, a flat visual grid with strong preview images outperforms a categorized picker. No taxonomy debt, no wrong groupings, users learn it fast. Add category filter bar as a v2 additive layer when count exceeds ~16. Grid math: 4-col, 32px gutters, 24px gaps on a 4px module grid = 286px previews at 1280px viewport. 8 items above fold at 768px height — acceptable for specialized tools.

**Post state simplification trigger.** If a user describes a batch workflow (stamp out multiple similar posts), that's a signal the state model is too restrictive. Active/archived with read-only archived state breaks batch workflows. Workspace model (always editable, exports are snapshots) fixes it.

**Tab close = data loss is acceptable when:** input volume is minimal, a recovery path exists (History tab with "Use as new post"), and the browser beforeunload dialog catches genuine misclicks. Do not build autosave infrastructure for tools with <5 fields per template.

**Backlog filing pattern.** When a feature is clearly post-MVP but architecturally sound, file it in the flow document with: what it is, why it's deferred, what infrastructure already supports it. Keeps the backlog discoverable without cluttering the MVP spec.

---

## Pitfalls

**Collection-words masquerading as objects.** Library, catalog, calendar, map, feed, inbox, gallery, dashboard — these are views of objects, not objects. Always ask: "what is one item in this?" The item is the object. The collection-word becomes a nav pattern or filtered list-view, designed later.

**Abstract nouns that are hoped-for outcomes.** Exposure, success, engagement, growth, trust, discovery — these cannot be stored, clicked, or owned. Cut them immediately. If a stakeholder fights you, ask: "Can a user open an Engagement and edit it?" If no, it's not an object.

**Jumping to layout or interaction before objects are validated.** Wireframes built on a wrong object model will be scrapped. The validation gate exists to catch this cheaply. Insist on it.

**CTA brainstorm revealing missing objects.** The most common source of new objects is the C step. When a CTA requires a noun not in the object list, that noun is a candidate object. Stop, add it, run O+R for it, then resume C. Do not silently embed it in an attribute.

**Forced ranking mistaken for layout order.** Attribute ranking #1 means most important to the user's comprehension of the object — it does not mean it goes at the top of the screen, in the nav, or on the card. Layout is an IxD decision. Make this explicit every time ranking comes up.

**Persistent nav and homepage designed first.** Nav and homepage are synthesis artifacts — they reflect the validated object model and key user flows. Designing them first is designing the answer before knowing the question. They are always last.

**Treating ORCA as waterfall.** The steps are ordered but not linear. CTA reveals objects (loop to O). Attributes reveal nested objects (loop to O+R). Validation fails (loop to O). Announce the loop when it happens so the user understands it's correct process, not backtracking.

---

## Sequencing — Full Design Process

```
1. Objects (O)
2. Relationships / Nesting (R)
3. CTAs (C)          ← loops back to O if new objects found
4. Attributes (A)    ← loops back to O+R if nested objects found
5. CTA Inventory     ← fill 6-field table per CTA
6. Validate          ← object-nav prototype + mental model test
7. Interaction Design (IxD) — flows, states, transitions
8. Layout — content priority per object view
9. Navigation patterns — reflect validated object hierarchy
10. Homepage — last
```

### IxD phase in practice

Maintain a dedicated ixd.md file. Structure:
- Prerequisites (object map version, slot inventory, decisions log — all pinned by path)
- Scope statement: flows/states/transitions only — no layout, no nav, no visual design
- Confirmed UI decisions section: lock resolved decisions here with rationale, source data, and backlog items
- Flows section: one subsection per flow

Flow naming convention: give each flow both a number and an illustrative name.
Format: `Flow N — [Evocative Name] ([functional description])`
Examples: "Flow 1 — The Blank Canvas (Core creation flow)", "Flow 3 — The Accordion (Carousel editing)"
The illustrative name aids recall and discussion. The functional description is the canonical reference.

Flow stub format:
- Write a numbered step sequence inside a code block
- Attach open questions directly below the code block, labeled "Open:"
- Mark flows as (IN PROGRESS), (NOT STARTED), or (DONE)
- Lock confirmed UI decisions into the "Confirmed UI decisions" section — remove them from Open

Competitive research during IxD:
When a UI pattern decision needs grounding (e.g. template gallery grouping, picker interaction models), use delegate_task with web toolset to run competitive analysis in parallel. The subagent researches how major tools solve the same problem. Synthesize findings yourself — extract the dominant patterns, name the tradeoffs, state your lean, present to the user. Do not outsource the synthesis or the recommendation.

UI decision locking checklist before moving to layout:
- All flows have step sequences written out
- All open questions resolved or explicitly risk-accepted
- Grid/spacing decisions recorded with math and source data
- Backlog items filed (future expansion ideas, post-MVP considerations)
- TODO items attached to specific flows or decisions (e.g. scrape for frequency data)

Do not begin step N+1 until step N is confirmed or explicitly risk-accepted.

### IxD phase in practice

Maintain a dedicated ixd.md file. Structure:
- Prerequisites (object map version, slot inventory, decisions log — all pinned by path)
- Scope statement: flows/states/transitions only — no layout, no nav, no visual design
- Confirmed UI decisions section: lock resolved decisions here with rationale, source data, and backlog items
- Flows section: one subsection per flow

Flow naming convention: give each flow both a number and an illustrative name.
Format: `Flow N — [Evocative Name] ([functional description])`
Examples: "Flow 1 — The Blank Canvas (Core creation flow)", "Flow 3 — The Accordion (Carousel editing)"
The illustrative name aids recall and discussion. The functional description is the canonical reference.

Flow stub format:
- Write a numbered step sequence inside a code block
- Attach open questions directly below the code block, labeled "Open:"
- Mark flows as (IN PROGRESS), (NOT STARTED), or (DONE)
- Lock confirmed UI decisions into the "Confirmed UI decisions" section — remove them from Open

App shell decisions belong in the confirmed section, not inside individual flows.
Classic three-column shell pattern: left = navigation/selection (what you're working ON), center = canvas (the work surface), right = tools/context (what you're working WITH). Both panels are independent — right panel does not displace left panel. Left panel is absent for view modes where selection isn't relevant.

State model discipline:
- Challenge every assumed state. "Draft" is only a state if the system actually needs to store and display unsaved work. If you export-or-nothing, draft is noise — cut it.
- Abandoned/orphan states are a scope call: localStorage + uuid-sub-url recovery is post-MVP unless the user has explicitly stated data loss is unacceptable at MVP.
- "Required slots" is a product philosophy decision, not a default. WYSIWYG (you export what you see, empty slots render empty) is simpler and more honest. Challenge required-field assumptions explicitly.

Competitive research during IxD:
When a UI pattern decision needs grounding (e.g. template gallery grouping, picker interaction models), use delegate_task with web toolset to run competitive analysis in parallel. The subagent researches how major tools solve the same problem. Synthesize findings yourself — extract the dominant patterns, name the tradeoffs, state your lean, present to the user. Do not outsource the synthesis or the recommendation.

Template gallery taxonomy research findings (from the_lorf session, 2026-04):
- Three dominant patterns: format-first (Canva, Figma), task/goal-first (Adobe Express, Notion), audience/role-first (Google Workspace)
- For non-technical internal users with fixed output format: flat visual grid with no grouping is valid up to ~12 items; category anchor-bar filter is additive post-MVP
- Optimal top-level category count: 5–9 (cognitive load research). 12 items flat with strong preview images is defensible for specialist tools
- Preview images are load-bearing UX, not decoration — user must identify the type in <2s from thumbnail alone
- Sort order for flat grid: hardcoded by frequency of use for MVP; scrape production data to validate before launch
- 4-column grid at 1280px with 32px gutters and 24px item gaps yields 286px per item — legible at a glance on smallest widespread desktop

UI decision locking checklist before moving to layout:
- All flows have step sequences written out
- All open questions resolved or explicitly risk-accepted
- Grid/spacing decisions recorded with math and source data
- Backlog items filed inline (future expansion ideas, post-MVP considerations)
- TODO items attached to specific flows or decisions (e.g. "scrape LinkedIn for frequency stats")

---

## References

- OOUX methodology: https://www.ooux.com/
- ORCA process overview: https://www.ooux.com/resources/orca
- Sofia Quintero's original OOUX articles: https://alistapart.com/article/ooux-a-foundation-for-interaction-design/
- Object-based UX wiki: https://www.ooux.com/learn
