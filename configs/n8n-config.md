# إعدادات n8n | Config

**Category:** Configs

## البنية
- المنصة: Railway (Hobby plan، $5/شهر).
- n8n version: 2.27.4 (Community Edition، License مفعّل).
- Project name: renewed-forgiveness.
- URL: n8n-production-bfd1.up.railway.app
- OAuth Redirect: https://n8n-production-bfd1.up.railway.app/rest/oauth2-credential/callback
- Postgres: شغّال.
- (Oracle Cloud اتجرب واتلغى — capacity errors + تعقيد networking).

## Credentials المربوطة
1. Anthropic (Claude API).
2. Google Sheets (OAuth2 عبر Google Cloud Project "maeketia").
3. Telegram (بوت @MarKeTia_AI_bot).

## Orchestrator Workflow
- Telegram Trigger (On message) → Code Node → Switch (9 routes).
- Switch بيقرأ `{{ $json.command }}` (مخرج Code Node) — مش raw message text.

## HTTP Request Node (لـ Claude API)
- Headers: `x-api-key` (lowercase), `anthropic-version: 2023-06-01`, `content-type: application/json`.
- Body: Specify = JSON mode.

## بند مفتوح
- `file_id` → URL: محتاج خطوة getFile قبل استدعاء Claude بالصورة (تفاصيل في workflows/technical-analysis-workflow.md).

## حدود الاستخدام
- News + Acquisition: لازم حد أقصى استخدام في n8n (أكتر اتنين بيحرقوا توكنز).
