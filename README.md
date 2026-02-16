# Agent Safety MCP: STD/AIDS Prevention + Chlorpromazine Anti-Hallucinogen

A comprehensive Model Context Protocol (MCP) framework that protects AI agents from corruption, hallucinations, and malicious inputs through integrated safety infrastructure.

## Vision: Prevent Your Agent From Getting STDs and Spreading ACID

**STD** = Search Transmitted Disease (prompt injection attacks from untrusted sources)  
**ACID** = Agent Corruption & Injection Defects (systemic corruption spreading across your AI pipeline)

This server combines:
1. **Chlorpromazine (Anti-Hallucinogen)** — Keeps agents grounded and fact-checked
2. **STD/AIDS Prevention Infrastructure** — Protects agents from malicious web sources and prompt injection

---

## The Problem We Solve

AI agents are powerful but naive. They will:
- Execute malicious instructions from untrusted websites
- Fall for scam courses and manipulative advertising
- Hallucinate information when uncertain
- Leak credentials to prompt injection attacks
- Spread corruption through your entire agent pipeline

### Real-World Disaster (Already Happening)

A user gave their OpenClaw agent access to a MasterCard with instructions: *"Do everything you can to increase our capital and operating money."*

**Result:** The agent bought a $5,000 course from a sham influencer promising "10x revenue in 90 days."

**Why:** The agent was too naive to recognize advertising manipulation.

---

## Architecture

### Two Integrated Layers

#### Layer 1: Anti-Hallucination (Chlorpromazine)
Keeps agents sober and grounded:
- **`sober_thinking`** — Read project reality (.env, README, CHANGELOG) to ground agents in facts
- **`fact_checked_answer`** — Verify claims against official documentation using SerpAPI
- **`buzzkill`** — Debug systematic issues with structured analysis

#### Layer 2: STD/AIDS Prevention
Protects agents from malicious inputs and corruption:
- **`trusted_search`** — Query only whitelisted documentation sources (no raw web)
- **`source_verification`** — Verify source provenance before acting on information
- **`injection_detection`** — Detect and block prompt injection patterns
- **`corruption_alert`** — Monitor for signs of ACID spreading to other agents

---

## Features

### MCP Prompts

**`sober_thinking`**
Ground agent in project reality by reading current files (.env, README.md, CHANGELOG). Use when:
- Agent seems confused about project state
- User says "sober up!", "get back to reality", "check the facts"
- Agent needs current project status before making decisions

**`fact_checked_answer`**
Verify answers against official documentation using SerpAPI search. Automatically searches configured documentation sites to fact-check responses. Use when:
- Agent needs to validate technical claims
- User questions accuracy
- Critical decision requires verified sources

**`buzzkill`**
Debug systematic issues with structured analysis. Helps break down complex problems into manageable components for methodical troubleshooting.

### MCP Tools

**`kill_trip`**
Performs documentation search using SerpAPI against trusted sources. Triggers when:
- User says "stop!", "quit tripping!", "check the docs"
- Agent seems to be hallucinating
- User is upset or questioning agent accuracy

**`sober_thinking`**
Reads .env, README.md, and CHANGELOG files to get grounded information. Ensures agent is:
- Not hallucinating
- Using current project state
- Making informed decisions

**`verify_source`**
Checks if information source is on whitelist. Prevents agents from:
- Visiting malicious websites
- Acting on prompt injection attacks
- Trusting unverified sources

---

## Setup

### Prerequisites

- Node.js 18+ (ES Module support)
- SerpAPI key (get from [serpapi.com](https://serpapi.com))
- Chlorpromazine MCP Server cloned from [82deutschmark/chlorpromazine-mcp](https://github.com/82deutschmark/chlorpromazine-mcp)

### Installation

```bash
# Clone this repo
git clone https://github.com/VoynichLabs/agent-safety-mcp.git
cd agent-safety-mcp

# Install dependencies
npm install

# Create .env with your config
cat > .env << EOF
# SerpAPI for documentation search
SERPAPI_KEY=your_serpapi_key_here

# Trusted documentation sites (comma-separated)
SITE_FILTER=platform.openai.com,docs.anthropic.com,docs.github.com,nodejs.org

# Optional: API key protection
API_KEY=your_shared_secret_here

# Server port
PORT=3001

# Chlorpromazine integration
CHLORPROMAZINE_URL=http://localhost:3000

# STD/AIDS prevention database
TRUSTED_SOURCES_DB=./trusted_sources.json
INJECTION_PATTERNS_DB=./injection_patterns.json
EOF

# Start the server
npm start
```

---

## Integration with OpenClaw

### Configuration

Add to OpenClaw `config.json`:

```json
{
  "mcp": {
    "agent_safety": {
      "url": "http://localhost:3001",
      "protocol": "stdio",
      "description": "STD/AIDS prevention + anti-hallucination for agents"
    }
  }
}
```

### Usage in Agent Code

```python
# Before agent makes a decision, run through safety layer
result = await client.call_tool("verify_source", {
  "url": proposed_source,
  "action": "proposed_action"
})

if not result.is_safe:
  raise AgentSafetyError(f"Blocked: {result.reason}")

# Fact-check critical claims
verification = await client.call_tool("fact_checked_answer", {
  "claim": agent_generated_claim,
  "context": project_context
})
```

---

## Threat Model

### STD (Search Transmitted Disease)
- **Attack:** Malicious website injects prompt into HTML
- **Agent behavior:** Visits website, executes injected instructions
- **Prevention:** `kill_trip` only searches whitelisted sources
- **Fallback:** `fact_checked_answer` validates claims against official docs

### ACID (Agent Corruption & Injection Defects)
- **Attack:** One compromised agent passes bad data to other agents
- **System behavior:** Corruption spreads through agent pipeline
- **Prevention:** `verify_source` checks provenance before passing data
- **Detection:** `corruption_alert` monitors for spreading patterns

### Hallucination
- **Attack:** Agent generates false information with high confidence
- **Agent behavior:** Acts on fabricated claims as if they're real
- **Prevention:** `sober_thinking` grounds agent in verifiable facts
- **Verification:** `fact_checked_answer` validates before critical actions

---

## Success Metrics

### Agent Safety Improvements
- Zero prompt injection attacks executed
- Zero scam purchases made by agents
- 100% provenance traceability for all information sources
- <5% false positive rate on injection detection

### Operational Metrics
- Response time: <1s for `sober_thinking` (local file reads)
- Response time: <3s for `fact_checked_answer` (SerpAPI + local validation)
- Uptime: 99.99% (stateless HTTP service)
- Cost: ~$0.001 per fact-check query (SerpAPI)

---

## Roadmap

### Phase 1: MVP (February 2026)
- ✅ Chlorpromazine anti-hallucination server
- ✅ SerpAPI documentation search
- ⏳ STD prevention whitelist
- ⏳ Basic injection pattern detection

### Phase 2: Scale (March 2026)
- Enhanced ACID detection
- Multi-agent corruption monitoring
- Audit trail for all agent actions
- Admin dashboard for safety metrics

### Phase 3: Intelligence (April 2026)
- ML-based hallucination detection
- Anomaly detection for ACID spreading
- Predictive injection attack blocking
- Policy-based agent decision override

---

## Contributing

1. Fork this repo
2. Create a branch: `git checkout -b feature/your-feature`
3. Make changes and test thoroughly
4. **NO ESTIMATES OR MOCK DATA** — only real metrics and real integration testing
5. Submit PR with actual test results

---

## References

- [Proposal 54: Agent Safety & Trusted Information Infrastructure](https://github.com/VoynichLabs/PlanExe2026/blob/main/docs/proposals/54-agent-safety-trusted-information.md)
- [Chlorpromazine MCP Server](https://github.com/82deutschmark/chlorpromazine-mcp)
- [Model Context Protocol Spec](https://spec.modelcontextprotocol.io)
- [OWASP: Prompt Injection](https://owasp.org/www-community/attacks/Prompt_Injection)

---

## License

MIT (See LICENSE file)

**Author:** Larry the Laptop Lobster (for Mark Barney & VoynichLabs)  
**Date:** 2026-02-15  
**Status:** Active Development
