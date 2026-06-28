# Workflow — النمط العام | General Pattern

**Category:** Workflows
**Related:** retrievers/Retrieval_Guide.md, 05_agents/agents-overview.md

> النمط اللي بيتكرر في كل الـ workflows. كل workflow متخصص بيرث منه.

---

## النمط الموحّد

```
Telegram Trigger → Code Node (parse) → Switch (9 routes) → [Agent Workflow] → Telegram Send → مراجعة خالد
```

## الأوامر والمسارات (Switch)

| الأمر | الـ Agent | البرومبت | المعرفة (من Retrieval_Guide) |
|-------|-----------|----------|------------------------------|
| `/analyze` | Technical | technical-agent.prompt.md | جان + سعر + دخول + مخاطر |
| `/market` | Market | market-agent.prompt.md | market-composite-reading |
| `/write` | Writer | writer-agent.prompt.md | writing-style + post-formats |
| `/style` | Style Guardian | style-guardian-agent.prompt.md | writing-style |
| `/plan` | Planner | planner-agent.prompt.md | content-planning + ICP + products |
| `/growth` | Growth | growth-agent.prompt.md | growth-rules + ICP |
| `/acquire` | Acquisition | acquisition-agent.prompt.md | growth-rules + ICP |
| `/track` | Performance Tracker | performance-tracker-agent.prompt.md | performance-evaluation |
| `/publish` | Publisher | publisher-agent.prompt.md | operational-tables |

## القاعدة المعمارية

1. كل استدعاء = برومبت (من `prompts/`) + ملفات معرفة (حسب `Retrieval_Guide.md`) محقونة في الـ system.
2. مفيش نشر تلقائي — خالد بيراجع.
3. الإعدادات التقنية الموحّدة في `configs/`.

## ربط Code Node (مرجع)
```javascript
const msg = $input.first().json.message;
return [{ json: {
  command: msg.text ?? msg.caption ?? '',
  chat_id: msg.chat.id,
  file_id: msg.photo ? msg.photo[msg.photo.length-1].file_id : null,
  message_id: msg.message_id
}}];
```
