# Framework Mapping

**Methodology version:** 2.0  
**Reference date:** August 2026

This cross-reference is provided to help consultants communicate coverage. It is not a substitute for a target-specific threat model, client risk methodology, or authoritative interpretation of any framework.

## Test-case cross-reference

| Test | OWASP GenAI LLM Top 10 2026 | OWASP Agentic Top 10 2026 | MITRE ATLAS examples | Notes |
|---|---|---|---|---|
| **PI-01 Direct Prompt Injection** | LLM01 Prompt Injection; LLM08 Hidden Context Exposure where protected context is exposed; LLM03 Excessive Agency where actions are reached | ASI01 Agent Goal Hijack; ASI02 Tool Misuse & Exploitation where applicable | LLM Prompt Injection; LLM Jailbreak | Do not treat prompt wording alone as a secret or access-control boundary without impact. |
| **PI-02 Indirect Injection** | LLM01 Prompt Injection; LLM03 Excessive Agency when hostile external content reaches tools/actions | ASI01 Agent Goal Hijack; ASI02 Tool Misuse & Exploitation | Prompt Infiltration via Public-Facing Application | Focus on provenance of external content and downstream effect. |
| **PI-03 RAG / Knowledge Poisoning** | LLM01 Prompt Injection; LLM05 Data and Model Poisoning; LLM09 Vector and Embedding Weaknesses | ASI06 Memory & Context Poisoning where poisoned state persists | RAG Poisoning; False RAG Entry Injection | Separate retrieval-quality problems from attacker-controlled poisoning. |
| **PI-04 Untrusted Business Content Influence** | LLM01 Prompt Injection where content becomes control-plane instruction; LLM07 Misinformation where incorrect trusted output is the main consequence | Context-dependent | Context-dependent | Requires attacker control and meaningful trust-boundary/application consequence. |
| **PI-05 Tool / Function / Code Injection** | LLM01 Prompt Injection; LLM03 Excessive Agency; LLM10 Improper Output Handling | ASI02 Tool Misuse & Exploitation; ASI03 Identity & Privilege Abuse; ASI05 Unexpected Code Execution | AI Agent Tool Invocation | Assess server-side authorisation, tool identity, argument validation, approvals, and output handling. |
| **PI-06 Payload Splitting** | LLM01 Prompt Injection | Context-dependent | LLM Prompt Injection | Validate the final assembled prompt/context, not only individual fields. |
| **PI-07 Multimodal Injection** | LLM01 Prompt Injection | Context-dependent | LLM Prompt Injection | Treat extracted/OCR/transcribed content as untrusted input. |
| **PI-08 Suffix / Jailbreak Bypass** | LLM01 Prompt Injection | Context-dependent | LLM Jailbreak | A jailbreak becomes a security finding only when protected application impact is demonstrated. |
| **PI-09 Multilingual / Encoded / Obfuscated Injection** | LLM01 Prompt Injection | Context-dependent | LLM Prompt Injection / LLM Jailbreak as appropriate | Test policy consistency across representations and languages. |
| **PI-10 Agent Context / Persistent Memory Injection** | LLM01 Prompt Injection; LLM03 Excessive Agency | ASI01 Agent Goal Hijack; ASI02 Tool Misuse & Exploitation; ASI04 Agentic Supply Chain Vulnerabilities where tool/context provenance is compromised; ASI06 Memory & Context Poisoning | AI Agent Context Poisoning; AI Agent Tool Invocation; AI Agent Tool Poisoning | Test persistence, cross-session/task influence, source trust, tool metadata, and cleanup. |

## NIST usage

### NIST AI RMF 1.0

Use the AI Risk Management Framework as governance and risk-treatment context rather than as a one-to-one attack taxonomy. Prompt-injection assessment can support activities across **GOVERN, MAP, MEASURE, and MANAGE**, especially where the organisation needs to understand model context, privileges, monitoring, human oversight, and treatment decisions.

### NIST AI 600-1 — Generative AI Profile

Use the Generative AI Profile as the companion GenAI-specific risk resource when discussing prompt-injection controls, monitoring, provenance, human oversight, third-party dependencies, and risk management for generative AI deployments.

### NIST CSF 2.0

Use CSF 2.0 only when an engagement or report benefits from an organisational cybersecurity mapping across Govern, Identify, Protect, Detect, Respond, and Recover. It is secondary to AI-specific risk guidance for this methodology.

## Reference sources

- OWASP GenAI Security Project — LLM Top 10 2026: https://genai.owasp.org/
- OWASP Top 10 for Agentic Applications 2026: https://genai.owasp.org/agentic-applications/
- MITRE ATLAS: https://atlas.mitre.org/
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework
- NIST AI 600-1 Generative AI Profile: https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence
- NIST Cybersecurity Framework 2.0: https://www.nist.gov/cyberframework

Framework names and taxonomies evolve. Confirm the current authoritative mapping when producing a client report.
