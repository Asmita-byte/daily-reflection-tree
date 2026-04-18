# Write-Up: The Daily Reflection Tree

**Candidate:** Job Seeker · DT Fellowship Application
**Word count:** ~800 words

---

## Why These Questions

The hardest design problem wasn't writing questions. It was writing questions that feel like a conversation rather than a survey — questions that a tired person at 7pm might actually pause on.

**Axis 1 — Locus of Control** rests on Rotter's (1954) insight that people differ systematically in whether they locate causality inside themselves or in their circumstances. The tricky thing: both stances can be cognitively accurate in the same situation. A delayed train is genuinely not your fault. But *how you responded to it* almost always was. My opening question ("which one word fits today best?") doesn't ask about causality at all — it asks for a felt sense. The emotional temperature of the word (Productive vs Draining) predicts which follow-up will land, which is why the D1 decision node routes on answer text rather than signals. The second and third questions then probe beneath that initial frame, asking where attention went and whether choice was even visible. I deliberately included a "maybe" option on A1_Q3_EXT ("maybe — but the situation really did constrain my options") because forcing false clarity would make the question feel dishonest.

**Axis 2 — Contribution vs Entitlement** draws on Campbell et al.'s (2004) work on psychological entitlement — the durable belief that one deserves more than others, independent of contribution — and Organ's (1988) concept of Organizational Citizenship Behavior. The key design challenge here: entitlement is largely invisible to the person holding it. You don't feel entitled; you feel that the situation is genuinely unfair. So the questions don't name entitlement — they ask about energy direction and what "fair" would look like. Option D on A2_Q2_ENTITLE ("Honestly — maybe just finding something worth giving regardless") is the genuine out: even someone who started in the entitlement branch can recognize contribution as an alternative. Routing on accumulated signals (not just answer text) means this recognition gets counted.

**Axis 3 — Radius of Concern** follows Maslow's (1969) later work on self-transcendence — the often-neglected peak above self-actualization — and Batson's (2011) framework for perspective-taking as a cognitive act. The A3_OPEN question is the most behaviorally honest in the tree: it doesn't ask what you *should* think about, but whose experience you actually find yourself returning to. Someone who answers "Mine" isn't wrong — they may have had a genuinely isolating day. The follow-up question A3_Q2_SELF nudges gently: *did anyone break through?* This follows the structure Batson describes: perspective-taking doesn't happen spontaneously, but a small prompt can trigger it. A3_R_SELF doesn't shame self-focus; it ends with "just notice whether it lands" — a question to carry out, not answer in the session.

---

## How the Branching Was Designed

The primary routing mechanism is signal accumulation per axis. Each question option records either the "growth" pole (internal, contribution, altro) or the "default" pole (external, entitlement, self). Decision nodes compare these tallies to route the next question and, ultimately, the reflection.

The key trade-off I made: **depth over breadth**. Instead of covering more ground with shallower questions, each axis has three question nodes (opening + Q2 + Q3), with the Q3 varying by path. This means someone on the external-locus path gets asked "was anything still yours to decide?" — a question that would feel redundant or preachy on the internal path. The tree serves different content to different people, which is what makes it feel like a conversation rather than a uniform survey.

The bridge nodes (BRIDGE_1_2, BRIDGE_2_3) carry the conceptual progression: from *how you moved* (Axis 1) → to *what you brought* (Axis 2) → to *who you included* (Axis 3). Each axis's insight sets up the next: recognizing agency (Axis 1) prepares you to examine what that agency was *oriented toward* (Axis 2), which opens the question of who was in range of your orientation (Axis 3).

---

## What I'd Improve With More Time

1. **Mixed-path branches.** Currently the tree has 3 reflections per axis (dominant-A, dominant-B, tied). With more nodes, I'd add Q4 for mixed paths — a genuine third question rather than a tie-breaker.

2. **Cross-axis interpolation.** The summary currently references each axis independently. With more time I'd write summary templates that exploit the *combination* — e.g., someone who was external (Axis 1) but contribution (Axis 2) gets different closing language than someone who was external + entitlement.

3. **Session history.** A real deployment would track patterns across sessions ("You've leaned external three days in a row — what changed on the days you didn't?"). The signal schema is already designed to support this; it just needs a persistence layer.

4. **Question A3_Q2_ALTRO.** Option D ("I'm not sure I actually helped — I'm still processing") records a self signal, but in practice this is often *more* altrocentric than the other options — it's evidence of care about impact. I'd redesign this option or route it separately.

---

## Sources Consulted

- Rotter, J.B. (1954). *Social Learning and Clinical Psychology.* Prentice-Hall.
- Dweck, C.S. (2006). *Mindset: The New Psychology of Success.* Random House.
- Campbell, W.K. et al. (2004). Psychological Entitlement: Interpersonal Consequences and Validation of a Self-Report Measure. *Journal of Personality Assessment.*
- Organ, D.W. (1988). *Organizational Citizenship Behavior: The Good Soldier Syndrome.* Lexington Books.
- Maslow, A.H. (1969). The farther reaches of human nature. *Journal of Transpersonal Psychology.*
- Batson, C.D. (2011). *Altruism in Humans.* Oxford University Press.
