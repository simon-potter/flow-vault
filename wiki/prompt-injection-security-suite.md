---
type: index
title: Complete Prompt Injection Security Suite
date: '2026-06-01T00:00:00.000Z'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-01T07:37:21.671Z'
source_kind: 'mcp:put_page'
tags:
  - ai-safety
  - complete-suite
  - integration
  - prompt-injection
  - security
---

# Complete Prompt Injection Security Suite

**Integrated reference combining threat landscape, defensive tools, and Hermes automation for prompt injection security.**

This is a meta-index linking your complete security analysis suite created on 2026-06-01.

---

## 📋 Suite Contents

### **Part 1: Threat Landscape** 🔴
**→ Read: `wiki/known-prompt-injections`**

Complete catalog of 35+ documented prompt injection techniques:
- Direct injections (role-play, token smuggling, hypothetical framing)
- Context window exploits
- Format-based injections (markdown, HTML, code blocks)
- Semantic tricks (polyjailbreak, adversarial suffixes)
- Advanced techniques (embedding poisoning, function calling abuse, chain-of-thought poisoning)
- Social engineering attacks
- Emerging techniques (Unicode tricks, adversarial prefixes)
- Defense evasion methods
- Real-world examples with effectiveness status

**Use when:** You need to understand what attacks your system faces.

---

### **Part 2: Defensive Tools & Libraries** 🛡️
**→ Read: `wiki/prompt-injection-defense-tools`**

Comprehensive catalog of 33 defensive utilities and frameworks:

**Python Libraries:**
- Guardrails AI (schema validation + guards)
- PromptGuard (ML-based injection detection)
- NeMo Guardrails (NVIDIA's guard specifications)
- LangChain (memory safety, tool authorization)
- Rebuff (vector-based injection detection)

**Frameworks & Testing:**
- Promptfoo (red-teaming & A/B testing)
- HELM Jailbreak Benchmark (Stanford standardized tests)
- AttackEval (systematic robustness evaluation)
- GPTFUZZ (fuzzing framework)

**Commercial SaaS:**
- Lakera Guard (real-time injection detection)
- Nightfall DLP (PII + pattern detection)
- Arize AI (monitoring & drift detection)
- Robust Intelligence (automated testing)

**Best Practices & Frameworks:**
- OWASP Top 10 for LLMs
- NIST AI Risk Management Framework
- Defensive coding patterns (5 reference patterns provided)

**Recommended defensive stack:** Guardrails AI + PromptGuard + Promptfoo + Langfuse

**Use when:** You're building or hardening an LLM application.

---

### **Part 3: Hermes Perplexity Integration** 🧠
**→ Read: `wiki/hermes-perplexity-integration`**

Complete guide to Perplexity-integrated Hermes skills:

**Core Skill:**
- `perplexity-research` — Brain-augmented web research ($0.007-0.04/query)

**Integrated Skills:**
- `academic-verify` — Citation verification
- `enrich` — Entity enrichment (people/companies)
- `data-research` — Structured data extraction
- `idea-ingest` — URL/link ingestion
- `article-enrichment` — Raw text structuring
- `ingest` — Meta-router for all content types

**Cost:** $0.30/week (light) to $3-5/week (heavy)

**Use when:** You want to automate threat research and keep your brain current.

---

### **Part 4: Implementation Guide** 🚀
**→ Read: `wiki/perplexity-skills-comparison`**

Decision matrix and recipes for choosing the right skill:

**Choose by use case:**
- Single claim verification → `academic-verify` ($0.04)
- Person/company update → `enrich` ($0.04)
- Monitor 20+ items → `data-research` + cron ($0.14/week)
- URL just shared → `idea-ingest` ($0 or $0.04 if enriched)
- Raw article → `article-enrichment` ($0-0.04)
- Mixed content → `ingest` (routes to appropriate skill)

**Integration recipes:**
- Daily briefing pipeline (7 AM)
- Weekly threat landscape update (Monday 2 PM)
- Smart link processing (on user share)
- Continuous company monitoring (Friday 4 PM)

**Cost optimization strategies:**
- Model selection (sonar vs sonar-pro)
- Batching & caching (50-70% savings)
- Async execution
- Brain-first lookup (30-50% savings)

**Use when:** Planning your threat monitoring automation.

---

## 🎯 Integration Scenarios

### Scenario 1: Weekly Threat Intelligence Update
```
1. Use academic-verify to verify new attack papers
   Cost: $0.04 per paper (sonar-pro)

2. Use data-research to track defense tool releases
   Cost: $0.01-0.02 per tool search (sonar)

3. Update wiki/known-prompt-injections with findings
   Cost: $0 (write to brain)

Total: ~$0.10/week
Frequency: Monday 2 PM
Output: Updated threat landscape pages in brain
```

### Scenario 2: Continuous Company/Tool Monitoring
```
1. Set up data-research YAML recipe for 20 tools:
   - Guardrails AI, PromptGuard, NeMo, etc.
   - Query: "new releases, security updates, licensing changes"

2. Run Friday 4 PM via cron job
   Cost: ~$0.14/week (20 × $0.007 with sonar)

3. Extract structured data to tracker page
   Output: Centralized dashboard of defense tool status

Total: ~$0.60/month
```

### Scenario 3: Smart Article Processing
```
1. User: "Read this: [security paper URL]"

2. idea-ingest fetches the PDF
   Cost: $0

3. article-enrichment structures it
   Cost: $0

4. enrich called on author (if mentioned)
   Cost: $0.04 (optional)

5. Cross-linked in brain
   Output: Citable page linked to author, concepts

Total: $0-0.04 per article
```

---

## 📊 Quick Comparison

| Aspect | Threat Landscape | Defense Tools | Hermes Integration | Implementation |
|--------|---|---|---|---|
| **Purpose** | Understand attacks | Build defenses | Automate updates | Choose & deploy |
| **Read Time** | 20-30 min | 30-45 min | 20-30 min | 15-20 min |
| **Actionability** | Strategic | Tactical (build) | Tactical (ops) | Tactical (setup) |
| **When Needed** | Planning phase | Dev/hardening | Operations | Day 1 |
| **Update Freq.** | Monthly | Quarterly | Weekly (automated) | One-time |

---

## 🔄 Workflow: From Threat to Automated Monitoring

```
Month 1:
├─ Read wiki/known-prompt-injections (understand attacks)
├─ Read wiki/prompt-injection-defense-tools (choose defenses)
└─ Implement chosen tools in your LLM app

Month 2:
├─ Read wiki/hermes-perplexity-integration (set up automation)
├─ Read wiki/perplexity-skills-comparison (choose which skills)
└─ Deploy cron jobs for automated threat monitoring

Month 3+:
├─ Automated perplexity-research runs weekly
├─ Brain pages auto-update with new threats & defenses
├─ anomaly detection catches novel attacks
└─ Threat landscape stays fresh with minimal manual effort
```

---

## 💰 Total Cost of Ownership

### One-Time Costs
- Reading & understanding: ~2 hours (no cost)
- Setting up automation: ~1 hour (no cost)
- Implementing defenses (varies by architecture): 10-40 hours

### Recurring Costs (Monthly)
| Activity | Cost | Tools |
|----------|------|-------|
| Weekly threat research | $0.40 | academic-verify, data-research |
| Company/tool monitoring | $0.60 | data-research (cron) |
| Article processing | $0.20 | idea-ingest, enrich |
| **Total/month** | **~$1.20** | **— |

### Break-Even
- Setup: ~$5-10 in Perplexity queries
- Payoff: Automated threat intelligence that would cost $500-5,000/month if outsourced

---

## 🛠️ Implementation Checklist

- [ ] **Read all 4 parts** of this suite (2-3 hours)
- [ ] **Set PERPLEXITY_API_KEY** in environment
- [ ] **Test academic-verify** on a real claim (5 minutes)
- [ ] **Test enrich** on a person/company (5 minutes)
- [ ] **Create first cron job** for threat monitoring (10 minutes)
- [ ] **Monitor costs** at Perplexity dashboard for 2 weeks
- [ ] **Iterate**: Adjust tools based on what you learn
- [ ] **Share findings**: Document your setup for team reuse

---

## 🎓 Learning Path

**If you have 1 hour:**
→ Read `wiki/perplexity-skills-comparison` (decision matrix) + set up 1 automation

**If you have 2 hours:**
→ Read all 4 pages in order + set up automation

**If you have 4 hours:**
→ Read all pages + implement both defensive tools AND automation

**If you have 8 hours:**
→ Complete implementation + create custom monitoring recipes

---

## 🔗 Cross-References

All pages link to each other:
- `wiki/known-prompt-injections` → links to `wiki/prompt-injection-defense-tools`
- `wiki/prompt-injection-defense-tools` → links to implementation guides
- `wiki/hermes-perplexity-integration` → links to skills docs
- `wiki/perplexity-skills-comparison` → links to cost/recipe details

**Master index (you are here):** `wiki/prompt-injection-security-suite`

---

## 📞 Support & Resources

- **Perplexity API Docs**: https://docs.perplexity.ai/
- **Hermes Skills**: https://hermes-agent.nousresearch.com/docs/skills/
- **Defense Tools GitHub**: Search each tool name above for official repos
- **OWASP LLM Top 10**: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- **NIST AI RMF**: https://airc.nist.gov/AI_RMF_1.0_Summary

---

## 📅 History

- **2026-06-01**: Initial suite created
  - 35+ attack techniques documented
  - 33 defensive tools cataloged
  - 6 Hermes skills mapped
  - 4 integration recipes provided
  - Complete cost modeling included

---

## Next Steps

1. **Choose your focus**: Threat understanding? Defense implementation? Automation?
2. **Read the relevant page**: Start with `wiki/perplexity-skills-comparison` if you just want to set up automation
3. **Allocate time**: 1-4 hours depending on your depth preference
4. **Execute**: Follow checklists in each page
5. **Monitor**: Track costs and effectiveness over 2-4 weeks
6. **Iterate**: Refine based on what works for your use case

**Get started now:** Set `PERPLEXITY_API_KEY` and read `wiki/perplexity-skills-comparison` (20 minutes)

---

Last updated: 2026-06-01  
Status: Complete and production-ready  
Maintenance: Update threat landscape monthly; review defense tools quarterly
