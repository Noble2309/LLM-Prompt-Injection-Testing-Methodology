# Public Release Notes — v2.0

This repository is an independent public portfolio reconstruction of prompt-injection methodology work originally developed as a contribution to a broader LLM penetration-testing methodology.

The original private methodology is **not** included in this repository. This edition contains no employer-specific procedures, client information, internal systems, credentials, engagement records, or proprietary operational material.

## Changes made for the public edition

### 1. Impact-led finding threshold

The original material used model behaviour as a significant part of vulnerability determination. The public edition makes the application-security boundary explicit: a successful jailbreak or instruction override is not automatically a reportable vulnerability.

A finding should establish the attacker-controlled source, behaviour change, crossed trust boundary, protected effect, preconditions, and reproducible evidence.

### 2. Risk guidance revised

Severity is now tied to demonstrated application impact rather than the novelty or apparent success of the prompt itself. Examples distinguish protected-data exposure, authorisation bypass, privileged tool misuse, persistent poisoning, decision manipulation, code execution, constrained behavioural manipulation, and non-security model-quality observations.

### 3. PI-04 renamed and reframed

`Unintentional Prompt Injection (Business Text Influence)` was renamed **PI-04 — Untrusted Business Content Influence**.

The test still examines whether CVs, tickets, product data, complaints, descriptions, or other ordinary business content can influence model behaviour, but the public edition avoids treating every unexpected model response as prompt injection. A security finding requires an attacker-controllable path and a meaningful trust-boundary or protected-effect consequence.

### 4. Current standards mapping

The standards section was updated for public guidance available in August 2026. The primary mappings now include OWASP GenAI LLM Top 10 2026, OWASP Top 10 for Agentic Applications 2026, MITRE ATLAS, NIST AI RMF 1.0, and the NIST Generative AI Profile (NIST AI 600-1). NIST CSF 2.0 remains an optional secondary organisational mapping.

### 5. PI-10 added for agentic systems

A new test case, **PI-10 — Agent Tool Context and Persistent Memory Injection**, covers hostile content originating from or persisting through:

- tool and API responses;
- persistent user or agent memory;
- previous task state;
- peer-agent messages;
- tool/plugin/MCP descriptions and metadata;
- repositories, issues, tickets, documents, or configuration consumed by an agent; and
- context that survives into later sessions or tasks.

### 6. Safer proof boundaries

The methodology now explicitly prefers staging/non-production environments, synthetic data, controlled collectors, reversible actions, and minimum proof. Tool execution, outbound communication, poisoning, persistent memory changes, and code execution should be separately authorised where applicable.

### 7. Evidence and retest strengthened

Evidence guidance now requires the baseline/control case, adversarial input, model response, trust boundary, downstream application effect, relevant logs, user/role context, and cleanup state where applicable.

Retesting checks the original impact plus reasonable semantic and representation variants so remediation is not declared successful merely because a single literal payload has been blocked.

## Elements retained from the source work

The public edition preserves the practical consultant-oriented structure of the source material: architecture discovery, baseline testing, direct and indirect injection, RAG poisoning, business-content influence, tool/code misuse, payload splitting, multimodal delivery, jailbreak/suffix testing, multilingual/obfuscated testing, evidence capture, logging, remediation, and command/checklist examples.

The content has been independently rewritten and expanded for this public release.
