# إعدادات Claude API | Config

**Category:** Configs

- Model: `claude-sonnet-4-6` (Sonnet — مش Opus، لتوفير التكلفة).
- max_tokens: ~600 لاستدعاء التحليل (كافي للبوست).
- API Key name: MarKeTia-n8n (إدارة عبر Anthropic Console).
- Endpoint: https://api.anthropic.com/v1/messages

## قاعدة حقن المعرفة
Claude API ما بيشوفش Project Knowledge أوتوماتيك. المعرفة تتحقن في الـ system prompt من ملفات الـ KB حسب `retrievers/Retrieval_Guide.md`.

## التكلفة
- تحليل واحد ~$0.01. 100 تحليل/شهر < $1.
- إجمالي المنظومة ~$15/شهر (Railway $5 + Claude ~$10).
- نقطة التعادل: مشترك واحد في الـ Membership.
