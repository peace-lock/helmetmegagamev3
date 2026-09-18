# Brewing

Every recipe a brewer can make, with its real cost. Price a new brew off these
tables, not by feel. If you change a number here, also change the tag's
`requirement` block in `docs/tags.yaml` and the row in the **Alcohol & Drugs**
document in `docs/documents.yaml`.

**Brewing has no tier ladder.** Smithing prices a weapon by picking a tier
(`SMITHING.md`); brewing prices each recipe on its own, because the real cost
is usually the ingredient rather than the ⬢. So the tables below are the
ladder — there is nothing above them to derive a price from.

**This paragraph used to say no code enforced any of it, and then that only
the ingredient was on the honour system. Neither is true any more.** The Craft
flow charges the ⬢, spends the Move, checks the skills — and **every
ingredient in the tables below is a real tag that the craft SPENDS**
(`Tag.requirementItems`, `CORPSES.md` §8). Three units of a brew take three
units of its ingredient, the same way they take three lots of ⬢. There is no
prose ingredient left in brewing: the ones nothing could ever track were either
turned into real tags (`aberrant-heart`, `ravens-eye`) or
dropped, with the ⬢ raised to be the gate instead.

**One exception, kept rather than spent.** `bone-mask` matches any corpse and
only needs the body *to hand*. That is what a `group:` ingredient means and the
only thing it can mean: a group names no single stack to take a unit out of.
Everything else spends.

**Ingredients go in when the work STARTS**, the rule the ⬢ already lived
under — so a multi-turn project pays up front and abandoning it keeps
nothing. The finishing audit row records what was spent
(`details.consumed`), for a GM reversing the work by hand.

Moonshine is the only recipe in the game that costs **0 ⬢** and still has a
real ingredient, and that is deliberate rather than an oversight: the marsh
hands you the Godflesh, the throttle is the Routine, and at 3 ⬢ a bottle it
undercuts a farming day badly enough to be nobody's living. What it costs is
the drinker's eyes, a notch at a time (`FACTORY.md` §8) — and, since the pass
that made ingredients real, one whole Godflesh a bottle, which is what stops
it undercutting the Factory's refining.

## 1. Skills

| Slug | Name | pt | Gate |
|---|---|---|---|
| `brewing-basic` | Brewing I | 5 | none |
| `brewing-skilled` | Brewing II | 5 | `parentTag: brewing-basic` (cumulative, total 10) |
| `brewing-expert` | Brewing III | 5 | `parentTag: brewing-skilled` (cumulative, total 15) |

Brewing III is new with the medical pass — it exists to gate the five
medicines below that used to be a Medical crafter's work (§3a).

## 2. Brewing I

Every ingredient below is **spent** unless the row says *kept*. The Turns
column is the recipe's own `turnsCost`, a decimal share of a turn's work — so
four 0.25 Alcohol fill one Routine and a spare quarter takes more brewing. A
0 there is a free craft: no Move at all (CRAFTING.md §2).

| Brew | ⬢ | Turns | Ingredient | Consumes into |
|---|---|---|---|---|
| `bliss` | 0 | 0.5 | `cave-fungus` | `euphoric`, `high` (3t) |
| `alcohol` | 2 | 0.25 | — | `tipsy` (and up the ladder — §5a) |
| `moonshine` | **0** | 1 | `godflesh` | `tipsy` (ladder, §5a), `blind-drunk` (2t), `damaged-vision` |
| `molotov-cocktail` | 2 | **0** — free | `alcohol` | — |
| `cleaning-powder` | 2 | 0.5 | — | — |
| `antidote` | 4 | 0.5 | — | — |
| `cat` | 3 | 1 | `alcohol` | `night-vision` (1t) |

## 3. Brewing II

| Brew | ⬢ | Turns | Ingredient | Consumes into |
|---|---|---|---|---|
| `pure-luck` | 0 | 1 | `aberrant-heart` | `aberrant-luck` |
| `flawless-skin` | 2 | 0.25 | — | `otherworldly-beauty` |
| `graga-sweat` | 2 | 1 | `graga-sac` | `brutish-strength` |
| `deadeye-drops` | 2 | 1 | `cave-fungus` | `increased-accuracy` |
| `ravenheart-red` | 4 | 0.5 | `alcohol` | `tipsy` (and up the ladder — §5a) |
| `mulligan-potion` | 8 | 0.5 | — | — |
| `phrygian-tears` | 4 | 1 | `cave-fungus` | `phrygian-toxin` |
| `white-honey` | **3** | 1 | `honey` | — |
| `purifier` | 6 | 1 | `cave-fungus` | — |

White Honey spends a `honey` — a gm-catalog Depot import, which makes it one
of the HIDDEN recipes: off the Recipes tab, out of the Craft menu until the
brewer holds the jar. Its own `cures:` list (the medical pass, TAGS.md §5c) is
`poisoned`, `envenomated`, `phrygian-toxin` and `choking` — not literally every
poison in the catalog. `phrygian-tears` is the most potent poison in the game
and is `cave-fungus` distilled a great deal further than Bliss goes; it is
public, so the recipe stays in the book.

**Nothing cures {shell-shocked} any more.** Forgiveness was the one door out
and it is gone with the poppy chain. Shell Shocked's own copy already says no
MEDIC can treat it; there is now no still that can either.

`gunpowder-grenade` (now named **Crude Grenade**) left this table
altogether: it is smith's work now (Smithing II, `items-weapons`),
listed in the Smithing paper beside `black-powder` and the `bomb`. See
`SMITHING.md`.

An empty **Consumes into** cell is not an oversight. `consumable` with no
`consumesInto` is set where the brew is spent *by a Move* rather than by the
drinker — a poison you administer, a flask you throw, a powder worked into
someone else's wound — so the GM applies the result to whoever it happened to.

## 3a. The medicines (medical pass)

Eight recipes moved in from the old Medical craft when the medical pass split
crafting the medicine from treating the patient with it: three price at
Skilled, five at Expert — four of those hidden or secret, the Portable
Surgical Pack plainly visible. Brewing them is a `brewing`
craft now, billed off `craftFamily()` like any other brew (`CRAFTING.md`
§2a); Healing a patient with a Heal request, and fitting the two prosthetics
below with `administerSkill`, are still Medical III's job
(`MEDICAL.md` §2, `TAGS.md` §5c) — one Action carries one Move, shared
across families since 2026-09-15, so a medic can brew a batch and heal a
patient in the same turn, as long as both fit in the one Move.

These don't fit the **Consumes into** shape above — they're `Tag.cures`
items (`MEDICAL.md` §1), not status brews — so the last column is **Cures**
instead.

| Brew II | ⬢ | Turns | Cures |
|---|---|---|---|
| `antidote` | 4 | 0.5 | poisoned, envenomated |
| `fever-draught` | 3 | 0.5 | feverish, heatstroke, cave-fever |
| `burn-dressing` | 4 | 0.5 | burned, severe-burns |

| Brew III | ⬢ | Turns | Ingredient | Cures |
|---|---|---|---|---|
| `autoinjector` | 3 | 1 | `antidote` + `fever-draught` + `brackenmoss` (HIDDEN — needs the brewer to hold all three) | bruised, sprained-ankle, burned, minor-bleeding, minor-wound, dislocated-shoulder, cracked-ribs, blunt-force-trauma, frostbite |
| `portable-surgical-pack` | 8 | 1 | — | — (a surgical-site enabler, not a cure — `MEDICAL.md` §3) |
| `last-breath` | 11 | 3 (project) | `aberrant-heart` (secret) | dying |
| `cybernetic-arm` | 15 | 3 (project) | `cybernetic-core` (secret) | missing-arm |
| `cybernetic-leg` | 15 | 3 (project) | `cybernetic-core` (secret) | missing-leg |

`last-breath` and the two cybernetics are `catalog: secret` and hidden by
conjunction — the Craft menu only shows them to a `brewing-expert` already
holding the named ingredient (`MEDICAL.md` §6). `autoinjector` is `catalog:
all` but HIDDEN the ordinary way: off the Recipes tab until the brewer holds
`brackenmoss`, the non-public ingredient (`CRAFTING.md` §2b). Neither
cybernetic has an aftermath — the graft leaves no mark — while `last-breath`
cures Dying outright with no die, the one item door onto a tier-7 cure that
isn't a Gambit.

## 4. Ingredients

**Every ingredient is a real tag now.** There is no honour-system column left:
either the brewer's sheet carries the thing, or the craft is refused.

| Tag | Where it comes from | How the recipe uses it |
|---|---|---|
| `cave-fungus` | foraged in the caves — never crafted, since the pass that took its 0-⬢ recipe away. Eaten raw it only makes you `nauseous`; the high is what boiling it into Bliss is for. | spent |
| `alcohol` | brewed, one tier down (also what `ravenheart-red` is made of) | spent |
| `nekker-pheromones` | **butchered** out of a {Nekker Corpse} | spent |
| `graga-sac` | **butchered** out of a {Graga Corpse} | spent |
| `skinless-brain` | **butchered** out of a {Skinless Corpse} | sold, not brewed |
| `godflesh` | hauled out of the marshes (`FACTORY.md`) | spent |
| `aberrant-heart` | off a fallen Aberrant | spent |
| `ravens-eye` | forageable — the loot pass wires it | a Trinket inlay only; no recipe spends one |
| `honey` | Depot import, gm-catalog — the White Honey link is a secret | spent |
| `tea` / `sweets` / `honey` | Depot imports; the cook picks one | spent (`anyOf`) |
| **a corpse** (`items-corpse` group) | died, or was killed | **kept** |

(`saltpeter` left this table with the grenade — powder is smith's business
now, `SMITHING.md`.)

The forageable tags in that table are new, and **nothing drops them yet**. The
prospecting loot table is what would wire acquisition (`MINING.md` §3b); this pass
only had to make the slugs exist. Until then they arrive by GM grant.

`skinless-brain` is the one ingredient that is also a moral problem. A Graga is
a beast; the Skinless used to be people and, per the Caves brief, can be talked
down. No recipe spends one any more, but the
Merchant still buys them dearly, which asks the same question of whoever
carries one in.

**`nekker-pheromones` is no longer brewed at all.** It is butchered out of a
Nekker Corpse; it lost its `craftable` flag and its row in §2.

**What used to be prose, and where it went.** An Aberrant's heart and a raven's
eye became `aberrant-heart` and `ravens-eye`. A willing lover's blood, someone's
tears and a lock of Nobility hair are simply gone, with the ⬢ carrying the gate
instead (§3). The old argument for keeping them — that getting one should be a
scene rather than a purchase — held for the social ones and never held for the
huntable ones, where there was no player on the other side, just a GM ruling on
whether somebody's fishing trip counted.

## 5. Yields

Two different numbers used to share one field here; they are two concepts
now (CRAFTING.md §2, Chris 2026-09-06). A brew that comes out in a batch
authors its WORK as a decimal — `turnsCost: 0.25` — and the arithmetic does
the rest: four Alcohol fill one Routine, one Alcohol leaves 0.75 of it for
other brewing work. A hard RATION — `perTurn`, 0-turn recipes only — caps a
0-turn brew at its own number, and only its own: there is no shared pool
behind any `turnsCost: 0` recipe any more, on the smithing/crafting Dead
Simple rung or here (`SMITHING.md` §2).

They shared a column as well as a table until 9/2026: a fractional cost was
stored as its denominator in `requirementPerTurn`, the same column the ration
lives in. Costs are decimals now and that column is a ration and nothing else.

| Brew | turnsCost (work each) | perTurn (ration) |
|---|---|---|
| `alcohol` | 0.25 | — |
| `lavish-meal` | 0.25 | — |
| `honeyed-cakes` | 0.25 | — |
| `fine-meal` | 0.25 | — |
| `trail-ration` | 0.25 | — |
| `flawless-skin` | 0.25 | — |
| `musk-lure` | 0.25 | — |
| `bone-mask` | 0.25 | — |
| `cleaning-powder` | 0.5 | — |
| `antidote` | 0.5 | — |
| `ravenheart-red` | 0.5 | — |
| `bliss` | 0.5 | — |
| `mulligan-potion` | 0.5 | — |
| `molotov-cocktail` | **0** — free | — |

**The ration column is empty now.** Every recipe that used to read "up to N a
turn" costs a quarter of a Move instead — the ration was the last of the old
system, and a quarter-Move says the same thing without a second mechanism.
`molotov-cocktail` is the one free craft left: no Move, no cap, and the bottle
of alcohol is the whole price.

**The ⬢ cost is per unit, and it multiplies.** Three alcohols in one turn cost
6 ⬢, not 2. Every yield row in the document carries an `{info:…}` tooltip
saying so, since the table itself has no room to.

## 5a. The drinking ladder

Every drink still consumes into `tipsy` and none of them names anything else.
The escalation lives on the status tags themselves, as `Tag.escalatesInto`
(`docs/tags.yaml`, `db/prisma/schema.prisma`), so a new brew gets the ladder
for free by consuming into `tipsy` like the rest.

| You are | You drink | You become |
|---|---|---|
| sober | anything alcoholic | **Tipsy** (1t) |
| **Tipsy** | again | **Wasted** — the Tipsy comes off |
| **Wasted** | again | **Unconscious** |
| **Unconscious** | — | nothing; you cannot act |
| **Hangover** | again | **Tipsy**, and round it goes |

**Wasted** and **Unconscious** both expire into **Hangover** (1t) through the
ordinary `expiresInto` machinery — the same road `seizure` takes to `stupid`,
with no new turn pass.

**Unconscious is in `INCAPACITATING_SLUGS`** (`db/lib/incapacitation.js`): out
cold is out cold, so you can be looted, dragged and tied up where you fell. It
is deliberately **not** in `FINISHABLE_SLUGS` — passing out in a tavern is not
a death sentence anyone can carry out without a GM.

Three things that are easy to get wrong:

- **Only the consume path climbs.** `db/lib/tagWrites.js#grantTagSlugs` is
  shared with `removesInto`, Undo and every GM grant, and it stays deliberately
  ignorant of the ladder. A GM handing somebody Tipsy twice from the Dev Panel
  does nothing the second time, which is correct — that is not a drink.
- **The walk starts from the rung you occupy, not the one being granted.**
  Somebody already Wasted does not hold Tipsy, so a naive "do they hold what
  I'm granting?" test would pour them a fresh Tipsy instead of putting them on
  the floor. `web/lib/consumeGrants.js#climbLadder` owns this.
- **The top rung is a no-op, not a fall.** Drinking while Unconscious clears
  nothing and grants nothing. Clearing a rung without granting its successor
  would make one more drink *sober you up*.

The Fighting penalties on all three tags are **prose, not code** — nothing in
the repo reads `tipsy`. They are numbers a GM weighs while adjudicating, which
is how Tipsy has always worked.

**Lightweight and Iron Liver** reshape the climb, in `web/lib/
consumeGrants.js#resolveConsumeGrants`. Lightweight sends the character's
*first* drink straight to the second rung (Sober → Wasted, skipping Tipsy).
Iron Liver does the opposite to a climb already underway: it costs a drink to
grant a hidden `holding-it-down` marker instead of climbing, and only the
drink after that actually climbs (clearing the marker too) — so an Iron Liver
drinker paces at 1 drink → Tipsy, two more → Wasted, two more → Unconscious.
The catalog's `conflictsWith` keeps a character from holding both at once. The
three slugs (`lightweight`, `iron-liver`, `holding-it-down`) are duplicated by
hand at the top of `consumeGrants.js`, because that file is imported by client
components (`TagRail.js`, `RequestActionsProvider.js`) and pulling
`@lifeweb/db/lib/constants` into the browser bundle isn't an option — keep
them in sync with `db/lib/constants.js` if either ever changes.

Brewing files its Routine through the Craft button, same as any other
craftable tag — `phrygian-tears` no longer carries `gambit: true`, since
crafting is never a Gambit (`CRAFTING.md`).

## 6. Where a player reads this

The **Alcohol & Drugs** document (`docs/documents.yaml`, key `alcoholdrugs`)
carries ⬢, turns, the batch yield and the ingredient, and nothing else. A
yield row also carries an `{info:…}` token — a `?` glyph whose payload is its
own tooltip sentence, rendered by `DocumentMarkdown.js`. What a brew *does*
lives in the tag's own description and shows on hover — `TagChip.js` renders
the description plus a **Recipe** line built by
`formatTagRequirement` (`db/lib/formatTagRequirement.js`) from the same
`requirement` block these tables come from. Don't restate an effect in the
document; it is already two places.


## Brewing (Distilling)

A `mastery` tag (`TAGS.md` §4a) gated on Brewing II: every brewing
recipe yields **two** of its item for the price of one.

The doubling lives in `grantCrafted` (`web/app/(app)/character/requestActions.js`),
the single grant every craft path funnels through, rather than beside its three
callers — and deliberately **downstream of the ingredient plan and the ⬢
spend**, both of which are computed from `quantity` and must stay that way.
Doubling the cost as well would make the tag do nothing.

Two details that are easy to get wrong:

- **The family is read off `baseTag ?? tag`, not `tag`.** When a recipe mints a
  custom row the minted tag carries no `requirementSkills`, so `craftFamily()`
  would read it as the generic `craft` and quietly stop doubling.
- **The audit row's `quantity` stays the RECIPE RUNS**, not the units granted.
  The per-turn rations in `web/lib/requests.js` count that field, so billing
  the doubled output would halve a Distilling brewer's own `perTurn`
  allowance on a 0-turn recipe. What actually landed is recorded beside it as
  `granted` when the two differ.

A non-stackable brew is unaffected: `addToStack` pins one to quantity 1 however
many times it is granted.
