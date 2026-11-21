# مؤلفه‌ها و فناوری‌های پیشنهادی

!!! note "پیش‌نویس"
    این جدول نقطه شروع است و پس از پاسخ به [سؤالات باز](../open-questions.md) نهایی می‌شود. انتخاب نهایی هر ردیف باید با آزمایش روی داده واقعی سازمان (به‌ویژه صدای فارسی جلسات) تأیید شود.

| مؤلفه | گزینه پیشنهادی | جایگزین‌ها | توضیح |
|---|---|---|---|
| ارکستراسیون Agent | Hermes Agent (Nous Research) | LangGraph، OpenHands، چارچوب اختصاصی | پشتیبانی از MCP، مرورگر، Skills خودساخته، Cron، حافظه Honcho |
| مدل زبانی (LLM) | وب‌سرویس بیرونی مجاز است؛ مسیر جایگزین: مدل باز Qwen روی vLLM داخلی | سایر مدل‌های باز با پشتیبانی خوب فارسی | تنها مؤلفه‌ای که می‌تواند بیرون از سازمان باشد ([نگهداری داده](data-residency.md)) |
| دروازه LLM | LiteLLM | — | جابه‌جایی بین مدل بیرونی و محلی، لاگ و پنهان‌سازی داده حساس |
| سرویس‌دهی مدل | vLLM (Endpoint سازگار با OpenAI) | Ollama، llama.cpp، SGLang | Hermes و Honcho هر دو با Endpoint سازگار با OpenAI کار می‌کنند |
| گفتار به متن فارسی | Whisper فاین‌تیون فارسی (مثل Nava یا BuzzASR) + faster-whisper | سرویس‌های STT داخلی ایران | نیاز به لایه Streaming/VAD؛ ارزیابی روی صدای واقعی جلسات |
| تشخیص گوینده | pyannote.audio | NeMo diarization | ثبت صدای مرجع اعضای ثابت جلسات برای شناسایی نام |
| حافظه مکالمات | Honcho (Self-host) | Mem0، Zep | مجوز AGPL؛ فعال‌سازی احراز هویت |
| پایگاه داده اصلی | PostgreSQL + pgvector | — | رویدادها، تصمیم‌ها، گراف دانش، بردارها |
| گراف دانش | جداول رابطه‌ای در PostgreSQL | Neo4j (اختیاری) | |
| Document RAG | Embedding چندزبانه **محلی** + pgvector | Onyx، RAGFlow (به‌عنوان مرجع یا پایه) | |
| استخراج پیوست‌ها | Docling، PyMuPDF، pandas، LibreOffice، 7-Zip، ezdxf + ODA File Converter | Apache Tika | جزئیات: [پیوست‌ها](../requirements/attachments.md) |
| OCR فارسی | Tesseract / PaddleOCR / Surya / VLM محلی | — | مقایسه روی نامه‌های اسکن‌شده واقعی |
| اتصال به سامانه‌ها | MCP Serverهای اختصاصی | — | Read-only در فاز ۱ |
| مرورگر خودکار | ابزار مرورگر Hermes / Playwright | browser-use | برای سامانه‌های فاقد API |
| زمان‌بندی | Cron داخلی Hermes | Airflow، Temporal | خلاصه خبری ۹ صبح، پردازش شبانه نامه‌ها |
| رابط مانیتور | وب‌اپ تمام‌صفحه RTL با WebSocket | — | نمایش متن زنده، موضوعات، پیشنهادها و منابع |
| امنیت | Vault برای اعتبارنامه‌ها، SSO/LDAP، Audit log | — | |
