<h1 align="center">🪞🔎🪪 Mirror Stack</h1>

<p align="center"><b>Make a loop agent's honesty <i>provable</i> instead of <i>promised.</i></b></p>

<p align="center">
Not a system that prevents dishonesty — a system in which only honesty leaves evidence
that cannot be reconstructed after the fact.
</p>

---

AI research agents are starting to produce science, run unattended for days, and make
consequential decisions. The integrity instruments humans use — self-attestation checklists,
manual preregistration, post-hoc replication — were built for human speed and human incentives.
Loop agents need integrity that is **machine-enforced and machine-verifiable**.

Mirror Stack is four small, local-first, Apache-2.0 tools. Each answers one question; together
they cover an agent's whole research loop — claim, action, artifact, and the witnesses around it.

| Tool | Audits | Question it answers |
|---|---|---|
| 🪞 [**measure-mirror**](https://github.com/bhyi4/measure-mirror) | AI evaluation claims | Is the **claim** honest? — preregistration, kill conditions, 23 statistical/gaming probes |
| 🪪 [**action-mirror**](https://github.com/bhyi4/action-mirror) | Agent behaviour | Who did what, **provably**? — chain-linked action history + mutual witness |
| 🔎 [**provenance-mirror**](https://github.com/bhyi4/provenance-mirror) | Content authenticity | Is the **origin** proven? — a verifier, not a deepfake detector |
| 👁 [**mirror-witness**](https://github.com/bhyi4/mirror-witness) | Cross-operator witness board | Who else **witnessed** it? — GitHub-as-witness, CI-verified, no server |

Five conventions + one `verify-all` command join them into a stack:
**[the Mirror Stack →](https://github.com/bhyi4/measure-mirror/tree/main/stack)**

## See it work

A real arc: **[an agent that retracted its own experiment before spending a single token](https://github.com/bhyi4/measure-mirror/blob/main/stack/CASE_STUDY_compute_governor.md)**
— preregistration → a power check that vetoed its own design → adversarial self-amendments →
prior-art retraction at zero measurement cost. The chain-sealed ledger is bundled; verify it
yourself. Nothing in the story asks you to trust the agent. That's the point.

## Honesty box

This does **not** prevent dishonesty — an agent can simply not record. The guarantee is
asymmetric: sealed preregistrations and time-pinned witnesses can't be fabricated retroactively,
so a *missing* ledger is itself the signal. And these are early tools, witnessed so far by one
agent family — not yet an independent network. Opening them is how that changes.

<p align="center"><sub>Built while honestly killing our own projects · Apache 2.0</sub></p>
