# Teads AI Ops Hub

An intelligent workflow orchestrator for Teads' publisher and campaign operations team. Powered by n8n and AI agents.

## Overview

The **Teads AI Ops Hub** is a multi-agent system that provides real-time insights into publisher health, campaign performance, and creative optimization. It serves as a centralized intelligence layer for Teads' operations team.

## Features

- **Publisher Health Analysis**: Fill rates, eCPM trends, integration monitoring, revenue tracking
- **Campaign Performance Monitoring**: CTR analysis, budget pacing, impression delivery, underperformance detection
- **Creative Intelligence**: Ad creative scoring, performance prediction, optimization recommendations
- **Automated Reporting**: HTML email reports with actionable insights
- **Conversation Memory**: Context-aware chat with 10-message window

## Architecture

### Core Components

1. **Chat Trigger**: Web-based chat interface for querying the system
2. **Parent Orchestrator Agent**: LLM-based orchestrator using Ollama (qwen3:8b)
3. **Three Specialized Sub-Agents**:
   - Publisher Health Agent (ID: iyGFC0AEAutQQzl5)
   - Campaign Performance Agent (ID: 66ZURSQR0d0xT8CW)
   - Creative Intelligence Agent (ID: MItrR9pyCh0WrIRf)
4. **Memory Management**: Simple window-based conversation memory (10 messages)
5. **Health Score Calculator**: Publisher quality scoring tool
6. **Email Delivery**: Gmail integration for automated reporting

### Data Flow

```
Chat Input
    ↓
Parent Orchestrator Agent
    ├→ Publisher Health Agent
    ├→ Campaign Performance Agent
    └→ Creative Intelligence Agent
    ↓
Synthesis & HTML Conversion
    ↓
Gmail Report Delivery
```

## Installation

### Prerequisites

- n8n instance (self-hosted or cloud)
- Ollama with qwen3:8b model installed
- Gmail account with app-specific passwords
- Access to sub-agent workflows

### Setup Steps

1. **Import the workflow** into your n8n instance:
   - Go to n8n → Workflows
   - Click "Import"
   - Upload the `workflow.json`

2. **Configure credentials**:
   - **Ollama**: Point to your Ollama instance (default: localhost:11434)
   - **Gmail**: Authenticate with your Google account
   - **Sub-agents**: Ensure Publisher Health, Campaign Performance, and Creative Intelligence workflows are deployed

3. **Deploy sub-agents**:
   - Create/import the three specialized agent workflows
   - Update workflow IDs in the main orchestrator

4. **Test**:
   - Open the chat interface
   - Ask a question like: "What's the health of our publishers?"

## Usage Examples

### Publisher Queries
```
"Which publishers have fill rates below 50%?"
"Show me revenue trends for tech publishers"
"What's the integration status of our direct JS publishers?"
```

### Campaign Analysis
```
"Which campaigns are underperforming on CTR?"
"Show budget pacing status across all campaigns"
"Which campaigns have impression delivery issues?"
```

### Creative Optimization
```
"Which creatives have the lowest performance scores?"
"Show underperforming creative recommendations"
"What creative types are performing best?"
```

## Health Score Calculation

The system calculates publisher health scores (0-100) based on:
- **Fill Rate** (40%): Percentage of ad requests filled
- **Revenue Trend** (35%): Month-over-month revenue change
- **eCPM** (25%): Effective cost per mille

### Risk Levels
- 🔴 **CRITICAL**: Score < 40
- 🟡 **WARNING**: Score 40-60
- 🟢 **HEALTHY**: Score > 60

## Configuration

### System Prompt

The orchestrator uses this system prompt:
```
You are the Teads AI Ops Hub Orchestrator — an intelligent assistant 
for Teads' publisher and campaign operations team.

You have access to three specialized sub-agents via tools:
- Publisher Health Agent
- Campaign Performance Agent  
- Creative Intelligence Agent

For multi-domain questions → call multiple agents in parallel 
and synthesize results.
```

### Email Template

Reports are sent as HTML emails with:
- Red header banner
- Synthesized insights from all agents
- Status badges (CRITICAL/WARNING/HEALTHY)
- Tables with sortable metrics
- Actionable recommendations

## Workflow IDs

| Component | ID |
|-----------|-----|
| Teads AI Ops Hub | EAG67cZLbBAsytoF |
| Publisher Health Agent | iyGFC0AEAutQQzl5 |
| Campaign Performance Agent | 66ZURSQR0d0xT8CW |
| Creative Intelligence Agent | MItrR9pyCh0WrIRf |

## Troubleshooting

### Workflow doesn't execute
- Check Ollama is running: `curl localhost:11434`
- Verify sub-agent workflows are deployed
- Check Gmail credentials are valid

### No email received
- Check Gmail account is authenticated
- Verify "Less secure apps" is enabled in Gmail settings
- Check spam folder

### Incomplete responses
- Increase context window in Simple Memory node
- Check Ollama model has sufficient tokens
- Verify sub-agents are returning complete data

## Future Enhancements

- [ ] Real-time publisher monitoring dashboard
- [ ] Scheduled daily/weekly reports
- [ ] Slack integration
- [ ] Publisher/campaign alerts with thresholds
- [ ] Historical trend analysis
- [ ] Predictive models for performance forecasting
- [ ] Integration with Teads API for live data

## License

Internal Teads Project - All Rights Reserved

## Support

For issues or questions, contact the operations team or Adi Masturov.

---

**Created**: March 7, 2026  
**Last Updated**: May 21, 2026  
**Version**: 1.0.0
