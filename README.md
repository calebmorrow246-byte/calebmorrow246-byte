# Caleb A. Morrow

**Systems engineer building practical AI tooling for IT operations.** About eight years across infrastructure, identity and service management, now focused on putting LLMs to work safely: scoped integrations, measured benchmarks, and automation that people can audit.

Missouri · [LinkedIn](https://www.linkedin.com/in/caleb-morrow-b309b9138/) · caleb.morrow246@gmail.com

---

## Featured work

Each project has its own README explaining **why it exists, why it was built the way it was, and what it improves**. Company, host and account details are scrubbed from all of them.

| Project | What it is |
|---|---|
| [**freshservice-ai-triage**](https://github.com/calebmorrow246-byte/freshservice-ai-triage) | Serverless app that gives every new IT ticket a private AI first-pass triage note. In production; provider-swappable (Claude, ChatGPT, Azure OpenAI); 133 tests. Built least-privilege on purpose: four capabilities, not a full API key. |
| [**kb-standardization-pipeline**](https://github.com/calebmorrow246-byte/kb-standardization-pipeline) | Migrated a 326-article knowledge base onto six standard templates using scripts plus Claude Code as an auditable batch engine, with image-safe placeholders, local review, and backup-first pushes. 307 articles pushed live. |
| [**mcp-servers**](https://github.com/calebmorrow246-byte/mcp-servers) | Twenty MCP servers connecting an AI assistant to ITSM, monitoring, vulnerability, backup, storage, virtualisation, DNS and identity systems. The design question throughout: how much access, and where the safety guarantee lives (by construction, guarded writes, or the credential). |
| [**private-llm-stack**](https://github.com/calebmorrow246-byte/private-llm-stack) | A two-stage on-prem LLM pilot: a deterministic RAG proxy built after the chat UI's built-in RAG failed, a fixed-method CPU vs GPU benchmark, and a local coding-model lab with honest limits. No savings claimed. |

## Design case study

[**Self-hosted ITSM platform design**](itsm-platform-design.md): the architecture, integrations and migration plan I designed to replace a hosted service desk with a self-hosted open-source platform. Evaluated and designed; not deployed.

## What I work with

- **Infrastructure and systems:** Azure, VMware vSphere, Hyper-V, Windows Server, Microsoft 365
- **Identity and access:** Active Directory, Entra ID, Okta, Google Identity, IAM, RBAC, SSO
- **Networking and security:** Cisco, Meraki, Juniper, Palo Alto, Fortinet, SonicWall, segmentation, enterprise Wi-Fi
- **Automation and ITSM:** PowerShell, Node.js, Python, Freshservice, workflow automation
- **AI and integration:** Claude API, MCP server development, RAG patterns, LLM benchmarking, Claude Code
- **Certifications:** CompTIA A+, CompTIA Network+, Certified Fiber Optic Technician (CFOT)

## How I work

I'd rather write the case down than pitch it: measure first, label the limits of every number, and put guardrails where they can't be bypassed. The READMEs above show that in practice.
