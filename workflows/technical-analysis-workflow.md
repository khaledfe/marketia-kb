# Workflow — التحليل الفني | Technical Analysis

**Category:** Workflows
**Related:** prompts/technical-agent.prompt.md, retrievers/Retrieval_Guide.md, configs/

> توثيق تسلسل التنفيذ. ده أول workflow بيتبني (القاعدة: workflow واحد يشتغل صح قبل التالت).

---

## المدخلات
- صورة شارت من تليجرام (مرسوم عليها أدوات جان/فيبو/مستويات).
- نص اختياري مع الصورة (caption).

## التسلسل

```
1. Telegram Trigger (On message)
       ↓
2. Code Node (JS)
   - يستخرج: command, chat_id, file_id, message_id
   - command = msg.text ?? msg.caption ?? ''
   - file_id = msg.photo[last].file_id (لو فيه صورة)
       ↓
3. Switch Node ({{ $json.command }})
   - route: /analyze → التحليل الفني
       ↓
4. [PENDING] Telegram getFile
   - GET api.telegram.org/bot{TOKEN}/getFile?file_id={file_id}
   - يطلع file_path
   - يبني URL: api.telegram.org/file/bot{TOKEN}/{file_path}
       ↓
5. Retrieval Step
   - حسب retrievers/Retrieval_Guide.md (قسم /analyze)
   - يحمّل: prompt التقني + ملفات جان + (وايكوف/داو/دعم-مقاومة) + دخول + مخاطر
       ↓
6. HTTP Request → Claude API
   - model: claude-sonnet-4-6, max_tokens: ~600
   - Headers: x-api-key, anthropic-version: 2023-06-01, content-type: application/json
   - Body (JSON): system = البرومبت + المعرفة المحقونة، messages = [الصورة (URL/base64) + caption]
       ↓
7. Telegram Send (التحليل) → لخالد للمراجعة
   - Chat ID: {{ $('Telegram Trigger').item.json.message.chat.id }}
   - Text: {{ $json.content[0].text }}
       ↓
8. مراجعة خالد (يدوي) → تعديل → موافقة
       ↓
9. [لاحقاً] Publisher + تسجيل في Predictions/Published_Posts
```

## المخرجات
- تحليل فني (سيناريو واحد + نقطة إبطال + أهداف) بأسلوب خالد.
- مسودة لخالد — مش نشر مباشر.

## نقاط مفتوحة (Pending)
- **خطوة 4 (`file_id` → URL):** لسه مش متنفذة في الـ workflow. لازم تتضاف قبل استدعاء Claude بالصورة.
- **خطوة 5 (Retrieval):** آلية حقن المعرفة من الملفات — تتنفذ حسب `Retrieval_Guide.md`.

## المرجع
- البرومبت: `prompts/technical-agent.prompt.md`.
- قواعد المعرفة: `retrievers/Retrieval_Guide.md`.
- الإعدادات التقنية: `configs/n8n-config.md` + `configs/claude-api-config.md`.
