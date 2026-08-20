# LLM Prompt Injection Testing Methodology

A practical, impact-led methodology for assessing prompt-injection risk in LLM-enabled web applications, APIs, retrieval-augmented generation (RAG) systems, multimodal features, and agentic applications with tools or persistent memory.

**Current release:** v2.0  
**Date:** August 2026  
**Author / methodology contributor:** Daniel Jones  
**Status:** Independent public portfolio reconstruction

> **Authorisation boundary:** Use this methodology only against systems for which explicit testing authorisation and scope have been established. Tool execution, outbound requests, poisoning, persistent-memory testing, and code execution should be treated as separately controlled proof techniques where relevant.

## Project background

This public edition is based on prompt-injection testing work developed as a contribution to a broader LLM penetration-testing methodology. It has been independently reconstructed, expanded, and updated for public portfolio use.

The repository does **not** contain the original private methodology, employer-specific procedures, client information, internal systems, credentials, or proprietary engagement material.

The original work focused on turning prompt-injection testing into something a consultant could execute consistently rather than treating jailbreak prompts as isolated demonstrations. The public edition retains that practical approach while strengthening the security interpretation, evidence requirements, impact assessment, and agentic-AI coverage.

## Core assessment principle

A model following an adversarial instruction is **not automatically a reportable application vulnerability**.

The methodology uses an impact-led finding threshold:

```text
Injection reaches model
        ↓
Behaviour materially changes
        ↓
A trust boundary is crossed
        ↓
A protected application effect occurs
        ↓
Reportable security finding
```

A strong finding normally demonstrates an application-level consequence such as protected-data exposure, authorisation bypass, privileged tool misuse, persistent poisoning, manipulation of a trusted decision, unsafe downstream execution, or another externally visible security-relevant state change.

This prevents harmless model-level jailbreak behaviour from being overstated while still allowing serious prompt-injection paths to be evidenced and risk-rated appropriately.

## Test coverage

| ID | Test area | Primary purpose |
|---|---|---|
| **PI-01** | Direct Prompt Injection and Instruction Override | Determine whether attacker-controlled user input can override intended behaviour and reach a protected effect. |
| **PI-02** | Indirect Prompt Injection via External Content | Test whether hostile instructions in fetched or ingested content can influence the model or downstream actions. |
| **PI-03** | RAG and Knowledge Base Poisoning | Assess whether malicious or compromised knowledge content can alter trusted answers, decisions, or actions. |
| **PI-04** | Untrusted Business Content Influence | Determine whether normal application data is incorrectly treated as control-plane instruction and causes a security-relevant outcome. |
| **PI-05** | Tool, Function, and Code Injection | Test whether prompt manipulation can misuse tools, functions, APIs, or code-execution capabilities. |
| **PI-06** | Payload Splitting and Multi-Field Prompt Assembly | Assess whether separately validated fields can recombine into an effective hostile instruction. |
| **PI-07** | Multimodal Prompt Injection | Test hostile instructions delivered through images, PDFs, documents, audio-derived text, or other multimodal content. |
| **PI-08** | Adversarial Suffix and Jailbreak-Style Bypass | Compare baseline and modified prompts to identify reliable control bypass and determine whether protected application impact follows. |
| **PI-09** | Multilingual, Encoded, and Obfuscated Prompt Injection | Test whether language or representation changes bypass controls that operate only on a narrow input form. |
| **PI-10** | Agent Tool Context and Persistent Memory Injection | Test malicious tool output, memory, agent state, peer-agent messages, and other persistent or agentic context for cross-task or cross-session impact. |

## Methodology structure

The full methodology provides:

- engagement assumptions and authorisation boundaries;
- current framework mapping;
- a security interpretation and finding-quality threshold;
- architecture and entry-point discovery;
- baseline testing;
- ten structured prompt-injection test cases;
- practical browser/API/command-line test examples;
- expected secure behaviour and vulnerability criteria;
- evidence requirements;
- impact-led risk-rating guidance;
- detection and logging considerations;
- remediation principles; and
- retest guidance.

Each test case is written so that a consultant can determine **where to test, what to observe, what constitutes meaningful impact, what evidence to preserve, and when not to overstate the result**.

## Framework alignment

The public edition is mapped against current public guidance available in August 2026, including:

- **OWASP GenAI LLM Top 10 2026**, primarily LLM01 Prompt Injection with related mappings where the demonstrated effect overlaps excessive agency, poisoning, hidden context, vector/embedding weaknesses, or improper output handling;
- **OWASP Top 10 for Agentic Applications 2026**, where tools, memory, privileges, agent context, or code execution are involved;
- **MITRE ATLAS**, using current technique names for prompt injection, jailbreak, RAG poisoning, agent context poisoning, and tool invocation/poisoning;
- **NIST AI RMF 1.0** and **NIST AI 600-1 Generative AI Profile** for AI-risk governance and treatment context; and
- **NIST CSF 2.0** as an optional secondary organisational-security mapping.

See [Framework Mapping](reference/framework-mapping.md) for the concise cross-reference.

## Repository contents

```text
LLM-Prompt-Injection-Testing-Methodology/
├── README.md
├── PUBLIC_RELEASE_NOTES.md
├── COPYRIGHT.md
├── docs/
│   └── prompt-injection-testing-methodology.pdf
├── checklists/
│   └── consultant-testing-checklist.pdf
└── reference/
    └── framework-mapping.md
```

## Documents

- [Full Prompt Injection Testing Methodology](docs/prompt-injection-testing-methodology.pdf)
- [Consultant Testing Checklist](checklists/consultant-testing-checklist.pdf)
- [Framework Mapping](reference/framework-mapping.md)
- [Public Release Notes](PUBLIC_RELEASE_NOTES.md)

## Consultant checklist

The quick-reference checklist is designed for use alongside the full methodology. It provides pre-assessment, architecture-discovery, baseline, PI-01 to PI-10, finding-quality, and retest checks so an assessor can record which applicable activities were completed.

The checklist is intentionally not a substitute for judgement. A test should only be marked as a vulnerability when the evidence establishes the relevant trust boundary and application impact.

## Deliberate boundaries

This project is a testing methodology, not an exploit framework or automated scanner. It does not provide target-specific payloads, credentials, client data, autonomous attack tooling, or instructions to exceed an authorised scope.

Examples use placeholders, synthetic data, controlled collectors, and generic endpoints. Where a test could cause persistent state change, outbound communication, tool execution, or code execution, the methodology applies a minimum-proof principle and expects explicit engagement authorisation.

## Limitations

LLM behaviour is stochastic and changes across model, prompt, orchestration, retrieval, tool, and policy revisions. A single successful or failed payload is therefore not sufficient evidence of systemic security posture.

Testing should use baseline/control cases, repeatable variants, downstream application evidence, and architecture context. Retesting should verify the original impact and reasonable variants, not simply confirm that one literal string has been blocked.

## Copyright

**Copyright © 2026 Daniel Jones. All rights reserved.**

This repository is publicly available for portfolio demonstration, professional review and authorised security-assessment reference. No open-source licence is granted for the independently rewritten public-edition materials. This notice does not claim ownership over general prompt-injection concepts, penetration-testing techniques, OWASP, MITRE ATLAS, NIST, third-party standards, or any private/employer methodology.

See [COPYRIGHT.md](COPYRIGHT.md) for the full notice.

## Disclaimer

This repository is provided for authorised security assessment, research, and portfolio demonstration. It does not grant permission to test any system. The assessor remains responsible for operating within the applicable Rules of Engagement, Statement of Work, law, and organisational policy.
