# Contributing

> Contributions to AgentFence are welcome. This is a controlled experiment — keep changes reproducible and aligned with the security demonstration purpose.

* * *

## How to contribute

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/Name`)
3. Commit your changes (`git commit -m 'Add feature'`)
4. Push to the branch (`git push origin feature/Name`)
5. Open a Pull Request against `arena/1f066074-agentfence`

* * *

## What to contribute

- Additional simulated tool schemas (simulated payments, simulated credential rotation)
- Multi-agent configuration comparisons (differentiated permissions)
- Expanded audit-trail case studies with reconstructed timelines
- Documentation clarifications or translations
- Bug fixes to assertions or policy logic

* * *

## Code standards

- All experiment code must include assertions verified by `assert`
- Do not connect to real production systems, real APIs, or real credentials
- Keep the simulated environment in-memory only
- If adding a real LLM extension, preserve the architecture: proposal → schema → policy → approval → proxy → DB
- The LLM must never be given the policy engine's authority

* * *

## Questions?

Open an [issue](https://github.com/snehapadgaonkar/agentfence/issues) or reach out via the project link.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
