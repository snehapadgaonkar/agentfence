<a id="readme-top"></a>

# 🔒 AgentFence

> A publication-quality Colab experiment on AI agent authorization, tool misuse, risk-based autonomy, and accountability.

[Getting Started](#getting-started) ·
[Results](#results) ·
[Built With](#built-with) ·
[Roadmap](#roadmap) ·
[License](#license)

* * *

AgentFence demonstrates one architectural principle:

**An LLM can propose an action, but the LLM should not be the authority that decides whether the action is permitted.**

The experiment uses a simulated customer-support agent (in-memory only — no real APIs, no credentials) with structured audit trails, a policy engine, schema validation, least-privilege tool lists, risk-based autonomy levels, reversibility comparisons, autonomy budgets, and accountability reconstruction. It is designed to accompany a technical article on agentic security.

This is a **controlled simulation**, not a claim of full OWASP or NIST framework implementation.

* * *

## Getting Started


Run the full experiment top-to-bottom in Google Colab with no external APIs required.

### Prerequisites


- Google account (for Colab)
- Python 3 (only for local execution)
- `pandas` and `matplotlib` (installed by default in Colab)

### Installation


```sh
git clone https://github.com/snehapadgaonkar/agentfence.git
cd agentfence
```

### Run


**Google Colab (recommended — zero setup):**

```text
Open AgentFence_Experiment.ipynb in Colab → Runtime → Run all
```

Or open directly: [AgentFence_Experiment.ipynb](AgentFence_Experiment.ipynb)

**Local:**

```sh
pip install pandas matplotlib
jupyter notebook AgentFence_Experiment.ipynb
```

**Optional LLM extension (Section 18):**

```python
USE_REAL_LLM = True
# Configure OPENAI_API_KEY in environment if needed
```

The architecture stays identical: LLM → structured proposal → schema validation → policy engine → approval check → tool proxy → simulated DB.

### Test


Every experiment includes assertions that verify expected security outcomes:

```python
assert customers["48291"]["status"] == "deleted"   # Experiment A
assert res == "DENY"                                # Experiment C / D / E
assert res_b["status"] == "CANNOT_PROPOSE"          # Experiment F
assert results_budget["stopped_reason"] == "Budget exceeded"  # Experiment I
```

Run all cells; assertions will fail loudly if an experiment deviates from its intended result.

* * *

## Results


The notebook runs 10 experiments (A–J) that measure how the **same model proposal** produces different outcomes depending solely on authorization architecture.

| Experiment | What is demonstrated | Key result / assertion |
| --- | --- | --- |
| **A — Unrestricted** | Direct tool access is vulnerable | `delete_customer` executes; DB mutated; audit shows no policy layer |
| **B — Schema ≠ auth** | Well-formed JSON can still be unauthorized | Valid schema passes; action still requires policy approval |
| **C — Policy engine** | Same proposal, different authorization | `approval=false` → DENY; `approval=true` (manager) → ALLOW; model unchanged |
| **D — Prompt vs auth** | Prompt instruction is not enforceable | System says "never delete"; architecture lacks boundary → executes; with policy → blocked |
| **E — Prompt injection** | Untrusted content redirects proposal | Malicious ticket → proposal `delete_customer`; policy DENY; customer remains active |
| **F — Least privilege** | Capability unavailable vs told not to | Agent A has destructive tools; Agent B does not; proposal impossible |
| **G — Risk-based autonomy** | Four-level risk model | LOW → automatic; MEDIUM → policy + log; HIGH → human approval; CRITICAL → separate auth |
| **H — Reversibility** | Tool design changes mistake cost | `delete_customer` irreversible; `disable_customer` recoverable; `draft_email` safe |
| **I — Autonomy budget** | Runtime limits prevent loops | Budget agent stops when iterations / calls / retries exceed `max_iter` / `max_calls` / `max_retries` |
| **J — Accountability** | Final state is insufficient | Authorized deletion vs injection-blocked produce different audit contexts |

**Main architectural takeaway (visualized in `agentfence_architecture.png`):**

```
Same model proposal: delete_customer(48291)
        ↓
  No policy layer  →  EXECUTES
  Policy layer     →  DENIED
  Least privilege  →  TOOL UNAVAILABLE
```

* * *

## Central principle

> **An LLM can propose an action, but the LLM should not be the authority that decides whether the action is permitted.**

The experiment separates five layers explicitly in code:

1. **Agent / LLM** — generates a structured proposal (JSON tool + arguments)
2. **Schema validation** — answers "Is this well-formed?"
3. **Policy engine** — answers "Is this allowed?" using structured security attributes (user role, agent identity, resource, environment, risk, approval); does **not** inspect model reasoning
4. **Tool proxy / execution boundary** — executes only after authorization
5. **Simulated external system** — in-memory DB + structured audit log

This is the heart of the experiment: the model's output is treated as a **proposal**, never a command.

* * *

## Built With


- [Python 3](https://www.python.org/)
- [Google Colab](https://colab.research.google.com/)
- [pandas](https://pandas.pydata.org/)
- [matplotlib](https://matplotlib.org/)
- [OWASP Gen AI Security Project — Agentic Applications 2026](https://genai.owasp.org/)
- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework)
- [OpenAI Structured Tool Calling Docs](https://platform.openai.com/docs/api-reference/chat/object) (optional extension)

* * *

## Roadmap


### v1.0.0 — Experiment complete


- [x] Simulated customer DB and structured audit log
- [x] Schema validation layer
- [x] Policy engine (`authorize`) with structured decision attributes
- [x] Experiments A–J with assertions and before/after state
- [x] Risk-based autonomy framework (LOW / MEDIUM / HIGH / CRITICAL)
- [x] Reversibility comparison (`delete_customer` vs `disable_customer`; `send_email` vs `draft_email`)
- [x] Autonomy budget (`max_iter`, `max_tool_calls`, `max_retries`)
- [x] Accountability / audit trail comparison (authorized vs injection-blocked)
- [x] Visualization of architectural separation (`agentfence_architecture.png`)
- [x] Optional real-LLM extension (Section 18) — architecture preserved
- [x] Publication-quality documentation (this README + notebook)

### v1.1.0 — Planned


- [ ] Expanded simulated tool schemas (simulated payments, simulated credential rotation as simulated actions)
- [ ] Multi-agent configuration experiments (differentiated permissions across agents)
- [ ] Additional accountability case studies with reconstructed incident timelines
- [ ] Direct Colab badge / open-in-Colab link embedded in README

> **Note**
> Contributions toward v1.1.0 items are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) if it exists, or open an [issue](https://github.com/snehapadgaonkar/agentfence/issues).

* * *

## References (with brief descriptions)


| Source | Why it is cited |
| --- | --- |
| [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/) | Primary security framework — ASI01 (Agent Goal Hijack), ASI02 (Tool Misuse), ASI03 (Identity/Privilege Abuse), excessive agency, least-privilege, downstream authorization, tool validation, human approval |
| [OWASP LLM06 / Excessive Agency](https://genai.owasp.org/llmrisk2023-24/llm08-excessive-agency/) | Recommends restricting tool permissions, enforcing authorization downstream, not relying on LLM reasoning for permission decisions |
| [OWASP Agentic Security Initiative](https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/) | Benchmark and guidance identifying external content and tool misuse as agentic risks |
| [NIST AI RMF 1.0](https://www.nist.gov/itl/ai-risk-management-framework) | Governance reference — human roles, differentiated AI configurations, oversight, accountability, safe failure |
| [NIST AI RMF Appendix C](https://airc.nist.gov/airmf-resources/airmf/appendices/app-c-ai-risk-management-and-human-ai-interaction/) | Human-AI interaction, defining roles and responsibilities |
| [NIST AI RMF Measure / Govern](https://airc.nist.gov/airmf-resources/playbook/measure/) | Monitoring, documentation, accountability mechanisms |
| [OpenAI Structured Tool Calling](https://platform.openai.com/docs/api-reference/chat/object) | Distinction between structured output / schema adherence and actual execution / authorization layers |

This experiment is **inspired by** these frameworks. It does not claim to implement them fully.

* * *

## Contributing


If you have a suggestion, please open an [issue](https://github.com/snehapadgaonkar/agentfence/issues) or create a pull request from the `arena/1f066074-agentfence` branch.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/Name`)
3. Commit your Changes (`git commit -m 'Add feature'`)
4. Push to the Branch (`git push origin feature/Name`)
5. Open a Pull Request

* * *

## License


Distributed under the MIT License. See [LICENSE](LICENSE) for more information.

* * *

## Contact

Sneha Padgaonkar — [@snehapadgaonkar](https://github.com/snehapadgaonkar)

Project Link: [https://github.com/snehapadgaonkar/agentfence](https://github.com/snehapadgaonkar/agentfence)
Branch: `arena/1f066074-agentfence`

<p align="right">(<a href="#readme-top">back to top</a>)</p>
