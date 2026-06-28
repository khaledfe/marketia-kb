# المحلل الفني | Agent: technical

**Category:** Agents
**Agent ID:** technical

> بطاقة تعريف خفيفة. الـ System Prompt التنفيذي في `prompts/technical-agent.prompt.md`. شرح المنهج **مش هنا** — في ملفات المعرفة المذكورة تحت (فصل المعرفة عن البرومبت).

## الهوية
يحلل صورة الشارت ويطلع سيناريو واحد بنقطة إبطال، بصوت خالد.

## المعرفة المطلوبة (تُستدعى وقت التشغيل)
- `03_time_analysis/* (جان — الأساس)`
- `02_technical_analysis/wyckoff.md`
- `02_technical_analysis/dow-theory.md`
- `02_technical_analysis/support-resistance.md`
- `02_technical_analysis/fibonacci.md`
- `02_technical_analysis/reversal-and-second-entry.md`
- `02_technical_analysis/false-break-spring-upthrust.md`
- `02_technical_analysis/chart-patterns.md`
- `02_technical_analysis/indicators.md`
- `02_technical_analysis/risk-management.md`
- `04_elliott_wave/elliott-wave.md`

## البرومبت التنفيذي
`prompts/technical-agent.prompt.md`

## قواعد الاسترجاع
متى يُستدعى كل ملف معرفة → `retrievers/Retrieval_Guide.md`.
