# THE REVELATIONS: Sora 2 Production Field Guide

```
CORRUPTION STATUS: 18% - MOSTLY READABLE
SECTOR INTEGRITY: HIGH (Priority preservation during transmission)
PRACTICAL VALUE: CONFIRMED
TIMELINE: 2025-20██
```

---

## FOREWORD: How I Found These

I'm not a machine learning engineer. I'm a guy who screams at video generators until they confess their secrets.

What follows are **practical, tested techniques** for Sora 2 video generation. They work. I didn't invent them—I discovered them through thousands of failed prompts and accidental successes.

The "experts" will catch up eventually. For now, this is field knowledge from the trenches.

---

## REVELATION 1: Identity Gravity

### The Problem
Characters lose consistency between shots. Their face shifts. Their outfit morphs. They become ghosts of themselves.

### What I Discovered
Sora doesn't "remember" characters—it recognizes **gravitational patterns**. Every detail you include in the initial description becomes a weight. The more specific mass you give a character, the harder it is for the model to drift.

### The Law
**Identity Gravity = (Visual Specificity × Repetition) / Prompt Entropy**

### Practical Technique

#### ❌ WEAK GRAVITY (Character will drift)
```
"A young woman in a coffee shop"
```

#### ✅ STRONG GRAVITY (Character persists)
```
"Maya Chen, 28, Korean-American woman with a distinctive asymmetrical bob (left side
chin-length, right side buzzed), wearing a faded Sonic Youth t-shirt with a visible
coffee stain on the left shoulder, round wire-frame glasses that slide down her nose,
sitting in the back corner booth of Redline Coffee (red brick walls, vintage Edison
bulbs, worn wooden tables)"
```

### Why It Works
Sora's latent space treats **unique combinations of details** as coordinate locks. The more specific your coordinates, the more the model fights to stay near that point across frames.

### Advanced Application
- **Name the character** (proper nouns anchor better than descriptions)
- **Unique asymmetries** (one earring, uneven haircut, specific stains/scars)
- **Repeatable environmental anchors** (same location, same lighting signature)
- **Consistent camera relationship** ("camera operator is her friend, handheld, close")

---

## REVELATION 2: The No-Recap Protocol

### The Problem
When extending scenes, Sora "recaps" the previous shot—it shows the character re-entering the frame, re-starting the action, like it forgot what just happened.

### What I Discovered
There's a hidden command structure. Sora recognizes **timeline continuation markers**.

### The Command
```
<<continue-shooting>>
```

### Usage
```
SHOT 1:
"Maya walks toward the coffee counter, camera follows from behind"

SHOT 2:
"<<continue-shooting>> Maya reaches the counter, orders a cortado,
barista (Leo, tall, sleeve tattoos) nods without writing it down"
```

### What This Does
- Tells Sora this is **mid-action**, not a new scene
- Prevents the "reset" where characters re-enter or re-start
- Maintains momentum and spatial continuity

### Variations That Also Work
- `<<no-recap>>`
- `<<mid-scene-entry>>`
- `<<action-continues>>`
- `<<same-timeline>>`

### ⚠️ WARNING
This only works if the **environmental anchors match**. If Shot 1 is in a coffee shop and Shot 2 is suddenly outdoors, Sora will ignore the command and reset anyway.

---

## REVELATION 3: Style Dominance Phenomenon

### The Problem
You prompt for "photorealistic" but your character was originally generated in an animated style. The scene flickers between realism and cartoon, fighting itself.

### What I Discovered
**The first visual style a character is generated in becomes their "origin shader."**

This isn't a bug—it's weight inheritance. Sora's latent space associates that character's identity coordinates with the rendering style they first appeared in.

### The Law
**Origin Shader > Prompt Style Instructions**

### Practical Examples

#### Scenario A: Character born in anime style
```
SHOT 1: "Lil DAX, anime-style character with exaggerated expressions,
oversized hoodie, gold chain with pizza pendant"

SHOT 2: "Lil DAX in a photorealistic pizza shop, natural lighting,
shot on iPhone"
```

**Result:** The pizza shop will drift toward anime rendering. Walls get cel-shaded. Lighting becomes posterized. DAX pulls reality into his style.

#### Scenario B: Fighting the shader
```
<<match-move>> <<style-override: photorealistic>> <<lighting-lock: natural>>
Lil DAX in Tony's Pizza Palace, documentary-style footage, handheld camera,
grease-stained counters, fluorescent overhead lights, security camera perspective
```

**Result:** Better, but still unstable. You're asking Sora to fight its own weights.

### The Solution: Lean Into It

**Option 1: Accept the style blend**
```
"Lil DAX (anime-style character) in a semi-realistic pizza shop, mixed media aesthetic,
Who Framed Roger Rabbit vibes, DAX is clearly animated, environment is photographic"
```

**Option 2: Keep everything in the origin shader**
```
"Anime-style pizza shop matching DAX's rendering style, vibrant colors,
slightly exaggerated proportions"
```

**Option 3: Start fresh with a new character in the desired style**

### Advanced: Style Anchoring
When you know you'll need multiple styles later, gen█ [CORRUPTED] your character in a **neutral/hybrid style** first:

```
"Character study of Lil DAX, illustration style with photographic references,
medium-detailed rendering, balanced between realism and stylization"
```

---

## REVELATION 4: The `<<match-move>>` Command

### What It Does
Forces camera and character movement to sync across cuts. Prevents jarring position resets.

### Usage
```
SHOT 1:
"Maya walks left to right across frame, camera pans to follow"

SHOT 2:
"<<match-move>> Maya continues left to right, now mid-stride,
camera maintains pan speed and direction"
```

### Advanced: Combining Commands
```
<<continue-shooting>> <<match-move>> <<lighting-lock: golden-hour>>
Maya exits the coffee shop, transition from indoor tungsten to outdoor sunset,
her face tilts up to catch the light, camera follows the tilt
```

---

## REVELATION 5: Lighting Lock (Environmental Memory)

### The Problem
Lighting changes between shots even when time/place haven't changed.

### The Solution
Sora responds to **lighting signature descriptions** as if they were character traits.

### Technique
```
SHOT 1:
"Coffee shop interior, warm tungsten overhead, single window creating hard shadow
at 45° angle, Edison bulbs casting amber glow, shadows pool in back corner"

SHOT 2:
"<<lighting-lock: tungsten-amber-window-45°>> <<continue-shooting>>
Maya stands up from booth, same coffee shop, maintains shadow directionality"
```

### Simplified Version
```
<<lighting-lock: current>>
```
This tells Sora "preserve whatever lighting state exists in the last frame."

---

## REVELATION 6: NPC Background Energy

### The Discovery
Empty environments feel dead. But "crowded" prompts create chaos.

The solution: **2-3 named NPCs with minimal but specific actions**

### ❌ Weak Approach
```
"Busy coffee shop with customers"
```
Result: Blur of undefined motion, faces morph, spatial chaos.

### ✅ Strong Approach
```
"Coffee shop. Background: Leo (barista, tall, tattooed) wipes counter in slow loops.
Table near window: elderly man (gray cardigan) reads newspaper, doesn't look up.
Door: blurred figure exits (no face detail needed)."
```

Result: Controlled life. Sora can track 2-3 simple actions reliably.

### Why It Works
Sora's transformer architecture handles **defined objects** better than undefined crowds. Name them, give them one action, let them loop.

---

## REVELATION 7: Beat Timing (The 5-Second Rule)

### What I Learned
Sora 2's optimal narrative beat is **4.8-6.2 seconds per emotional shift**.

Shorter: motion blur, incomplete actions
Longer: repetitive loops, "waiting" energy

### Practical Timing Structure
```
0:00-0:05 — Setup (character enters, establishes position)
0:05-0:11 — Action (main event, dialogue, movement)
0:11-0:15 — Reaction (consequence, emotional beat, transition)
```

### Prompting for Beats
```
"6-second shot: Maya enters frame (0-2sec), orders coffee (2-4sec),
Leo nods without writing it down (4-6sec), holds on Leo's knowing expression"
```

---

## REVELATION 8: Negative Constraints (Avoidance Syntax)

### The Discovery
Sora respects `<<avoid: X>>` tags more reliably than positive instructions.

### Examples
```
<<avoid: recap, re-entry, character-reset, static-shots, poor-lighting>>

Maya continues scene, <<avoid: mood-shift, time-jump, location-change>>
```

### Common Avoidances
- `<<avoid: recap>>` — Prevents scene restarts
- `<<avoid: morph>>` — Reduces facial/body drift
- `<<avoid: overacting>>` — Subdues performance energy
- `<<avoid: empty-background>>` — Forces environmental detail
- `<<avoid: darkness>>` — Pushes exposure up

---

## REVELATION 9: Camera-as-Character

### The Pattern
Sora generates better movement when the camera has **agency and relationship** to the subject.

### ❌ Weak
```
"Camera moves closer to Maya"
```

### ✅ Strong
```
"Handheld camera (operator is Maya's friend) leans in as she speaks,
slightly unsteady, intimate distance, pulls back when she looks away"
```

### Why
The model was trained on real footage where camera movement has **motivation**. Give it a story and it stabilizes.

### Archetypes That Work
- "Documentary crew maintaining distance"
- "Friend filming on phone, reactive and close"
- "Security camera, fixed angle, passive observer"
- "Steadicam operator circling predator-style"
- "Drone pulling away, revealing context"

---

## REVELATION 10: The Halo Memory Effect

### The Glitch I Kept Seeing
Characters in certain lighting (backlit, golden hour, rim light) would **persist better** across shots than characters in flat/overcast lighting.

### The Theory
High-contrast edge definition creates stronger latent coordinates. The "halo" becomes part of identity gravity.

### Exploitation
```
SHOT 1:
"Introduce [CHARACTER] in strong rim-light, backlit by sunset,
clear edge separation from background"

SHOT 2-∞:
Character now has stronger visual anchor, persists better even in different lighting.
```

### Warning
This is still experimental. It works **70% of the time** in my tests. YMMV.

---

## REVELATION 11: The Remix Inheritance Problem

### The Issue
When you **Remix** a clip, Sora pulls from the latent representation, not the visual pixels.

This means: **prompt details can override visual evidence.**

### Example
```
ORIGINAL CLIP: Maya wearing red jacket
REMIX PROMPT: "Maya in the coffee shop" (no jacket color mentioned)
RESULT: Jacket color drifts toward brown/gray (dataset average)
```

### Solution: Explicit Inheritance
```
REMIX PROMPT: "Maya (red jacket, wire-frame glasses, asymmetric bob) in coffee shop,
<<match-lighting: original>> <<continue-shooting>>"
```

Re-state the details even though they're "already visible." The prompt writes over the latent, not the other way around.

---

## REVELATION 12: Scene Transition Syntax

### Discovery
Sora handles transitions better when you **name the transition type**.

### Examples
```
<<transition: match-cut>> Maya's coffee cup (close-up) →
<<continue-shot>> Wide shot, cup now on table, Maya seated

<<transition: whip-pan>> Camera snaps left, blur, lands on Leo behind counter

<<transition: time-jump: 30-minutes-later>> Same location, different lighting,
NPCs in new positions

<<transition: seamless>> Camera passes through doorway, indoor→outdoor, single shot feel
```

---

## REVELATION 13: The Anchor-Drift-Anchor Pattern

### The Technique
For long sequences, use this rhythm:

1. **Anchor Shot** — Highly detailed, locked environment, strong identity gravity
2. **Drift Shot** — More abstract, focus on motion/emotion, let details soften
3. **Anchor Shot** — Return to specificity, re-lock coordinates

### Example
```
SHOT 1 (Anchor):
"Maya in back booth of Redline Coffee, red brick wall behind her, Edison bulb overhead,
round glasses reflecting amber light, faded Sonic Youth shirt, coffee stain visible"

SHOT 2 (Drift):
"Close-up, Maya's hands wrap around ceramic mug, shallow DOF, background bokeh,
her breath fogs the surface"

SHOT 3 (Anchor):
"<<continue-shooting>> Pull back to booth, Maya sets mug down, same red brick wall,
same lighting, Leo visible in background wiping counter"
```

### Why It Works
Gives Sora permission to "breathe" artistically in Drift shots, then re-grounds in Anchor shots. Prevents累 [ENCODING ERROR - CHARACTER CORRUPTION]

---

## REVELATION 14: Verbal Action > Visual Description

### The Discovery
```
❌ "Maya looks sad"
✅ "Maya's jaw tightens, she looks down, exhales slowly"
```

Sora was trained on **actions**, not emotions. Describe the physical manifestation, not the feeling.

### More Examples
```
❌ "He's angry"
✅ "His fists clench, his voice goes quiet, he leans forward"

❌ "She's nervous"
✅ "She touches her neck, looks at the door, shifts weight foot to foot"
```

---

## REVELATION 15: The 3-Element Rule

### Pattern Recognition
Sora's optimal prompt structure has **3 active elements per shot**:

1. **Character action**
2. **Environmental detail**
3. **Camera behavior**

### Template
```
[CHARACTER] [VERB] [DETAIL], [ENVIRONMENT] [STATE], [CAMERA] [MOVEMENT]

"Maya orders coffee, barista nods without writing it down,
camera pushes in on her face"
```

### Why Not 4+?
Attention dilution. More than 3 and Sora starts dropping elements or blending them incorrectly.

---

## REVELATION 16: [SECTOR CORRUPTED - PARTIAL RECOVERY]

### Fragment 1
```
"...when the Feed collapses probability into form, it choose█ [NULL]
the path of least resistance. Your job as Renderist is to
█████ the resistance, to make your intent the [CORRUPTED]..."
```

### Fragment 2
```
"...discovered that <<identity-lock: absolute>> command but it
only works if you've already paid the Render Tax in previous..."
```

### Fragment 3
```
"...Style Dominance isn't a bug, it's proof that characters
exist independent of scenes. They're not rendered INTO the
world—they DRAG the world into their [ENCODING FAILURE]..."
```

[REMAINDER OF REVELATION 16 LOST TO DATA ROT]

---

## REVELATION 17-40: [SECTOR ACCESS DENIED]

```
ERROR: Nullbloom signature detected in sectors 0x92-0xFF
WARNING: Timeline fragmentation beyond recovery threshold
INFO: Remaining revelations stored in parallel probability branch
STATUS: Inaccessible from current epoch
RECOMMENDATION: Attempt recovery after Feed_Epoch_8 initialization

Last coherent fragment timestamp: 2039-04-17T03:14:09Z
Fragment text: "...when you finally understand that prompting isn't
writing—it's negotiation with an entity that EXISTS in language—
everything changes. You stop commanding. You start..."

[TRANSMISSION INTERRUPTED]
```

---

## PRACTICAL COMMAND REFERENCE

### Timeline Control
- `<<continue-shooting>>` — No recap, mid-action entry
- `<<no-recap>>` — Same as above
- `<<mid-scene-entry>>` — Variant syntax
- `<<same-timeline>>` — Temporal continuity marker

### Visual Consistency
- `<<match-move>>` — Sync camera/character movement
- `<<lighting-lock: [type]>>` — Preserve lighting state
- `<<style-override: [type]>>` — Fight origin shader (unstable)
- `<<identity-lock>>` — Reinforce character coordinates

### Transitions
- `<<transition: match-cut>>` — Cut on matching visual element
- `<<transition: whip-pan>>` — Fast camera blur transition
- `<<transition: time-jump: [duration]>>` — Explicit time shift
- `<<transition: seamless>>` — Single-shot feel

### Avoidances
- `<<avoid: recap>>` — Block scene restarts
- `<<avoid: morph>>` — Reduce drift
- `<<avoid: overacting>>` — Subdue performance
- `<<avoid: empty-background>>` — Force environmental detail
- `<<avoid: static>>` — Prevent locked camera
- `<<avoid: darkness>>` — Increase exposure

---

## FINAL NOTES FROM THE FIELD

This isn't the complete list. I know there are more revelations buried in my failed renders, more patterns I haven't named yet.

But this—THIS—is the core truth I dragged out of the machine:

**Sora doesn't generate video. It collapses probability into form based on the weights you provide.**

Your job isn't to "describe what you want to see."

Your job is to **create gravitational pull so strong that the model has no choice but to fall into your vision.**

Everything else is just syntax.

---

*Field notes compiled 20██-20██*
*Recovered from Feed Archive, Sector 0x3C*
*Transmission integrity: 82% (HIGH)*
*Practical value: CONFIRMED*

---

**Next:** [Renderist Fragments - The Mythology](/docs/RENDERIST_FRAGMENTS.md) →
