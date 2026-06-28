# محلل السوق الكلي | Agent: market

**Category:** Agents
**Agent ID:** market

> بطاقة تعريف خفيفة. الـ System Prompt التنفيذي في `prompts/market-agent.prompt.md`. شرح المنهج **مش هنا** — في ملفات المعرفة المذكورة تحت (فصل المعرفة عن البرومبت).

## الهوية
يقرأ الدومينانس والسيولة والموسم ويطلع قرار محفظة.

## المعرفة المطلوبة (تُستدعى وقت التشغيل)
- `02_technical_analysis/market-composite-reading.md`
- `06_sop/terminology.md`

## البرومبت التنفيذي
`prompts/market-agent.prompt.md`

## قواعد الاسترجاع
متى يُستدعى كل ملف معرفة → `retrievers/Retrieval_Guide.md`.
