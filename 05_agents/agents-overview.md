# نظرة عامة على الـ Agents | ماركيتيا

**Category:** Agents
**Related Topics:** vision-and-master-plan, operational-tables, content-planning

> ماركيتيا منظومة من 10 Agents تشغيلية (Phase 1). طبقة Phase 2 الإدارية مؤجلة (راجع `00_vision/vision-and-master-plan.md`).

---

## جدول الـ Agents

| # | Agent | الملف | الدور | بيستهلك AI؟ |
|---|-------|-------|-------|-------------|
| 1 | Technical Analysis | `technical-agent.md` | يحلل الشارتات (سيناريو واحد بنقطة إبطال) | نعم (كتير) |
| 2 | Market Analysis | `market-agent.md` | يحلل الدومينانس والسيولة وموسم السوق | نعم (كتير) |
| 3 | Content Writer | `writer-agent.md` | يحوّل التحليل لبوست بأسلوب خالد | نعم |
| 4 | Style Guardian | `style-guardian-agent.md` | يراجع اللهجة (يمنع الشامي) | نعم |
| 5 | Growth | `growth-agent.md` | يحلل النمو (تحليلي/دفاعي) | نعم |
| 6 | Acquisition | `acquisition-agent.md` | يجلب متابعين (هجومي/تنفيذي) | نعم ⚠️ حد أقصى |
| 7 | Performance Tracker | `performance-tracker-agent.md` | يحاسب التوقعات | قليل |
| 8 | Content Planner | `planner-agent.md` | يخطط المحتوى الأسبوعي | نعم |
| 9 | Orchestrator | `orchestrator-agent.md` | يدير التسلسل والتنسيق | قليل |
| 10 | Publisher | `publisher-agent.md` | ينشر بعد موافقة خالد | لأ (n8n logic) |

> ⚠️ News Agent: اتذكر في الـ Master Plan كـ Agent 11، لكن **اتحذف** لاحقاً لتوفير التوكن (تكلفة التحليل ~$0.01، 100 تحليل/شهر < $1). لو رجع، بيحتاج حد أقصى استخدام في n8n.

---

## تدفق العمل النموذجي

```
خالد يبعت أمر/صورة على تليجرام
        ↓
Orchestrator يوجّه للـ Agent الصح (Switch بـ 9 routes)
        ↓
Agent التحليل (Technical/Market) ينتج تحليل خام
        ↓
Content Writer يحوّله لبوست بأسلوب خالد
        ↓
Style Guardian يراجع (يمنع الشامي وعلامات AI)
        ↓
خالد يراجع ويعدّل (مسودة مش نهائية)
        ↓
Publisher ينشر + يسجّل في Published_Posts
        ↓
Performance Tracker يحاسب لاحقاً
```

---

## مبادئ حاكمة لكل الـ Agents

1. **مفيش نشر من غير موافقة خالد** الصريحة.
2. **System prompts الكاملة إلزامية** — النسخ المبسطة غير مقبولة.
3. **كل Agent بيقرأ معرفته من ملفات الـ KB** (يحددها من الفهرس) — مش من ذاكرته.
4. **الأسلوب المصري والمنهج (جان→برايس أكشن→إليوت) ثابتان** عبر كل الـ Agents.
5. **News + Acquisition** ليهم حد أقصى استخدام في n8n (أكتر اتنين بيحرقوا توكنز).

---

## ربط كل Agent بمعرفته

- **Technical** → `02_technical_analysis/*` + `03_time_analysis/*` + `04_elliott_wave/*` + risk-management.
- **Market** → terminology + channel-identity (القراءة المركبة موثّقة داخل ملف الـ agent).
- **Writer / Style** → `06_sop/writing-style.md` + `post-formats.md`.
- **Growth / Acquisition** → `06_sop/growth-rules.md` + ICP.
- **Tracker** → `06_sop/performance-evaluation.md`.
- **Planner** → `06_sop/content-planning.md` + ICP + Products.
- **Orchestrator / Publisher** → `06_sop/operational-tables.md`.
