# The Day of Reckoning & Dead City — A Two-Part Interactive Fiction Series

> **Two linked text-based games written in [Ink](https://www.inklestudios.com/ink/), set in the same zombie-apocalypse world and following the same characters across both stories.**
> Play them right in your browser or desktop using the free [Inky editor](https://github.com/inkle/inky/releases) — just open the `.ink` files and hit **Play**.

---

## 🔗 LinkedIn Introduction

*The following is a brief write-up suitable for sharing this project on LinkedIn:*

> I built a two-part, text-based interactive fiction series entirely in **Ink** (Inkle's narrative scripting language) — playable straight inside a chat-style interface with no graphics, no engine, just branching prose and decisions.
>
> **Game 1 — The Day of Reckoning:** A tense, linear rescue mission. You get a phone call from your sister Haley as a zombie outbreak engulfs the city. You have a time limit, a class to choose, and a route to fight through before it's too late. Every choice — how you cross a burning bridge, which items you scavenge, whether you run or fight — feeds into an injury and danger system that can end your run at any moment.
>
> **Game 2 — Dead City:** A full resource-management survival sim. You and the survivors you gathered in Game 1 (including Haley) hole up in an abandoned school. Each day you assign jobs — scavenging, farming, guarding, clearing zombie-infested rooms, healing — while managing food, water, medicine, materials, morale, and an ever-rising infestation pressure. Clear all 50 rooms and build 30 structures to win.
>
> The project demonstrates branching narrative design, simulation logic (utility-based NPC behaviour, randomised loot, multi-variable resource loops), and game balancing — all inside a single scripting language with no external libraries.

---

## 📖 About the Series

The two games share the same world and cast of characters. **The Day of Reckoning** covers the first hours of the outbreak; **Dead City** begins roughly a week later with the same group trying to survive long-term. You don't need to play Game 1 first, but doing so gives the characters in Game 2 a lot more meaning.

Both `.ink` files are self-contained and can be opened directly in the **Inky** editor (free, cross-platform).

---

## 🎮 How to Play

1. Download and install the free **[Inky editor](https://github.com/inkle/inky/releases)**.
2. Open either `DayOfReckoning.ink` or `DeadCity.ink`.
3. Click **Play** (the triangle button) in the top-right panel.
4. Read the text, click a numbered choice, and see where the story goes.

No installation beyond Inky is required. Both games run entirely as text.

---

## Game 1 — The Day of Reckoning

### Story
The zombie apocalypse has just begun. Trapped in gridlocked traffic, you receive a desperate call from your sister **Haley** — she's locked inside Room 203 of her school with her teacher and classmates. You have to reach her before time runs out and the situation becomes unrecoverable.

### Class Selection
Before you leave your car you choose a background, which shapes your abilities and available options for the whole run:

| Class | Perk | Difficulty |
|---|---|---|
| **Firefighter** | Starts with a fire extinguisher; higher danger resistance | Easy |
| **Police Officer** | Starts with a pistol and baton; highest combat danger resistance | Medium |
| **Runner / Gymnast** | Parkour ability; can bypass obstacles others cannot | Medium |
| **Civilian** | No gear; bonus scavenge luck (+10 % find chance & upper cap) | Hard |

### Core Systems

**⏱ Time Limit**
Every action advances a `time` counter. When `time` reaches **25** the game ends — Haley's situation becomes hopeless. Every decision about where to go and what to do trades precious time.

**⚠️ Danger & Injury**
A `danger` value accumulates as you encounter zombies and hazards. If it crosses a threshold relative to your `dangerResist`, you take an injury. Injuries stack; too many kills you. Medical supplies can be used at any point to heal, but they're scarce.

**🎒 Scavenging & Items**
The main hub — **Hardstone Street** — lets you branch off to scavenge cars, a fire truck, and a pawn shop before pressing on. Each location has one-time loot (flagged so it can't be double-collected):
- **Melee weapon / gun** — reduces danger from zombie encounters
- **Fire extinguisher** — suppresses the burning bridge obstacle
- **Ladder** — opens an alternative school-entry route
- **Healing supplies** — used to recover injuries on demand

Scavenge rolls are probabilistic (`baseFindChance` + class bonus, capped at `findChanceMax`), so the same run never plays out identically.

**🔀 Route Choices**
You can reach the school via a **burning bridge** (suppressed by an extinguisher or run through with fire damage) or a **crumbling footbridge** (multiple crossing strategies, each with injury risk). The path you take, your class, and the items you carry all interact to produce different outcomes.

---

## Game 2 — Dead City

### Story
A week after the outbreak. You, Haley, and four other survivors have barricaded themselves inside an abandoned school. Eight rooms are cleared; forty-two remain overrun. Resources are dwindling, morale is fraying, and zombie pressure rises every night. You are the leader. Every day you decide who does what — and the consequences compound.

### Your Survivors (starting group)

| Name | Strengths | Notes |
|---|---|---|
| **Haley** | Balanced (scavenge 3, farm 3, guard 10) | Your sister from Game 1 |
| **Marcus** | Elite doctor (tier 5) | Heals the whole group at once |
| **Chen** | Builder & farmer (farm 4, build) | Most efficient at construction |
| **Sofia** | Elite scavenger (tier 5) | Finds the most supplies per run |
| **Rodriguez** | Elite room clearer (tier 5, guard 20) | Best zombie fighter |
| **Elena** | Low morale, high fear, low loyalty | A liability — handle carefully |

Four more **rescuable survivors** are hidden in the building and unlock at room milestones (15, 25, 35, 45).

### Core Systems

**📅 Day Loop**
Each day you assign a job to every available survivor, then end the day. Resources are consumed, jobs execute (with skill-tier-based outcomes), events may fire, and zombie pressure rises. Repeat until you win or the group collapses.

**📦 Resources**
Four tracked supplies — `foodSupply`, `cleanWater`, `medicineSupply`, `materialSupply`. Each day the group consumes food and water per person. Running out triggers crisis events. Build **farmhouses** and **water wells** for passive daily income.

**🧟 Infestation Pressure & Guards**
Zombie pressure increases every day. Once it crosses thresholds, you need a minimum **guard score** on night watch or the group suffers a deadly breach. Guards don't reduce infestation — only **room-clearing** does. This creates a constant tension between spending labour on clearing (long-term safety) versus guarding (short-term survival).

| Infestation | Guard score needed |
|---|---|
| 0–9 | None |
| 10–24 | 5+ |
| 25–49 | 15+ |
| 50–69 | 25+ |
| 70–89 | 35+ |
| 90–99 | 50+ |
| 100+ | 70+ |

**🏗 Buildings**
Spend `materialSupply` to construct up to 30 buildings (10 farmhouses, 10 water wells, 5 guard towers, 5 medic tents). Buildings provide passive bonuses every day. Completing all 30 is one of the two win conditions.

**🎭 NPC Simulation**
Every survivor has individual `health`, `fatigue`, `hunger`, `morale`, `fear`, `grief`, `trust`, and `loyalty` values that shift based on events and how you treat them. Elena's resentment can boil over into theft. Haley can fall sick. A utility-jitter constant (`UTILITY_JITTER_MAX = 15`) adds randomness to NPC decision-making so behaviour isn't perfectly predictable.

**🏆 Win Condition**
Clear all **50 rooms** and build all **30 buildings**. Both conditions must be met. Lose if the group is wiped out, resources hit zero and trigger an unrecoverable crisis, or morale collapses.

---

## 🛠 Technical Notes

- Both games are written entirely in **[Ink](https://www.inklestudios.com/ink/)**, a narrative scripting language designed for interactive fiction.
- No external libraries, game engines, or build steps required.
- The Ink runtime can also be embedded into Unity or web projects via [inkjs](https://github.com/y-lohse/inkjs) if you want to deploy these games online.
- All logic — probability rolls, resource arithmetic, NPC utility functions, conditional narrative — is implemented in pure Ink using `VAR`, `CONST`, functions, tunnels, and knots.

---

*MIT Licensed. See [LICENSE](LICENSE) for details.*
