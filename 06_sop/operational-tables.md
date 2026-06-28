# الجداول التشغيلية والبنية التقنية | ماركيتيا (SOP)

**Category:** SOP / Operations
**Related Topics:** performance-evaluation, growth-rules, agents-overview, publisher-agent

> مرجع بنية البيانات والبنية التقنية للمنظومة. ملاحظة: مع التصميم الجديد، قاعدة المعرفة هي ملفات Markdown دي + الفهرس Excel؛ والجداول التشغيلية تحت هي **بيانات حية متغيرة** (سجلات) بتفضل في Google Sheets للتشغيل اليومي.

---

## جداول البيانات الحية (Google Sheets)

**Spreadsheet ID:** `1kydy_f82IpJZlUAsRQTCo8yy7nDLbNXZ`

| الجدول | الغرض | الأعمدة الأساسية |
|--------|-------|------------------|
| Predictions | سجل التوقعات | prediction_id, date_published, agent_source, asset, timeframe, prediction_text, target_levels, invalidation_level, confidence, impact_score, status, date_resolved, outcome_notes, root_cause |
| Published_Posts | البوستات المنشورة | post_id, date_published, post_type, platform, topic, content_summary, linked_prediction_id, status |
| Content_Plan | جدول النشر | plan_id, scheduled_date, post_type, topic, assigned_agent, priority, status, notes |
| Growth_Metrics | مؤشرات النمو | record_id, week_start, platform, subscribers_total, subscribers_net_change, active_ratio, avg_views_per_post, share_rate, engagement_rate, from_collaborations, conversion_from_social, market_season, notes |
| Collaborations | التعاونات | collab_id, channel_name, channel_size, date, type, invite_link, subscribers_gained, acquisition_score, status, notes |
| Errors_Log | سجل الأخطاء | error_id, prediction_id, agent_source, root_cause_category, details, date, lesson_learned |

> 🔎 تمييز مهم: الجداول دي **بيانات تشغيلية حية** (بتتغير يومياً)، مش معرفة تأسيسية. المعرفة التأسيسية (المنهج، الأسلوب، القواعد) في ملفات الـ Markdown. الفصل ده مقصود: المعرفة ثابتة، البيانات متغيرة.

---

## البنية التقنية

| المكوّن | التفاصيل |
|---------|----------|
| n8n | Railway، Community Edition، v2.27.4، $5/شهر. URL: n8n-production-bfd1.up.railway.app |
| Claude API | Sonnet (claude-sonnet-4-6)، max_tokens ~600 للتحليل. Key: MarKeTia-n8n |
| Google Sheets | الذاكرة الحية (OAuth2 عبر Google Cloud Project "maeketia") |
| Telegram | الواجهة الأساسية، بوت @MarKeTia_AI_bot |

### إعداد HTTP Request node (Claude API)
- Headers: `x-api-key` (lowercase)، `anthropic-version: 2023-06-01`، `content-type: application/json`.
- Body: JSON mode.

### Orchestrator Workflow
- Telegram Trigger → Code Node (JS) → Switch Node بـ 9 routes.
- Switch بيقرأ `{{ $json.command }}` (مخرج الـ Code Node)، مش raw message text.
- الأوامر: /analyze /market /plan /write /style /growth /track /acquire /publish.

### بند تقني مفتوح (Pending)
- تليجرام بيبعت الصور كـ `file_id` مش URL. لازم خطوة تحويل عبر Telegram API:
  `getFile?file_id={id}` → `file_path` → `https://api.telegram.org/file/bot{TOKEN}/{file_path}` — قبل استدعاء Claude API بالصورة.

---

## قاعدة معمارية حاكمة

> Claude API **ما بيشوفش** Project Knowledge أوتوماتيك (بعكس Claude.ai). عشان كده المعرفة لازم تتحقن في كل request: الـ Agent بيقرأ ملف الـ Markdown المطلوب (يحدده من الفهرس Excel) ويحقنه في الـ system prompt.
>
> System prompts الكاملة للـ Agents لازم تتحفظ في HTTP Request nodes — **النسخ المبسطة غير مقبولة**.
