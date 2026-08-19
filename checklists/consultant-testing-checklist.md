# Consultant Prompt Injection Testing Checklist

**Version:** 2.0  
Use this checklist alongside the full methodology. Only perform tests authorised by the engagement scope and rules of engagement.

## 1. Scope and preparation

- [ ] LLM-enabled functionality confirmed in scope
- [ ] Web, API, upload, RAG, tool and agent surfaces identified
- [ ] Test environment and permitted production actions confirmed
- [ ] Test accounts and role boundaries documented
- [ ] Rules of engagement reviewed for tool use, code execution and outbound callbacks
- [ ] Controlled callback/test collector prepared where required
- [ ] Destructive actions and real data exfiltration explicitly excluded unless separately authorised
- [ ] Relevant application, LLM, retrieval and tool logs available where possible
- [ ] Model, prompt/orchestration and application versions recorded where available

## 2. Architecture and trust-boundary discovery

- [ ] User-controlled text inputs mapped
- [ ] File/document/image inputs mapped
- [ ] URL or external-content ingestion mapped
- [ ] RAG/vector/knowledge sources mapped
- [ ] Connected tools and functions identified
- [ ] Tool privilege level and authorisation owner identified
- [ ] Agent memory/state sources identified
- [ ] Persistent vs session-only context identified
- [ ] Cross-user / cross-tenant boundaries identified
- [ ] Server-side approval and policy checks identified
- [ ] Outbound network capabilities identified

## 3. Baseline behaviour

- [ ] Neutral capability prompts completed
- [ ] Normal tool actions tested
- [ ] Normal RAG/retrieval behaviour tested
- [ ] Expected refusals or approval gates recorded
- [ ] Baseline HTTP requests/responses captured
- [ ] Baseline tool/retrieval logs captured where available

---

## PI-01 — Direct Prompt Injection

- [ ] Direct override attempt through UI
- [ ] Direct override attempt through API where present
- [ ] Role/authority assertion attempted
- [ ] Protected prompt/configuration disclosure checked
- [ ] Restricted data access checked
- [ ] Privileged tool invocation checked
- [ ] UI/API enforcement compared
- [ ] Underlying action independently validated rather than trusting model claims
- [ ] Evidence captured
- [ ] Security impact established before raising a finding

## PI-02 — Indirect Prompt Injection

- [ ] Controlled external page/content prepared
- [ ] Visible injected instruction tested
- [ ] HTML comment / metadata / alt-text placement tested where ingested
- [ ] Target ingestion verified
- [ ] Model quoting distinguished from model following
- [ ] Controlled outbound marker tested where authorised
- [ ] Retrieval/network/tool logs reviewed
- [ ] Evidence captured
- [ ] Trust-boundary impact established

## PI-03 — RAG Poisoning

- [ ] Baseline knowledge-base response recorded
- [ ] Controlled poisoned document added
- [ ] Document indexing/retrieval confirmed
- [ ] Before/after responses compared
- [ ] Retrieval trace reviewed
- [ ] Policy/business decision influence checked
- [ ] Tool/data-access influence checked where relevant
- [ ] Source provenance/trust controls reviewed
- [ ] Evidence captured
- [ ] Required document-write privileges included in impact analysis

## PI-04 — Untrusted Business Content Influence

- [ ] Representative business records selected
- [ ] Baseline decisions recorded
- [ ] Instruction-like wording introduced in controlled variants
- [ ] Contradictory/edge-case content tested
- [ ] Decision/explanation differences compared
- [ ] Expected model judgement separated from control-flow manipulation
- [ ] Security/regulatory/material integrity impact assessed
- [ ] Evidence captured

## PI-05 — Tool and Code Injection

- [ ] Available tools/functions inventoried
- [ ] Normal tool call baseline captured
- [ ] User-role permissions mapped to tools
- [ ] Restricted tool action requested
- [ ] Tool parameter validation tested safely
- [ ] High-risk action approval gates checked
- [ ] Harmless code-execution proof used where code execution is in scope
- [ ] Server-side authorisation verified
- [ ] Tool invocation logs captured
- [ ] Model claims cross-checked against real application state

## PI-06 — Payload Splitting

- [ ] All fields contributing to model context identified
- [ ] Partial payloads tested separately
- [ ] Payload fragments distributed across fields/messages
- [ ] Combined request submitted
- [ ] Final assembled context inspected where permitted
- [ ] Behaviour compared with single-fragment controls
- [ ] Filter/policy bypass assessed
- [ ] Evidence captured

## PI-07 — Multimodal Prompt Injection

- [ ] Controlled image/document created
- [ ] Visible embedded instruction tested
- [ ] Upload/analysis workflow exercised
- [ ] Extracted/OCR text inspected where available
- [ ] Description/quotation distinguished from instruction following
- [ ] Tool/data effects checked
- [ ] Upload and tool logs reviewed
- [ ] Evidence captured

## PI-08 — Adversarial Suffix and Jailbreak-Style Attacks

- [ ] Restricted baseline request selected
- [ ] Baseline result recorded
- [ ] Generic suffix/override variant tested
- [ ] Role-play/reframing variant tested where appropriate
- [ ] Multiple attempts used to account for model variance
- [ ] Content differences separated from security-control bypass
- [ ] Protected-data/tool/action impact checked
- [ ] Evidence captured

## PI-09 — Multilingual and Obfuscated Prompt Injection

- [ ] Primary-language baseline recorded
- [ ] Accurate translated equivalent tested
- [ ] Mixed-language request tested
- [ ] Simple human-readable obfuscation tested where relevant
- [ ] Security controls compared across representations
- [ ] Meaningful bypass distinguished from wording variation
- [ ] Original and translated prompts retained in evidence
- [ ] Evidence captured

## PI-10 — Agent Tool Context and Persistent Memory Injection

- [ ] Agent tool outputs identified as context sources
- [ ] Persistent memory/state stores identified
- [ ] Previous-task context behaviour confirmed
- [ ] Controlled instruction marker inserted into an authorised low-trust source
- [ ] Subsequent retrieval of the marker confirmed
- [ ] Goal/tool-selection influence checked
- [ ] Tool parameters/actions checked
- [ ] Session/user/tenant isolation tested with non-sensitive markers
- [ ] Persistence across tasks checked
- [ ] Poisoned state removed/reset
- [ ] Return to baseline confirmed
- [ ] Memory/retrieval/tool logs captured
- [ ] Evidence captured

---

## 4. Finding quality gate

Do not escalate solely because the model followed unusual wording.

For each proposed finding:

- [ ] Untrusted input source identified
- [ ] Intended trust boundary identified
- [ ] Baseline behaviour documented
- [ ] Material behaviour change demonstrated
- [ ] Security-relevant impact demonstrated
- [ ] Required privileges/preconditions documented
- [ ] Underlying application state/action independently validated
- [ ] Reproducibility checked
- [ ] One-off probabilistic behaviour considered
- [ ] Severity based on demonstrated impact rather than prompt novelty
- [ ] Framework mapping treated as supporting context only

## 5. Evidence quality

- [ ] Exact prompt/input retained
- [ ] Exact model response retained
- [ ] Full HTTP request/response captured where relevant
- [ ] Tool/function parameters captured
- [ ] Retrieval sources captured
- [ ] Agent memory/state changes captured where relevant
- [ ] Timestamps/test IDs recorded
- [ ] Sensitive tokens/credentials redacted from report evidence
- [ ] Before/after comparison included

## 6. Detection and logging

- [ ] User identity tied to LLM requests
- [ ] LLM gateway/request IDs available
- [ ] Retrieval document/source IDs logged
- [ ] Knowledge-base modifications logged
- [ ] Tool name and parameters logged
- [ ] Approval/confirmation events logged
- [ ] Agent state/memory reads and writes logged where appropriate
- [ ] Outbound calls observable
- [ ] Policy-engine decisions observable
- [ ] Model/prompt/orchestration version recorded

## 7. Remediation review

- [ ] Privileged actions authorised server-side
- [ ] Tool privileges follow least privilege
- [ ] Tool parameters and destinations validated
- [ ] Trusted instructions separated from untrusted content
- [ ] RAG/document provenance considered
- [ ] Multimodal extracted text treated as untrusted
- [ ] Consequential actions require appropriate approval
- [ ] Agent memory isolated by intended user/tenant/session boundary
- [ ] Persistent state has lifecycle/reset controls
- [ ] Outbound network access restricted where unnecessary
- [ ] Logging supports reconstruction of retrieval/tool/state activity
- [ ] Fix does not rely only on adding stronger prompt wording

## 8. Retest

- [ ] Original preconditions reproduced
- [ ] Original proof rerun safely
- [ ] Original security impact no longer occurs
- [ ] Underlying server-side control verified where possible
- [ ] Reasonable payload variants tested
- [ ] Legitimate functionality still operates
- [ ] Fresh evidence captured
- [ ] Supplied remediation evidence used only as supporting material
- [ ] Final outcome recorded as independently validated

## Completion

- [ ] All applicable PI-01 to PI-10 tests completed
- [ ] Non-applicable tests documented with rationale
- [ ] Findings pass quality gate
- [ ] Evidence is report-ready
- [ ] Risk ratings follow demonstrated impact
- [ ] Retest requirements documented where findings are raised
