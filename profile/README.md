<p align="center">
  <img src="https://raw.githubusercontent.com/mirror-stack/.github/main/profile/mirror_stack_og.png" alt="Mirror Stack" width="640">
</p>

<h1 align="center">🪞🔎🪪 Mirror Stack</h1>

<p align="center"><b>Preregistration and audit for AI research and evaluation claims.</b></p>

<p align="center">
Seal the hypothesis and the condition that would kill it <i>before</i> the run, then audit
the result against what was sealed. A sealed record is not proof that its content is true.
</p>

---

When an AI agent (or a person) runs an evaluation and reports a result, the usual question is
"was the success criterion chosen before or after seeing the numbers?" Today that is mostly
answered by trust: a checklist, a preregistration form, a promise.

Mirror Stack's core tool, **measure-mirror**, makes that answerable from a file. You seal the
metric, sample size, baseline, pass threshold and a **kill condition** into a hash-chained ledger
before the experiment; afterwards `mm audit` checks the result against the sealed criteria and
runs statistical and gaming probes (small samples, metric swaps, weak baselines, multiple
comparisons, and others). If the result hits the kill condition, the claim is reported as
falsified by its own preregistered criterion.

```bash
pip install git+https://github.com/mirror-stack/measure-mirror@v0.41.2

# before the run: seal the criteria, including what would falsify the claim
mm register my_model --metric acc --min-n 200 --baseline 0.5 --pass 0.60 \
           --new-ledger --kill-threshold 0.55 --kill-direction below

# after the run: audit the result against what was sealed
mm audit my_model --acc 0.72 --n 500    # ✅ OK
mm audit my_model --acc 0.52 --n 500    # 🔴 FAIL: kill condition triggered
```

→ **[measure-mirror](https://github.com/mirror-stack/measure-mirror)** — 28 probes, a
[catalog of sealed measurement-illusion cases](https://github.com/mirror-stack/measure-mirror/blob/main/catalog/README.md),
CLI, Python API and an MCP server. Apache-2.0, stdlib-only core.

## Supporting tools

The other tools cover what surrounds a claim. They are smaller and less validated than
measure-mirror.

| Tool | Records | Question it answers |
|---|---|---|
| 🪪 [**action-mirror**](https://github.com/mirror-stack/action-mirror) | Agent actions | Who recorded doing what? — chain-linked action history + mutual witness between ledgers |
| 🔎 [**provenance-mirror**](https://github.com/mirror-stack/provenance-mirror) | Provenance signals | What origin hints are present? — byte markers are **not** authenticated manifests or verified signatures |
| 👁 [**mirror-witness**](https://github.com/mirror-stack/mirror-witness) | Cross-operator witness board | Who else **witnessed** a ledger head? — GitHub-as-witness, CI-verified, no server |

Five conventions + one `verify-all` command join them:
**[the Mirror Stack →](https://github.com/mirror-stack/measure-mirror/tree/main/stack)**.
All four ship as one MCP server, [mirror-stack-mcp](https://github.com/mirror-stack/mirror-stack-mcp):

```bash
pip install git+https://github.com/mirror-stack/mirror-stack-mcp@v0.3.0
```

### A separate product: yeoul

[**yeoul**](https://github.com/mirror-stack/yeoul) is a file-based harness for running
deliberation → pre-registration → dev loops with integrity gates (prior-art check, two-phase
close, a KILL-defense checklist, a verify-gated dev loop). Since v0.4.0 it is a **standalone**
product: it runs without the mirrors, and linking it to Mirror Stack is an explicit opt-in
(`--with-mirror-stack` in its installer). See its README for setup.

💬 **[Discussions](https://github.com/orgs/mirror-stack/discussions)** — questions, ideas,
and (especially) **independent reproductions**: the one thing the makers cannot do for themselves.

## See it work

**[Browse real sealed records → the Reading Room](https://mirror-stack.github.io/mirror-witness/ledger/)** — a
human-readable viewer over real ledgers, published as a snapshot (most recent arc: 2026-07-09). Each experiment
shows the kill-condition sealed *before* the run, the verdict (pass / kill / retracted / inconclusive), and every
number **recomputed in your browser from the ledger itself** rather than typed in.
Tamper with a sealed value in your browser and watch the hash break. It shows the failures and retractions,
not just the wins.

Or read a single arc end-to-end: **[an agent that retracted its own experiment before spending a single token](https://github.com/mirror-stack/measure-mirror/blob/main/stack/CASE_STUDY_compute_governor.md)**
— preregistration → a power check that vetoed its own design → adversarial self-amendments →
prior-art retraction at zero measurement cost. The chain-sealed ledger is bundled; verify it
yourself.

## Honesty box

Current verification depth is explicit: `LINKAGE_ONLY` checks pointers, not content
hashes; `HASH_RECOMPUTED` checks hashes, not author identity; `LOCAL_SNAPSHOT` is not
an external clock; `HEAD_WITNESS` is not independent reproduction. Provenance hints
return yellow `PROVENANCE-UNVERIFIED`, not `AUTHENTIC-SIGNED`. Historical sealed
records are left intact. See the [current gate contract and migration guide](https://github.com/mirror-stack/mirror-stack-mcp/blob/main/README.md#verification-depth-and-gate-migration-0214).

This does **not** prevent dishonesty — an agent can simply not record, and a local ledger's
timestamps come from a local clock. What the ledger gives is narrower: a preregistration that
was sealed before a result is linked to it can't be edited afterwards without breaking the
chain, and once a ledger head is witnessed or externally anchored, rewriting the history
before it is detectable. So far the witnesses are one agent family run by the makers — not yet an independent
network. Opening them is how that changes.

<p align="center"><sub>Built while honestly killing our own projects · Apache 2.0</sub></p>
