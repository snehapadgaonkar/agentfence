<a id="readme-top"></a>

<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/snehapadgaonkar/agentfence">
    <img src="agentfence_architecture.png" alt="AgentFence Architecture" width="320" height="220">
  </a>

<h3 align="center">AgentFence</h3>

  <p align="center">
    A controlled Colab experiment on AI agent authorization, tool misuse, risk-based autonomy, and accountability.
    <br />
    <a href="https://github.com/snehapadgaonkar/agentfence"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="AgentFence_Experiment.ipynb">Open Notebook</a>
    &middot;
    <a href="https://github.com/snehapadgaonkar/agentfence/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/snehapadgaonkar/agentfence/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

[![AgentFence Architecture][product-screenshot]](AgentFence_Experiment.ipynb)

**AgentFence** is a publication-quality, fully self-contained Google Colab experiment that demonstrates one architectural principle:

> *An LLM can propose an action, but the LLM should not be the authority that decides whether the action is permitted.*

The experiment uses a simulated customer-support agent with in-memory data, structured audit trails, a policy engine, schema validation, least-privilege tool design, risk-based autonomy levels, reversibility comparisons, autonomy budgets, and accountability reconstruction. It is designed to accompany a technical article on AI agent authorization and risk-based autonomy.

This is a **controlled simulation**, not a claim of full OWASP or NIST framework implementation. Key connections are made to selected OWASP Agentic Security 2026 principles (ASI01, ASI02, ASI03, excessive agency, least-privilege, downstream authorization, tool validation, human approval) and NIST AI RMF 1.0 guidance (human-AI roles, differentiated configurations, oversight, monitoring, accountability, safe failure).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Built With

* [Python 3](https://www.python.org/)
* [Google Colab](https://colab.research.google.com/)
* [pandas](https://pandas.pydata.org/)
* [matplotlib](https://matplotlib.org/)
* [OWASP Gen AI Security Project — Agentic Applications 2026](https://genai.owasp.org/)
* [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

The experiment runs top-to-bottom in Google Colab with no external APIs required for the core security demonstrations. An optional OpenAI extension (Section 18 of the notebook) can be enabled only if you have an API key configured.

### Prerequisites

* A Google account with access to [Google Colab](https://colab.research.google.com/)
* Python 3 environment (only needed for local execution)

### Installation

1. Clone the repo (optional — you can open the notebook directly)
   ```sh
   git clone https://github.com/snehapadgaonkar/agentfence.git
   ```
2. Open `AgentFence_Experiment.ipynb` in Colab, or run locally:
   ```sh
   pip install pandas matplotlib
   jupyter notebook AgentFence_Experiment.ipynb
   ```
3. Run all cells (`Runtime → Run all`).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

### Run the full experiment

Open `AgentFence_Experiment.ipynb` and run all cells sequentially. Each experiment (A–J) resets or isolates state so results are reproducible.

### Inspect the audit trail

After any experiment, inspect structured audit events with:
```python
display_audit("Experiment label")
```

### Optional LLM extension

In Section 18, set `USE_REAL_LLM = True` and configure `OPENAI_API_KEY` to replace simulated proposals with real model output. The architecture (proposal → schema → policy → execution) remains unchanged.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [x] Core experiments A–J with assertions
- [x] Policy engine with structured authorization
- [x] Risk-based autonomy framework (LOW / MEDIUM / HIGH / CRITICAL)
- [x] Visualization of architectural separation
- [x] Optional real-LLM extension (Section 18)
- [ ] Additional tool schemas (e.g., simulated payments / credential rotation as simulated actions)
- [ ] Expanded accountability case studies with multi-agent configurations

See the [open issues](https://github.com/snehapadgaonkar/agentfence/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Top contributors:

<a href="https://github.com/snehapadgaonkar/agentfence/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=snehapadgaonkar/agentfence" alt="contrib.rocks image" />
</a>



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Sneha Padgaonkar — [@snehapadgaonkar](https://github.com/snehapadgaonkar) — agentfence experiment

Project Link: [https://github.com/snehapadgaonkar/agentfence](https://github.com/snehapadgaonkar/agentfence)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [OWASP Gen AI Security Project — Top 10 for Agentic Applications 2026](https://genai.owasp.org/)
* [OWASP LLM06: Excessive Agency / Excessive Permissions](https://genai.owasp.org/llmrisk2023-24/llm08-excessive-agency/)
* [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework)
* [NIST AI RMF Appendix C: AI Risk Management and Human-AI Interaction](https://airc.nist.gov/airmf-resources/airmf/appendices/app-c-ai-risk-management-and-human-ai-interaction/)
* [OpenAI Platform — Structured Tool Calling](https://platform.openai.com/docs/api-reference/chat/object)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/snehapadgaonkar/agentfence.svg?style=for-the-badge
[contributors-url]: https://github.com/snehapadgaonkar/agentfence/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/snehapadgaonkar/agentfence.svg?style=for-the-badge
[forks-url]: https://github.com/snehapadgaonkar/agentfence/network/members
[stars-shield]: https://img.shields.io/github/stars/snehapadgaonkar/agentfence.svg?style=for-the-badge
[stars-url]: https://github.com/snehapadgaonkar/agentfence/stargazers
[issues-shield]: https://img.shields.io/github/issues/snehapadgaonkar/agentfence.svg?style=for-the-badge
[issues-url]: https://github.com/snehapadgaonkar/agentfence/issues
[license-shield]: https://img.shields.io/github/license/snehapadgaonkar/agentfence.svg?style=for-the-badge
[license-url]: https://github.com/snehapadgaonkar/agentfence/blob/main/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/snehapadgaonkar
[product-screenshot]: agentfence_architecture.png
