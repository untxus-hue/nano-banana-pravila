# ОФИЦИАЛЫ ПО NANO BANANA PRO (Gemini 3 Pro Image)

**Шпаргалка-справка. Собрана и подтверждена по-странично 10.08.2026. Каждый факт — с адресом.**

Правило сборки: фактом считается только то, что я открыл сам (WebFetch или прямой curl-разбор HTML).
Пересказ Deep-Research без открытия страницы фактом НЕ считается и вынесен в раздел «ОТСЕЯНО»
или «РАСХОЖДЕНИЯ». Ничего в коде завода не менялось.

Проверяемый ресерч оператора: `share.gemini.google/YQglKwjOVpl8` → редирект на
`gemini.google.com/share/771b769e595f` (Gemini 3.1 Pro, Deep Research, 10.08.2026 03:49).
Через WebFetch не открылся (Parse Error: Header overflow); работал по живому снимку страницы
`/tmp/.../scratchpad/ресерч_димы_снимок.txt` — полный текст отчёта внутри.

---

## 1. ОФИЦИАЛЫ (подтверждено по-странично)

Официалом считается только домен Google: `ai.google.dev`, `deepmind.google`,
`blog.google`, `developers.googleblog.com`, `cloud.google.com`, `docs.cloud.google.com`,
`support.google.com`.

### 1.1 deepmind.google/models/gemini-image/pro/
**Статус:** ✅ открыта, та самая модель (Nano Banana Pro = Gemini 3 Pro Image).
- Nano Banana Pro = **Gemini 3 Pro Image**, флагман DeepMind по картинке.
- Разрешения **1K / 2K / 4K**.
- Консистентность: **до 5 персонажей**; **до 14 объектов** в одном воркфлоу.
- Текст на кадре: «lowest error rates (**mostly under 10%**)» на однострочном рендере, лучшие показатели против конкурентов.
- **Все** сгенерированные изображения несут невидимую метку **SynthID**.
- Опирается на «real-world knowledge and deep reasoning» Gemini.
- Доступ: Gemini app, Google AI Studio, Gemini API, Gemini Enterprise Agent Platform.

### 1.2 deepmind.google/models/gemini-image/
**Статус:** ✅ открыта. ⚠ ВНИМАНИЕ: страница сегодня НЕ про старую «Nano Banana», а про всё семейство.
- Три модели: **Nano Banana Pro = Gemini 3 Pro Image**, **Nano Banana 2 = Gemini 3.1 Flash Image**,
  **Nano Banana 2 Lite = Gemini 3.1 Flash-Lite Image**.
- Общее для всех: мультимодальное понимание (картинки + текстовая инструкция), диалоговое уточнение,
  «real-world knowledge» через reasoning, генерация и редактирование.
- Позиционирование: Pro — «studio-quality precision and control»; Flash — «pro-level … at Flash speed»; Lite — самая быстрая и дешёвая.
- Разрешений и SynthID на этой странице НЕТ — брать с других страниц.

### 1.3 ai.google.dev/gemini-api/docs/image-generation («Nano Banana image generation — Interactions API»)
**Статус:** ✅ открыта, та самая модель (плюс соседи по семейству). Это главная API-страница.
- ID модели: **`gemini-3-pro-image`** (в OpenAI-совместимом слое встречается `gemini-3-pro-image-preview`).
- **Лимит референсов — 14, разложенный по ролям:**
  - **до 6** изображений **объектов** (high-fidelity вставка предмета),
  - **до 5** изображений **персонажей** (консистентность лица/анатомии),
  - **до 3** изображений **стиля**.
- Соотношения сторон: `1:1, 3:2, 2:3, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, 21:9`.
- Разрешения: **1K, 2K, 4K**; «K» пишется **заглавной**; по умолчанию **1K**.
  512px (0.5K) — только у Gemini 3.1 Flash-Lite Image.
- **Thinking включён по умолчанию.** «The model generates **up to two interim images** to test
  composition and logic. **The last image within Thinking is also the final rendered image.**»
  Черновики (thought images) отдельно не тарифицируются, но **токены размышления оплачиваются по умолчанию**.
- Параметры: `response_format` (`type`, `mime_type`, `aspect_ratio`, `image_size`),
  `generation_config` → `thinking_level`.
- **Выходные MIME: `image/jpeg` и `image/png`.**
- Все изображения — с водяным знаком **SynthID**.
- Grounding с Google Search — только веб-поиск (не поиск по картинкам).
- Video-to-image у Pro не поддерживается (по этой странице).
- Прицел: «legible, stylized text for infographics, menus, diagrams, and marketing assets».

### 1.4 docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-pro-image — **самая плотная карточка** (нашёл сам)
**Статус:** ✅ открыта (через прямой разбор HTML; WebFetch отдавал только навигацию). Та самая модель.
- Model ID: **`gemini-3-pro-image`**. Launch stage: **GA**. Release date: **28.05.2026**. Retirement: не раньше 28.05.2027.
- **4K-выход остаётся в статусе Preview на GA-эндпоинте.**
- Контекст: вход **65 536** токенов, выход **32 768** токенов.
- **Максимум изображений на промпт: 14.** Размер файла: **7 МБ** inline/консоль, **30 МБ** из GCS. Общий вход — **500 МБ**.
- Соотношения сторон (шире, чем на ai.google.dev): `1:1, 3:2, 2:3, 3:4, 1:4, 4:1, 4:3, 4:5, 5:4, 1:8, 8:1, 9:16, 16:9, 21:9, 9:21`.
- Разрешения: **1K, 2K, 4K (Preview)**.
- **Входные MIME: png, jpeg, webp, heic, heif.**
- **Токеномика картинки:** 560 входных токенов на каждое входное изображение;
  **1120 токенов на 1K (~1 Мп) и на 2K (~4 Мп)**, **2000 токенов на 4K (~16 Мп)**.
- Возможности: Thinking — **поддержан**; system instructions — да; grounding Google Search — да;
  **Content Credentials (C2PA) — поддержаны**; редактирование и мультитёрн-редактирование — да;
  чередование текста и картинок — да. Function calling, structured output, tuning — **НЕТ**.
- Параметры: temperature 0.0–2.0 (**default 1.0**), topP default 0.95, candidateCount 1.
- Регион: только `global`. Batch inference — поддержан.

### 1.5 ai.google.dev/gemini-api/docs/pricing
**Статус:** ✅ открыта. Цены на ту самую модель.
- **Gemini 3 Pro Image (Nano Banana Pro):** вход $2.00/1M токенов; выход $12.00/1M (текст/thinking)
  + **$120.00/1M за изображения** → **$0.134 за кадр 1K/2K** и **$0.24 за кадр 4K**.
- **Batch: ровно вдвое дешевле** → $0.067 (1K/2K) и $0.12 (4K).
- Для сравнения, Gemini 2.5 Flash Image (старая Nano Banana): $0.039 за кадр 1024×1024.

### 1.6 ai.google.dev/gemini-api/docs/models/gemini-3-pro-image (карточка модели, нашёл сам)
**Статус:** ✅ открыта, та самая модель.
- «Sophisticated **reasoning-driven engine** for professional-grade image editing and generation»,
  под сложный графдизайн и высокоточные продуктовые мокапы.
- Вход 65 536 / выход 32 768 токенов. Thinking — поддержан. Статус — GA.

### 1.7 docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking («Thinking»)
**Статус:** ✅ открыта (прямой разбор HTML). Прямо покрывает image-модели.
- Thinking включён по умолчанию; модели обучены выдавать «thinking process» как часть ответа.
- **Gemini 3 Pro Image — в списке моделей с поддержкой Thinking** (вместе с Gemini 3.1 Flash Image и Flash-Lite Image).
- **Таблица уровней — ключевое:**
  | Модель | Допустимые `thinking_level` | По умолчанию |
  |---|---|---|
  | **Gemini 3 Pro Image** | **HIGH** | **HIGH** |
  | Gemini 3 Pro | LOW, MEDIUM, HIGH | HIGH |
  | Gemini 3.1 Flash-Lite Image | MINIMAL, HIGH | MINIMAL |
  То есть у **Nano Banana Pro уровень мышления не понижается** — HIGH единственный.
- **Thought signatures** — зашифрованные слепки внутреннего рассуждения; при мультитёрне их надо
  возвращать модели. Если не передать — **ошибка 400**.

### 1.8 docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3
**Статус:** ✅ открыта (прямой разбор HTML). Про семейство Gemini 3 (не только картинку).
- `thinking_level`: **MINIMAL / LOW / MEDIUM / HIGH**; **HIGH — дефолт** для Gemini 3.
  MINIMAL «is as close as possible to a zero budget … but still requires thought signatures».
- **Температура:** «If your existing code explicitly sets temperature (especially to low values for
  deterministic outputs), it is recommended to **remove this parameter and use the Gemini 3 default of 1.0**
  to avoid potential looping issues or performance degradation».
- **Временные галлюцинации** (контекст: Gemini 3 Flash + инструмент Google Search):
  дословная рекомендуемая системная инструкция —
  «*For time-sensitive user queries that require up-to-date information, you MUST follow the provided
  current time (date and year) when formulating search queries in tool calls. Remember it is 2025 this year.*»
- **Отдельная** рекомендация (когда Search выключен): «*Your knowledge cutoff date is January 2025.*»
- `media_resolution` — управление числом токенов на изображение/кадр (детали vs цена/латентность).

### 1.9 ai.google.dev/gemini-api/docs/gemini-3 (нашёл сам)
**Статус:** ✅ открыта.
- «Nano Banana Pro (also known as Gemini 3 Pro Image) is our highest quality image generation model.»
- **Knowledge cutoff всего семейства Gemini 3 — январь 2025.**
- Нельзя одновременно `thinking_level` и старый `thinking_budget` — **400**.
- «For all Gemini 3 models, we **strongly recommend keeping the temperature parameter at its default value of 1.0**»;
  ниже 1.0 — возможны зацикливание и деградация.

### 1.10 docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-best-practices
**Статус:** ✅ открыта (прямой разбор HTML; через WebFetch отдавалась только навигация). Про Gemini-модели картинки.
Дословный свод правил Google:
- **Be specific** — вместо «fantasy armor» → «ornate elven plate armor, etched with silver leaf patterns, high collar, pauldrons shaped like falcon wings».
- **Provide context and intent** — сказать, ЗАЧЕМ кадр («create a logo for a high-end, minimalist skincare brand»).
- **Iterate and refine** — не ждать идеала с первого раза, доводить фоллоу-апом («make the lighting warmer»).
- **Use step-by-step instructions** — сложную сцену собирать по шагам: сначала фон, потом объект переднего плана, потом ключевой предмет. *(Прямая официальная опора под наш каскадный порядок блоков промпта.)*
- **Describe what you want, not what you don't** — вместо «no cars» → «an empty, deserted street with no signs of traffic».
- **Control the camera** — фото/кино-термины: «wide-angle shot», «macro shot», «low-angle perspective».
- **Prompt for images** — явно писать «create an image of», иначе модель ответит текстом.
- **Pass Thought Signatures** — при мультитёрн-создании/редактировании возвращать thought signatures, чтобы сохранить контекст рассуждения.

### 1.11 docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-limitations (нашёл сам)
**Статус:** ✅ открыта. Прямо называет Gemini 3 Pro Image. **Самое ценное для нас — языки.**
- «For best performance with **Gemini 3 Pro Image**, use the following languages: ar-EG, de-DE, EN,
  es-MX, fr-FR, hi-IN, id-ID, it-IT, ja-JP, ko-KR, pt-BR, **ru-RU**, ua-UA, vi-VN, zh-CN».
  → **русский официально в списке языков наилучшего качества.**
- «For best results using Gemini 3 Pro Image, include a **maximum of 14 images** in an input»
  (для Gemini 2.5 Flash Image — максимум 3).
- **«When generating an image containing text, first generate the text and then generate an image with that text.»**
  → официальная рекомендация: сначала выработать текст, потом просить кадр с ним.
- Модель может выдать не то число картинок, что просили; может ответить только текстом при
  двусмысленном промпте; может нарисовать текст картинкой. Аудио/видео на вход генерация не принимает.
- Небезопасный промпт → ответ с `FinishReason = STOP`.

### 1.12 cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-nano-banana (нашёл сам)
**Статус:** ✅ открыта. Официальный блог Google Cloud, прямо про Nano Banana Pro и Nano Banana 2.
- **Формула T2I:** `[Subject] + [Action] + [Location/context] + [Composition] + [Style]`.
- **Формула мульти-рефа:** `[Reference images] + [Relationship instruction] + [New scenario]` —
  т.е. **явно объяснить модели, ЧЕМ является каждый реф** («вот этот набросок — структура, вот эта ткань — текстура»).
- Редактирование: **семантическая маска словами** (inpainting текстом) + «be explicit about what to keep exactly the same».
- **Текст на кадре, 4 правила:** (1) слова в **кавычках**; (2) **назвать шрифт** («bold, white, sans-serif», «Century Gothic»);
  (3) писать на одном языке и указать язык вывода (локализация); (4) **«text-first hack»** — сначала выработать текст диалогом, затем просить кадр.
- Свет: «three-point softbox setup», «chiaroscuro lighting with harsh, high contrast», «golden hour backlighting creating long shadows».
- Камера/оптика: называть **аппарат** (GoPro / Fujifilm / одноразовая мыльница) и **объектив** («low-angle shot with shallow depth of field (f/1.8)», «wide-angle», «macro»).
- Цвет и плёнка: «as if on 1980s color film, slightly grainy», «cinematic color grading with muted teal tones».
- Материальность: не «пиджак», а «navy blue tweed»; для мокапа называть поверхность («minimalist ceramic coffee mug»).
- Начинать промпт **сильным глаголом** — задать основную операцию.
- Чего НЕ делать: отрицательные формулировки, голые списки ключевых слов, забытая типографика, общие эпитеты без материала/света/камеры.
- Подтверждает: контекст Pro 65 536 / выход 32 768, 1K/2K/4K, до 14 рефов, PNG/JPEG/WebP/HEIC/HEIF на вход,
  knowledge cutoff январь 2025, **C2PA Content Credentials + SynthID на всех кадрах**.

### 1.13 blog.google/technology/developers/gemini-3-pro-image-developers/ (нашёл сам)
**Статус:** ✅ открыта. Официальный блог Google, анонс для разработчиков.
- Подтверждает: до 14 входов сливаются в один кадр; **устойчивое сходство до 5 человек**;
  **6 high-fidelity объектов**; SOTA-рендер текста; SynthID в каждом созданном/отредактированном кадре;
  grounding с Google Search на реальные данные; 2K и 4K.
- На момент публикации — «paid preview» через Gemini API, AI Studio, Vertex AI, Google Antigravity.
  ⚠ Устарело относительно карточки Vertex, где модель уже **GA (28.05.2026)**, а Preview остался только у 4K-выхода.

### 1.14 ai.google.dev/gemini-api/docs/openai («OpenAI compatibility»)
**Статус:** ✅ открыта. Не про модель как таковую, про транспорт — но факты полезные.
- base_url: `https://generativelanguage.googleapis.com/v1beta/openai/`, эндпоинт `/v1/images/generations`.
- Картиночные модели в этом слое: **`gemini-2.5-flash-image`** и **`gemini-3-pro-image-preview`**.
- Поддерживаются `prompt`, `model`, `n`, `size`, `response_format`; grounding и safety — через `extra_body`
  (grounding только на Gemini 3 и новее).

### 1.15 ai.google.dev/gemini-api/docs/models/gemini-3.1-flash-image (для сверки соседа)
**Статус:** ✅ открыта. Это **НЕ** Nano Banana Pro — это Nano Banana 2. Взято только для контраста.
- `gemini-3.1-flash-image`; 0.5K/1K/2K/4K (дефолт 1K); **новые соотношения 1:4, 4:1, 1:8, 8:1**;
  Thinking поддержан; интеграция результатов **и текстового, и картиночного** веб-поиска.
- ⚠ Заявленного в ресерче «лимита 10 объектов и отсутствия переноса стиля» на официальной странице **нет**.

---

## 2. НАУЧНОЕ

### arxiv.org/abs/2510.09263 — «SynthID-Image: Image watermarking at internet scale»
**Статус:** ✅ открыта (abs). **Чья:** Google DeepMind — Sven Gowal + 25 соавторов (Bunel, Stimberg, Stutz,
Hayes, Shumailov, Wiles, Kohli и др.), подана 10.10.2025, cs.CR.
Что в аннотации дословно подтверждается:
- SynthID-Image — **deep-learning-система невидимой маркировки** ИИ-картинок; документирует
  требования, модели угроз и практику развёртывания «at internet scale».
- **Промаркировано более 10 миллиардов изображений и видеокадров** в сервисах Google;
  сервис верификации доступен **только доверенным тестировщикам**.
- Внешний вариант **SynthID-O** доступен по партнёрствам; он бенчмаркается **против других
  post-hoc методов** маркировки и показывает SOTA по визуальному качеству и устойчивости к
  типовым искажениям. → **«post-hoc» (маркировка после генерации) подтверждено самой аннотацией.**
- Выводы обобщаются на другие модальности, включая аудио.

**Что это значит для нас:**
1. Любой кадр из Nano Banana Pro **несёт SynthID** — это не опция, отключения нет ни в API, ни в карточке модели.
2. Плюс к SynthID — **C2PA Content Credentials** (карточка Vertex + Cloud-блог), т.е. в метаданных
   лежит запись о происхождении. Наши пост-обработки (ресайз/JPEG/грейд/ретушь) **метку не снимают**
   по замыслу системы; попытки «вычистить» её означают деградацию картинки.
3. Публичного детектора нет — верификация у Google для доверенных тестировщиков.
   Значит наш «зрячий» контроль на ИИ-происхождение через SynthID построить нельзя.
4. Практический вывод для площадок: считать, что происхождение кадра **технически доказуемо Google-ом**,
   и не строить процессы на предположении «незаметно».

---

## 3. ОТСЕЯНО

| Ссылка / источник | Почему отсеян |
|---|---|
| `docs.cloud.google.com/.../image/img-gen-prompt-guide` («Gemini image generation best practices» из списка оператора) | Домен официальный, **но страница про ДРУГУЮ модель — Imagen 2/3/4**, не про Gemini/Nano Banana. **Именно отсюда растёт правило «текст ≤25 символов»** — к Nano Banana Pro оно не относится. Верная страница — `multimodal/gemini-image-generation-best-practices` (п.1.10) |
| `share.gemini.google/YQglKwjOVpl8` | Это сам ресерч (вывод LLM), не источник. WebFetch не открыл (Header overflow), работал по живому снимку |
| `share.gemini.google/xGT2pvcmIVvp` (вложенная ссылка внутри отчёта) | Открыл: редирект на **тот же самый** `gemini.google.com/share/771b769e595f`. Отчёт ссылается сам на себя |
| `runware.ai/docs/models/google-nano-banana-pro` | НЕОФИЦИАЛ (сторонний API-провайдер). **Именно отсюда вся таблица точных пикселей** (1376×768, 5504×3072 и пр.), правило «resolution=4K только с рефами», формат WEBP на выход, `advancedFeatures→watermark`, совет кэшировать рефы в S3 |
| `docs.comfy.org/tutorials/partner-nodes/google/nano-banana-pro` | НЕОФИЦИАЛ (ComfyUI). Отсюда «ComfyUI Nightly обязателен», «Comfy Cloud auth», «DDR5-выгрузка» |
| `openrouter.ai`, `kie.ai`, `apiframe.ai`, `apipod.ai`, `evolink.ai`, `aifreeapi.com`, `help.apiyi.com` | НЕОФИЦИАЛ — перепродавцы/обёртки API |
| `medium.com`, `allenkuo.medium.com`, `gregrobison.medium.com`, `kolacki.eu` | НЕОФИЦИАЛ — личные блоги |
| `reddit.com` | НЕОФИЦИАЛ — форум |
| `researchgate.net` | НЕОФИЦИАЛ — агрегатор препринтов, не первоисточник |
| `www-veo3.com` | НЕОФИЦИАЛ. В названии домена стоит имя гугловского продукта (Veo 3) — **это не делает сайт официальным**, домен Google-у не принадлежит |
| `discuss.ai.google.dev` (всплыл в поиске) | Форум на домене Google, но **пользовательские сообщения**, не документация — как источник фактов не брал |
| `docs.cloud.google.com/.../models/thinking` через WebFetch | Через WebFetch отдавалась только навигация; **подтверждено повторным прямым разбором HTML** (см. 1.7) — в ОФИЦИАЛАХ |

---

## 4. МЫСЛЯТ ЛИ ОДИНАКОВО «Nano» И «Gemini»

Коротко: **это одна и та же голова, но у картиночной ветки урезан регулятор и другой продукт мышления.**

**Что общего (по официалам):**
- Nano Banana Pro **и есть** Gemini 3 Pro Image — та же линейка Gemini 3, тот же
  knowledge cutoff **январь 2025** (`ai.google.dev/gemini-api/docs/gemini-3`), тот же общий
  механизм thinking (`docs.cloud.google.com/.../models/thinking` перечисляет её в одном списке
  с текстовыми Gemini 3), те же **thought signatures** — зашифрованные слепки рассуждения,
  которые надо возвращать в мультитёрне, иначе **400**.
- Тот же параметр `thinking_level`, та же телеметрия: токены размышления **тарифицируются**.
- Тот же принцип: рассуждение **включено по умолчанию**, а не как надстройка.

**Чем отличается thinking у картиночной модели:**
1. **Продукт мышления другой.** У текстовой Gemini «мысль» — это текстовая цепочка. У Gemini 3 Pro Image
   мысль **материализуется картинками**: «The model generates **up to two interim images** to test
   composition and logic. **The last image within Thinking is also the final rendered image**»
   (`ai.google.dev/gemini-api/docs/image-generation`). То есть модель делает 1–2 черновых прогона
   композиции/логики/типографики и на них проверяет себя — а не гоняет текст в уме.
2. **Регулятор урезан.** У Gemini 3 Pro доступны `LOW / MEDIUM / HIGH`, у Gemini 3.1 Flash-Lite Image —
   `MINIMAL / HIGH`, а у **Gemini 3 Pro Image допустим только `HIGH`, и он же по умолчанию**
   (таблица на `docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking`).
   Проще: у Nano Banana Pro **нельзя «думать поменьше»** — она всегда думает на максимум.
   Это официально закрывает идею «сэкономить, понизив thinking_level» на Pro.
3. **Набор возможностей вокруг мышления другой.** У Gemini 3 Pro Image по карточке Vertex
   **нет** function calling, structured output, tuning, code execution — то есть агентная часть
   рассуждения отключена; оставлены system instructions и grounding через Google Search.
4. **Общее следствие для промпта.** Раз модель рассуждает, а не «диффундирует вслепую», официальные
   гайды требуют не хакерских трюков, а **ясной пошаговой инструкции**: «Use step-by-step instructions»,
   «Provide context and intent», «Describe what you want, not what you don't»
   (`.../multimodal/gemini-image-generation-best-practices`). Ровно как текстовой модели.

---

## 5. РАСХОЖДЕНИЯ

### 5.1 Ресерч оператора vs официалы

**Подтверждается официалами:**
- `gemini-3-pro-image` / `-preview` — да.
- 14 рефов = **6 объектов + 5 персонажей + 3 стиля** — да, дословно (ai.google.dev/image-generation).
- 1K/2K/4K, список соотношений сторон — да (Vertex-карточка даёт даже шире: +1:4, 4:1, 1:8, 8:1, 9:21).
- «Модель тестирует композицию перед финальным рендером», **до двух thought images**,
  финальный кадр — последний в цепочке Thinking — да, дословно.
- Thought signatures обязательны в мультитёрне, иначе 400 — да.
- SynthID на всех кадрах; arxiv 2510.09263 (Sven Gowal + 25), post-hoc, 10+ млрд кадров — да.
- Текст: ошибок «mostly under 10%» на однострочном рендере — да (deepmind.google/.../pro/).
- Batch API дешевле на 50 % — да (страница цен).
- Grounding через Google Search — да (у Pro — **только веб-поиск**; поиск по картинкам появился у Nano Banana 2).
- Системная инструкция про «Remember it is [год] this year» и «knowledge cutoff January 2025» —
  **формулировки настоящие**, но см. ниже про контекст.

**ПРОТИВОРЕЧИТ официалам:**
1. **«thinking_level LOW/MINIMAL для Gemini 3 Pro Image»** — ❌. Официальная таблица Google:
   у **Gemini 3 Pro Image единственное допустимое значение — HIGH** (оно же дефолт).
   Понижать уровень мышления у Pro нельзя, «экономия на thinking_level» на этой модели не существует.
2. **«temperature ближе к нулю для детерминированности»** — ❌ прямо наоборот.
   Google: «strongly recommend keeping the temperature parameter at its default value of **1.0**»;
   явное занижение рекомендуют **убрать из кода** (риск зацикливания и деградации).
3. **Точная таблица пикселей (1376×768, 2752×1536, 5504×3072 и т.д.)** — ❌ не официальная,
   она снята с `runware.ai`. Google официально даёт только: **1K ≈ 1 Мп, 2K ≈ 4 Мп, 4K ≈ 16 Мп**
   и токеномику 1120 / 1120 / 2000 + 560 токенов за каждое входное изображение.
4. **«`resolution: "4K"` допустим только вместе с `inputs.referenceImages`»** — ❌ не подтверждено
   ни на одной странице Google; это правило конкретного провайдера (runware).
5. **Выходной WEBP** — ❌. Официально выход — `image/jpeg` и `image/png`.
   WEBP/HEIC/HEIF — это **входные** MIME-типы.
6. **«Черновые thought images тарифицируются»** — ⚠ неточно. Google: сами черновики **отдельно не
   тарифицируются**, но **токены размышления оплачиваются по умолчанию**. Смысл экономики другой.
7. **«Gemini 3.1 Flash Image ограничена 10 объектами и не поддерживает перенос стиля»** — ❌ не подтверждено
   на официальной странице модели.
8. **Тайминги генерации 12–18 / 15–22 / 25–35 сек** — ❌ ни на одной странице Google нет; источник неизвестен.
9. **Системный промпт про даты** — ⚠ контекст подменён. Официально это рекомендация для
   **Gemini 3 Flash при включённом инструменте Google Search**, и это **две разные** рекомендации,
   которые ресерч склеил в одну строку. Дословно у Google: «Remember it is **2025** this year» —
   т.е. пример под свою дату, а не универсальная константа.
10. **Требования ComfyUI Nightly / Comfy Cloud / выгрузка в DDR5 / кэширование рефов в S3** — ❌
    к Google отношения не имеют, это ComfyUI и runware.
11. **Статус модели** — ⚠ ресерч не сказал главного: модель **GA с 28.05.2026**, но
    **4K-выход всё ещё Preview** на GA-эндпоинте.

**Чего в ресерче не было, а нам полезно:**
- **ru-RU официально в списке языков наилучшего качества для Gemini 3 Pro Image.**
- Официальное «сначала выработай текст, потом проси кадр с этим текстом».
- Формулы промпта от Google Cloud: `[Subject]+[Action]+[Location]+[Composition]+[Style]`
  и `[Reference images]+[Relationship instruction]+[New scenario]`.
- **C2PA Content Credentials** — вторая метка происхождения помимо SynthID.
- Лимиты веса: 7 МБ inline / 30 МБ из GCS / 500 МБ вход; окно 65 536, выход 32 768.
- У Pro **нет** function calling и structured output.

### 5.2 Официалы vs /root/АВТОЗАВОД/РЕСЕРЧ_GEMINI_06-08.md (тот файл НЕ правился)

| Пункт 06-08 | Вердикт по официалам 10.08 |
|---|---|
| **п.15** «кириллица ~25 символов на фразу, длиннее — резать» | ❌ **Порог 25 символов взят не из той модели.** Он живёт на `docs.cloud.google.com/.../image/img-gen-prompt-guide` — странице про **Imagen**, а не Gemini/Nano Banana. Живой замер завода (~160 симв. кириллицы без ошибок) официалам **не противоречит**: у Gemini 3 Pro Image заявлен рендер «legible, stylized text for infographics» и ru-RU в списке лучших языков. Правка в файле 06-08 (рабочий порог ~200 симв. блоками) — **подтверждается** |
| **п.15** «кавычки обязательны», «шрифт задаётся общим стилем» | ✅ кавычки — официальная рекомендация Google Cloud. ⚠ но про шрифт официал говорит **обратное**: шрифт надо **называть** («bold, white, sans-serif font», «Century Gothic»), а не полагаться на общий стиль |
| **п.1** «"free of lettering" провоцирует текст, нужна семантически плотная замена» | ✅ **направление подтверждено принципом Google**: «Describe what you want, not what you don't» (вместо «no cars» → «empty, deserted street»). Механизм (BPE-токенизация) официалом не подтверждён — но вывод верный |
| **п.2** «фоновые фигуры спиной — через структурные детали, и ставить в блоке КОНТЕКСТА до модификаторов стиля» | ⚠ не подтверждено дословно, **но не противоречит**: официальная формула Google ставит `[Composition]` и `[Style]` **в конце** — т.е. содержательное раньше стилевого. Совпадает по духу |
| **п.3** «низкий ракурс — только геометрическим принуждением, "камера на уровне асфальта" игнорируется» | ❌/⚠ **противоречит официалу**: Google прямо учит «Control the camera … "low-angle perspective"», «low-angle shot with shallow depth of field (f/1.8)». Ракурс словами официально работает. Наш обходной приём — кандидат на **перепроверку живьём**, возможно он лечил симптом старой модели |
| **п.4** «минимум 3 рефа лица (анфас/3-4/профиль)» | ⚠ официального минимума нет. Официально: **до 5 изображений персонажа** для консистентности. Направление «больше ракурсов лица» вписывается в лимит, но цифра «3» — наша, не Google |
| **п.5** «серый 18 % фон рефов — эталон» | ⚠ официалом **не подтверждено и не опровергнуто** — Google про фон рефов не пишет ничего. Остаётся нашим эмпирическим правилом |
| **п.6** «порядок рефов = иерархия внимания: структура → лицо → товар → фон» | ⚠ **не подтверждено**. Google даёт не порядок, а **роли**: 6 объектов / 5 персонажей / 3 стиля, и требует **словами объяснить роль каждого рефа** («Relationship instruction»). Это сильнее порядка — кандидат в правило: не полагаться на индекс, а подписывать роль в тексте промпта |
| **п.7–9** (судья кадра, VQAScore/DSG, гало) | вне зоны Google-официалов, не сверялось |
| **п.10–12** (Telegram/Higgsfield/Instagram) | вне зоны Google-официалов, не сверялось |
| **п.13–14** (CTR, эмодзи) | вне зоны Google-официалов, не сверялось |

### 5.3 ⚠ Главная оговорка по применимости

Завод ходит в модель **не напрямую в Google API**, а через Higgsfield
(`мотор.py:38` → `МОДЕЛЬ_УМОЛЧАНИЕ = "nano_banana_pro"`). Поэтому:
- **Применимо напрямую:** всё про промпт (формулы, текст в кавычках, шрифт словами, камера/свет,
  позитивные формулировки, пошаговость), лимиты рефов и их роли, языки, SynthID/C2PA, поведение thinking.
- **НЕ применимо напрямую:** `thinking_level`, `thought_signature`, парсинг `parts[]` и отсев
  thought images, `image_size`/`response_format`, цены за кадр Google, batch-скидка — всё это уровень
  Google API. Через посредника эти рычаги могут быть скрыты, зафиксированы или названы иначе.
  Прежде чем что-то из этого «чинить» в коде — проверять живьём, что посредник вообще их пробрасывает.
