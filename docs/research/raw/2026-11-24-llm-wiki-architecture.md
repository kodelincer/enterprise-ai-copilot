# متن خام: LLM Wiki و تفکیک مسئولیت‌ها (۱۴۰۵/۰۹/۰۳ — 2026-11-24)

!!! note
    پیام رضا بدون ویرایش. جمع‌بندی در [دانش ترکیبی: LLM Wiki + RAG + حافظه](../../architecture/llm-wiki.md).

> based on this add the idea and tools and explain if needed and update the webdoc in git : What you're describing is more than a RAG application. It is an enterprise knowledge system with persistent knowledge, document retrieval, agent memory, reasoning, and quality control.5. My recommendation for your architecture
> I'd separate these responsibilities:
>
> | Technology | Role |
> |---|---|
> | Obsidian | Knowledge workspace and visualization |
> | Markdown | Persistent knowledge format |
> | Hermes | Agent and orchestration |
> | LLM | Analysis, synthesis, and reasoning |
> | QMD | Local hybrid search over Markdown |
> | Honcho | Agent/user conversational memory |
> | Original document storage | Immutable source of truth. |
>
> also data about this link and how can merge and be use in our project : https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f?utm_source=chatgpt.com
>
> For larger knowledge bases, he suggests adding a search engine such as QMD.RAG is a retrieval mechanism. LLM Wiki is a knowledge-management architecture.
>
> | Component | Responsibility |
> |---|---|
> | Honcho / agent memory | Remember useful context about users, agents, and ongoing work |
> | RAG | Retrieve precise information from original documents |
> | LLM Wiki | Maintain interconnected, evolving knowledge synthesized from documents |
>
> For your metro AI assistant, I would actually combine all three.
