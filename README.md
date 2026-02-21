# Preply

Inverview prep.
Letter of motivation.

---

See detailed usage guide on
[Notion](https://zealous-eagle-e27.notion.site/Preply-30ecbccaa2ee807fbe5ac5dd20fb6731)

---

## skillE - AI Native Agent System

skillE is an AI Native Agentic Engineering system that provides specialized expertise for web performance analysis and optimization. (https://agentskills.io/home)

<img src="./Screenshot 2026-02-21 at 18.26.25.png" alt="Opencode" />

### What is skillE?

skillE is an agentic AI system that uses specialized experts to analyze and improve web performance. It leverages large language models with domain-specific knowledge to audit websites, identify performance issues, and provide actionable recommendations.

### Quick Start for Developers New to AI Native Agentic Engineering

If you're unfamiliar with AI Native Agentic Engineering, follow these steps to get started:

#### 1. Install opencode (Recommended AI Harness)

opencode is an interactive CLI tool that helps you work with AI Native Agentic Systems like skillE. It provides a smooth onboarding experience for developers new to agentic engineering.

```bash
# Install opencode via npm
npm install -g opencode

# Or via Homebrew on macOS
brew install opencode
```

#### 2. Verify Installation

```bash
opencode --version
```

#### 3. Run skillE

Once opencode is installed, you can interact with skillE:

```bash
opencode

$ /web_performance <Prompt>

```

Then describe what you need help with, for example:
"Analyze the web performance of https://example.com and save the results to WEB_PERFORMANCE.expert.md"

### Available Skills

- **Web Performance**: Analyzes website performance metrics, identifies bottlenecks, and provides optimization recommendations

### Project Structure

```
.agents/
├── skills/
│   └── web-performance/
│       ├── SKILL.md           # Skill definition
│       └── skillE/
│           └── web_performance/
│               ├── WEB_PERFORMANCE.expert.md    # Expert knowledge base
│               └── web_performance.audit.md      # Audit results
```

### Tips for Success

1. **Start with clear goals**: When asking skillE to analyze something, be specific about what you want to achieve
2. **Iterate**: AI agents work best through iterative refinement - start with a broad analysis, then dive deeper into specific areas
3. **Review outputs**: Always review the generated expert files and audits for accuracy
4. **Use opencode**: The opencode CLI provides an interactive experience that guides you through working with AI agents
