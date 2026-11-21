# محصولات و پروژه‌های مشابه

تحقیق اول: ۱۴۰۵/۰۸/۳۰ (2026-11-21). هدف: آیا چیزی شبیه «دستیار هوشمند سازمانی» با این مشخصات وجود دارد و از کدام اجزا می‌توان استفاده کرد؟

## جمع‌بندی

!!! abstract "نتیجه اصلی"
    **محصول آماده‌ای که همه نیازها را با هم برآورده کند پیدا نشد.** محصولات تجاری (Microsoft 365 Copilot، Glean، Fireflies) هر کدام بخشی را پوشش می‌دهند، اما (۱) ابری هستند و داده سازمان از کشور خارج می‌شود، (۲) فارسی گفتاری را در حد لازم پشتیبانی نمی‌کنند، (۳) به سامانه‌های داخلی ایرانی (دبیرخانه، CMMS بومی) وصل نمی‌شوند، و (۴) جلسه **حضوری** در اتاق را هدف نگرفته‌اند. پس مسیر درست، **ساخت سکو از اجزای متن‌باز** و داخلی است؛ همان معماری‌ای که در این مستند آمده.

## ۱. دستیارهای سازمانی تجاری

| محصول | چه می‌کند | چه چیزی را پوشش نمی‌دهد |
|---|---|---|
| **Microsoft 365 Copilot + Facilitator** | در Teams یادداشت زنده، اقدامات، پاسخ به سؤال در جلسه؛ متصل به اسناد Microsoft 365 | ابری؛ وابسته به اکوسیستم مایکروسافت؛ اتصال به سامانه‌های داخلی ایرانی ندارد |
| **Glean** | جست‌وجو و دستیار سازمانی روی بیش از صد کانکتور؛ «Enterprise Graph» از افراد، اسناد و فعالیت‌ها؛ Agentهای خودکار | ابری/تجاری؛ بدون دستیار زنده جلسه حضوری؛ بدون فارسی گفتاری |
| **Fireflies Live Assist** | پنل زنده در جلسات Zoom/Meet/Teams: یادداشت زنده، متن با نام گوینده، پیشنهادها (Follow up، Summarize، Action items)، پرسش از جلسات ۳۰ روز گذشته | فقط جلسات آنلاین؛ بارگذاری پایگاه دانش سازمانی هنوز ممکن نیست؛ ابری |

**درس‌ها برای ما:** گراف سازمانی Glean همان ایده [گراف دانش](../architecture/knowledge-graph.md) ماست. Live Assist نشان می‌دهد پیشنهادهای از پیش تعریف‌شده (خلاصه تا اینجا، اقدامات، پیگیری) در کنار پیشنهاد پویا تجربه کاربری خوبی می‌سازد.

## ۲. سکوهای متن‌باز دانش سازمانی (Self-hosted)

| پروژه | نقش احتمالی |
|---|---|
| **Onyx** (Danswer سابق) | چت سازمانی متن‌باز با کانکتورها، RAG و Agent؛ مرجع یا پایه لایه Document RAG |
| **RAGFlow** | موتور RAG با درک عمیق اسناد (جدول، PDF)؛ گزینه برای پردازش نامه و قرارداد |
| **Dify** | سکوی ساخت گردش‌کار LLM؛ برای نمونه‌سازی سریع |

## ۳. ارکستراسیون و حافظه Agent

| پروژه | یافته |
|---|---|
| **Hermes Agent** (Nous Research) | Agent با حافظه پایدار، **ساخت مهارت توسط خود Agent** و نگهداری پس‌زمینه آن‌ها (Curator)، کلاینت **MCP**، ابزار **مرورگر** (Chromium محلی یا CDP)، **Cron** با زبان طبیعی، افزونه حافظه **Honcho**، اتصال به هر Endpoint سازگار با OpenAI و مدل محلی (Ollama، llama.cpp)، اجرا با Docker. دقیقاً با نیاز «Browser-use → ساخت MCP از تجربه» هم‌راستاست |
| **Honcho** (Plastic Labs) | زیرساخت حافظه برای Agentهای دارای وضعیت؛ Self-host؛ PostgreSQL + pgvector؛ مدل Workspace/Peer/Session؛ چندمستاجری با RLS؛ **مجوز AGPL-3.0**؛ احراز هویت پیش‌فرض خاموش |
| **browser-use** | کتابخانه متن‌باز اتصال LLM به مرورگر (Playwright)؛ جایگزین/مکمل ابزار مرورگر Hermes |

## ۴. گفتار به متن فارسی {#stt}

| مدل | پایه | مجوز | نتایج گزارش‌شده (توسط سازندگان) | نکته |
|---|---|---|---|---|
| **Nava** (Nimruz) | whisper-large-v3-turbo، ۵۷۹ ساعت صوت فارسی | MIT | WER: FLEURS ‏۸٫۷٪، Common Voice ‏۱۳٫۲٪ | قطعه‌های ۳۰ ثانیه‌ای، بدون Timestamp؛ با faster-whisper و whisper.cpp اجرا می‌شود |
| **BuzzASR/persian** | whisper-large-v3 (فاین‌تیون کامل) | MIT | WER ترکیبی ۱۴٫۵٪ (CER ‏۴٫۷٪) در برابر CER ‏۱۲٪ Whisper پایه | پردازش دسته‌ای |
| Whisper پایه (OpenAI) | — | MIT | به‌وضوح ضعیف‌تر از نسخه‌های فاین‌تیون | |

**نتیجه:** مدل‌های باز فارسی قابل‌قبولی وجود دارد، اما **هیچ‌کدام Streaming و تشخیص گوینده را آماده ارائه نمی‌کنند**. پیمانکار باید VAD + قطعه‌بندی + Diarization (مثلاً pyannote) را بسازد و دقت را روی **صدای واقعی جلسات دفتر معاونت** (اصطلاحات فنی، اسامی، هم‌پوشانی گفتار) بسنجد. فاین‌تیون روی واژگان سازمان احتمالاً لازم است.

## ۵. دستیارهای جلسه متن‌باز

- **Meetily**: یادداشت‌بردار جلسه متن‌باز و محلی (حریم خصوصی‌محور) با STT محلی. مرجع خوبی برای خط لوله ضبط → متن → خلاصه، ولی دستیار زنده متصل به سامانه‌های سازمانی نیست. (جزئیات مجوز و قابلیت‌ها هنوز تأیید نشده.)
- **WhisperX / pyannote**: اجزای استاندارد متن‌باز برای هم‌ترازی زمانی و تشخیص گوینده.

## ۶. مدل زبانی

خانواده **Qwen** مدل‌های باز با پشتیبانی چندزبانه (از جمله فارسی) هستند و vLLM از نسخه‌های جدید آن پشتیبانی می‌کند. کیفیت فارسی رسمی/اداری و Tool-calling باید با مجموعه آزمون داخلی (نامه‌ها و متن جلسات واقعی) سنجیده شود.

## پیامدها برای مستند فنی

1. معماری «سکوی اختصاصی از اجزای متن‌باز» تأیید می‌شود.
2. Hermes Agent برای ارکستراسیون و یادگیری ابزار گزینه مناسبی است؛ پیمانکار باید یک نمونه اولیه (PoC) روی یک سامانه UI-only اجرا کند.
3. **مجوز AGPL-3.0 در Honcho** باید پیش از قرارداد بررسی حقوقی شود.
4. **STT فارسی زنده با تشخیص گوینده** پرریسک‌ترین بخش فنی است؛ باید در قرارداد معیار پذیرش عددی داشته باشد.
5. هیچ محصول ابری خارجی به دلیل محرمانگی و تحریم گزینه عملی نیست.

## منابع

- [Microsoft Teams Facilitator](https://support.microsoft.com/en-US/teams/copilot/facilitator-in-microsoft-teams-meetings)
- [Glean Enterprise Graph](https://www.glean.com/product/enterprise-graph)
- [Fireflies Live Assist](https://guide.fireflies.ai/articles/6032274417-what-is-fireflies-live-assist-get-real-time-suggestions-answers-and-notes-live-during-the-meeting)
- [Onyx self-hosted RAG](https://onyx.app/insights/self-hosted-rag)
- [Hermes Agent docs](https://hermes-agent.nousresearch.com/docs/llms.txt)
- [Honcho README](https://raw.githubusercontent.com/plastic-labs/honcho/main/README.md)
- [browser-use](https://dev.to/terminalchai/browser-use-the-open-source-library-connecting-llms-to-web-automation-18ic)
- [Nava (Persian ASR)](https://huggingface.co/Nimruz/Nava)
- [BuzzASR/persian](https://huggingface.co/BuzzASR/persian)
- [Meetily](https://github.com/Zackriya-Solutions/meetily)
- [Qwen3](https://github.com/QwenLM/Qwen3)
