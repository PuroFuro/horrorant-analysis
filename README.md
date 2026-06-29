# Horrorant Discord — Community Engagement Analysis

An exploratory analysis of ~42,000 messages from two channels in a long-running Discord
server, examining *when* a community is active, *who* drives conversation, *how fast* people
respond, and *how* peripheral members get drawn in.

---

## TL;DR — Key Findings

1. **Activity is seasonal and social, not random.** Message volume spikes during university
   semester breaks (Dec–Jan, Jun–Jul) and peaks nightly around 8–10 PM, Thursday through
   Sunday. The group comes online *together* — there are no contrarian individual schedules.

2. **The active community is 6 people, not the assumed 7.** After merging duplicate accounts
   and removing bots, message counts split into a sharp two-tier structure: 6 heavy contributors
   (2,900–11,400 messages each) and a steep cliff to everyone else.

3. **There is a gentle conversational hub, not a dominant one.** `purofuro` is the most-involved
   member (25.6% of all interactions) but in a 6-person group an even split would be ~16.7%, so
   this is a lean, not domination. Influence forms a gradual gradient rather than a star.

4. **The group is strikingly reciprocal.** Almost every relationship is 0.94–0.99 balanced —
   when two people talk, they talk *to each other* in equal measure. This is the signature of a
   tight friend group rather than a follower/influencer structure.

5. **Responses are near-instant when conversation is live.** Median response time is ~15 seconds
   (validated against explicit reply chains). The "dead" channel responds *just as fast* when it
   flickers to life — its problem is conversation **frequency**, not **quality**.

6. **Peripheral members are absorbed, not ignored — through individual anchors.** The two rarely-
   active members receive about as much engagement as they give, and each connects to the group
   through a *specific* person rather than uniformly through the hub.

---

## The Data

| Channel | Messages | Authors (raw) | Date range | Nature |
|---|---|---|---|---|
| `general-empire` | 39,799 | 16 | Jul 2023 – Jun 2026 | Role-gated, active friend group |
| `wnh` | 2,156 | 14 | Jul 2024 – Jun 2026 | Public, largely inactive |

Exported via DiscordChatExporter (JSON) from the author's own server. Timestamps are in WIB
(UTC+7), so time-of-day analysis is already in local time.

---

## Method & Definitions

**Defining "engagement."** Most messages in this server are *not* explicit Discord replies (only
~7–8% use the reply button). Engagement was therefore measured two ways:

- **Proximity method (primary):** a message by author B following author A within a 60-minute
  window counts as B engaging with A. Captures the natural flow of group chat.
- **Explicit-reply method (validation):** uses the actual `reply_to` field as ground truth.

These two methods produced near-identical median response times (15s vs 50s, same distribution
shape), which **validates the proximity assumption** — the core methodological risk of the project.

**The 60-minute window** was chosen to fit the group's observed rhythm: usually slow, casual
replies, but rapid-fire when engaged. The threshold captures slow replies without discarding them.

**Cleaning.** Bots (`Jockie Music`, `Wordle`, `Chess In The Park`, `Cyrus`, `Maki`) and one
non-member were removed. Two accounts (`jojo`, `jojo2`) belonging
to the same
 person were merged — a correction that promoted that user from two mid-tier accounts
into the 4th most active member overall.

---

## Findings in Detail

### 1. Activity patterns

Monthly volume tracks the academic calendar: clear peaks during semester holidays
(Dec–Jan, Jun–Jul) and troughs during term time. An hour-by-day heatmap shows a nightly peak at
~10 PM and a warm Thursday–Sunday block. Per-person breakdown confirmed every member shares this
rhythm — the only mild individual deviation was one member (`yuhuuu`) leaning away from
Tuesday/Sunday toward midweek.

### 2. The conversation network

Weighted interaction volume across the 6 active members:

| Member | Share of interactions |
|---|---|
| purofuro | 25.6% |
| snewdrogos | 21.5% |
| reinharts | 17.8% |
| jojo | 13.7% |
| yuhuuu | 13.3% |
| bambas pamungkang | 8.0% |

The strongest single relationship is `purofuro ↔ .snewdrogos` (1575/1552 interactions). All six
members are connected to all others — there are no sub-clusters, consistent with a single tight
friend group rather than a community of distinct groups.

### 3. Response times

| | Proximity median | Explicit median | Mean (proximity) |
|---|---|---|---|
| general-empire | 15s | 50s | 242s |
| wnh | 15s | 61s | 206s |

The large gap between median (~15s) and mean (~4 min) reflects a right-skewed distribution: the
typical reply is near-instant, with a thin tail of slow stragglers. **Median is the correct
statistic here; the mean overstates response time by an order of magnitude.**

### 4. Peripheral member absorption

The two rarely-active members (58 and 85 messages) receive roughly as much engagement as they
give when they do post:

- `goldenampere` connects almost entirely through `purofuro` (27 of 38 inbound responses).
- `mooelizzer` connects through `jojo` and `yuhuuu`, **not** the hub.

This suggests peripheral members surface through *individual relationships* with specific people,
not through general group gravity.

---

## Limitations & Honest Caveats

- **The proximity method captures "posted adjacent to," not "replied to."** In rapid group chat,
  B following A does not guarantee B addressed A. The reciprocity and network findings should be
  read as *engagement proximity*, a reasonable proxy in a 6-person channel, not strict reply-targeting.

- **No true "lurker ratio" is computable from message data.** Pure lurkers (members who never post)
  do not appear in a message export at all. With the full 8-person roster known from insider
  knowledge, the honest finding is simply: *no true lurkers; 6 active members, 2 rare visitors.*

- **Bot/non-member removal relied on insider knowledge, not an algorithm.** Two bots
  (Cyrus, Maki) were only catchable because the author knew the server — a bot posting dozens of
  conversational messages is statistically indistinguishable from a quiet human. The cleaning is
  best-effort, not provably exhaustive.

- **Small-sample findings are flagged as suggestive.** The peripheral-member analysis rests on
  dozens of interactions, not thousands. Directions are trustworthy where concentration is strong
  (e.g. 27 vs 4); fine rankings within small counts are not.

- **The `wnh` decline after Aug 2025 has a cause not present in the data**, and is described only
  as an observed pattern, not explained.

- **Network layout positions are aesthetic, not meaningful.** With 6 fully-connected nodes, spring
  layout placement is arbitrary; only node size/color (volume) and edge thickness (pair strength)
  carry information.

---

## Tools

Python · pandas · matplotlib · seaborn · networkx · Jupyter