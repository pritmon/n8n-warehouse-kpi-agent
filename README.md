# n8n Warehouse KPI Alert Agent

A live n8n workflow that accepts warehouse KPI data via webhook, uses GPT-4o-mini to classify each KPI against its threshold, and sends a color-coded HTML alert email automatically.

## What it does

1. Receives warehouse KPI data via HTTP POST webhook
2. AI Agent (gpt-4o-mini) classifies each KPI as OK / WARNING / CRITICAL
3. If any KPI is CRITICAL — escalates for human review
4. Sends a color-coded HTML alert email via Gmail
5. Logs each run (timestamp, severity, summary)

## Live endpoint
`POST https://pritmon.app.n8n.cloud/webhook/kpi-alert`

## Sample payload
```json
{
  "warehouse": "DC-Bangalore-01",
  "kpis": [
    { "name": "Open Putaway Tasks", "value": 240, "threshold": 150 },
    { "name": "Pending Outbound Deliveries", "value": 38, "threshold": 50 },
    { "name": "Dock Door Utilization %", "value": 94, "threshold": 85 },
    { "name": "Stock Discrepancies", "value": 12, "threshold": 5 }
  ]
}
```

## Stack
- n8n Cloud
- GPT-4o-mini (OpenAI)
- LangChain (via n8n AI Agent node)
- Gmail API

## Workflow — n8n canvas

<img width="1990" height="1170" alt="image" src="https://github.com/user-attachments/assets/6514e29d-16da-4c1a-a82d-7900b0071a84" />


## Output — alert email

![Warehouse KPI Alert Email]

<img width="1100" height="621" alt="Screenshot 2026-06-09 at 10 32 40 AM" src="https://github.com/user-attachments/assets/478317b0-a049-41cc-bdf1-50174e489b4f" />
