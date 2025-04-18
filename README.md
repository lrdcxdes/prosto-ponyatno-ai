# ПростоПонятно.ai 💡

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-FastAPI-green.svg)](https://fastapi.tiangolo.com/)

Веб-приложение для объяснения сложных тем, концепций, терминов или даже мемов простыми словами с помощью AI (Google Gemini). Реализовано полностью на FastAPI, включая обслуживание фронтенда и API.

*Это приложение создано как демонстрация и Open Source проект. Вы можете использовать его как основу для своих идей!*

![Скриншот ПростоПонятно.ai](placeholder.png)

## ✨ Ключевые возможности

*   🧠 **Объяснение тем с помощью Google Gemini:** Введите любой вопрос или тему и получите ответ.
*   🎯 **Разные уровни объяснения:** Выберите, как объяснить - "просто", "как подростку", "как 5-летнему", "кратко (TL;DR)", "через плюсы и минусы" или попросите AI придумать метафору.
*   🍕 **Пользовательские аналогии:** Предложите свою аналогию (например, "объясни на примере пиццы").
*   📝 **Markdown и подсветка кода:** Ответы форматируются с помощью Markdown, а блоки кода подсвечиваются с помощью `highlight.js`.
*   ✂️ **Копирование кода:** Удобная кнопка для копирования содержимого блоков кода.
*   💾 **Сохранение ответов:** Успешно сгенерированные и валидные ответы сохраняются в JSON-файлы для быстрого доступа и SEO.
*   🔍 **Асинхронный поиск:** Быстрый поиск по заголовкам и началу текста сохраненных объяснений.
*   ⚙️ **SEO-основы:** Генерация отдельных страниц для каждого сохраненного объяснения, `sitemap.xml` и `robots.txt`.
*   🚀 **Полностью на FastAPI:** Бэкенд, API и рендеринг HTML-страниц с помощью Jinja2 - всё в одном фреймворке.
*   🎨 **Обновленный UI:** Чистый, адаптивный интерфейс с поиском в шапке.

## 🚀 Технологический стек

*   **Веб-фреймворк:** [FastAPI](https://fastapi.tiangolo.com/)
*   **Шаблонизатор:** [Jinja2](https://jinja.palletsprojects.com/)
*   **AI Модель:** [Google Gemini API](https://ai.google.dev/) (`google-genai`)
*   **Markdown Рендеринг (Клиент):** [markdown-it](https://github.com/markdown-it/markdown-it)
*   **Подсветка Кода (Клиент):** [highlight.js](https://highlightjs.org/)
*   **Асинхронность:** `asyncio`, `aiofiles`
*   **Хранение данных:** Файловая система (JSON-файлы)
*   **Запуск:** [Uvicorn](https://www.uvicorn.org/)

## 🛠️ Установка и запуск

1.  **Клонируйте репозиторий:**
    ```bash
    git clone https://github.com/lrdcxdes/prosto-ponyatno-ai.git
    cd prosto-ponyatno-ai
    ```

2.  **Убедитесь, что у вас установлен Python 3.8+**.

3.  **Создайте и активируйте виртуальное окружение** (рекомендуется):
    ```bash
    python -m venv venv
    # Linux/macOS
    source venv/bin/activate
    # Windows
    # venv\Scripts\activate
    ```

4.  **Установите зависимости:**
    ```bash
    pip install -r requirements.txt
    ```

5.  **Настройте переменные окружения:**
    *   Переименуйте файл `.env.example` в `.env`.
    *   Откройте файл `.env` и вставьте ваш API-ключ от Google AI Studio (Gemini API):
        ```dotenv
        GOOGLE_API_KEY="ВАШ_GOOGLE_GENERATIVE_AI_API_KEY"
        ```
        Вы можете получить ключ здесь: [Google AI Studio](https://aistudio.google.com/app/apikey)

6.  **Запустите приложение:**
    ```bash
    uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
    ```
    *   `--reload`: Автоматический перезапуск сервера при изменении кода (удобно для разработки).

7.  **Откройте браузер** и перейдите по адресу `http://localhost:8000`.

## ⚙️ Конфигурация

Основная конфигурация выполняется через файл `.env`:

*   `GOOGLE_API_KEY`: **Обязательный** API-ключ для доступа к Google Gemini API.

Приложение автоматически создает папку `app/explanations` для хранения JSON-файлов с объяснениями.

## ▶️ Использование

1.  **Главная страница (`/`):**
    *   Введите тему или вопрос в текстовое поле.
    *   Выберите желаемый стиль объяснения из выпадающего списка.
    *   Если выбран стиль "С моей аналогией...", введите вашу аналогию в появившееся поле.
    *   Нажмите кнопку "Объяснить!".
    *   Результат появится ниже с форматированием Markdown и подсветкой кода. Если объяснение было успешно сохранено, появится ссылка на его постоянную страницу.
2.  **Поиск (в шапке):**
    *   Начните вводить запрос (минимум 3 символа) в поле поиска.
    *   Появится выпадающий список с найденными сохраненными объяснениями.
    *   Кликните на результат, чтобы перейти на страницу этого объяснения.
3.  **Страница объяснения (`/explanation/{slug}`):**
    *   Отображает конкретное сохраненное объяснение.
    *   Имеет уникальный URL, который можно добавить в закладки или поделиться.

## 📁 Структура проекта
```
prosto-ponyatno-ai/
├── app/
│ ├── main.py # Основной файл FastAPI (эндпоинты UI и API)
│ ├── services.py # Бизнес-логика (AI, файлы, поиск)
│ ├── models.py # Pydantic модели (запросы, ответы, хранение)
│ ├── core/
│ │ └── config.py # Загрузка конфигурации (.env)
│ ├── static/ # Статические файлы (CSS, JS)
│ │ ├── styles.css
│ │ └── script.js
│ ├── templates/ # Jinja2 HTML шаблоны
│ │ ├── index.html
│ │ └── explanation_page.html
│ └── explanations/ # Директория для хранения JSON файлов с объяснениями (создается автоматически)
│ └── .gitkeep
├── requirements.txt # Зависимости Python
├── .env.example # Пример файла переменных окружения
├── .gitignore
└── README.md # Этот файл
```

## 💡 Принцип работы

1.  **Запрос пользователя (UI):** Пользователь заполняет форму на главной странице (`index.html`). JavaScript (`script.js`) отправляет POST-запрос на `/api/explain` с темой и параметрами.
2.  **Обработка API (FastAPI):** Эндпоинт `/api/explain` в `main.py` принимает запрос.
3.  **Сервисный слой (`services.py`):**
    *   Функция `get_or_create_explanation` генерирует `slug` для запроса.
    *   Проверяет, существует ли файл `app/explanations/{slug}.json` (кеш).
    *   Если файл есть, читает и возвращает его содержимое.
    *   Если файла нет:
        *   Формирует промпт для Google Gemini API на основе темы и выбранного уровня/аналогии.
        *   Отправляет запрос к `generate_ai_explanation`.
        *   Получает ответ от AI.
        *   **Валидирует ответ:** Проверяет на наличие ошибок, индикаторов неудачи, минимальную длину.
        *   **Если ответ валиден:** Генерирует метаданные (title, description), создает объект `StoredExplanation` и асинхронно сохраняет его в JSON-файл (`save_explanation_to_file`).
        *   Возвращает текст объяснения и `slug`.
        *   **Если ответ не валиден:** Возвращает текст (ошибки или невалидный ответ) и `None` вместо `slug`.
4.  **Ответ API:** Эндпоинт `/api/explain` возвращает JSON с текстом объяснения и `slug` (или `null`, если сохранение не произошло).
5.  **Отображение (UI):** JavaScript на главной странице получает ответ:
    *   Если `slug` есть, рендерит Markdown-текст с помощью `markdown-it` и `highlight.js`, добавляет кнопки копирования и показывает ссылку на `/explanation/{slug}`.
    *   Если `slug` равен `null`, показывает сообщение об ошибке или невалидный ответ.
6.  **Страница объяснения (`/explanation/{slug}`):**
    *   GET-запрос обрабатывается в `main.py`.
    *   `load_explanation_from_file` читает нужный JSON-файл.
    *   Данные передаются в шаблон `explanation_page.html`.
    *   JavaScript в шаблоне рендерит Markdown из переданного текста при загрузке страницы.
7.  **Поиск:**
    *   JavaScript отправляет GET-запросы на `/api/search?q=...` по мере ввода в `search-input`.
    *   Эндпоинт `/api/search` вызывает `search_explanations`, которая асинхронно ищет совпадения `q` в именах файлов (`topic_raw`) и содержимом (`explanation_text`) JSON-файлов.
    *   Возвращается список найденных `slug` и `topic`.
    *   JavaScript отображает результаты в виде ссылок.

## 🤝 Участие в разработке (Contributing)

Буду рад вашему участию! Если у вас есть идеи по улучшению, предложения или вы нашли баг:

1.  **Issues:** Пожалуйста, создайте Issue для обсуждения вашей идеи или проблемы.
2.  **Pull Requests:**
    *   Сделайте форк репозитория.
    *   Создайте новую ветку для вашей фичи (`git checkout -b feature/AmazingFeature`).
    *   Сделайте ваши изменения.
    *   Закоммитьте изменения (`git commit -m 'Add some AmazingFeature'`).
    *   Отправьте ветку в ваш форк (`git push origin feature/AmazingFeature`).
    *   Создайте Pull Request.

## 📄 Лицензия

Этот проект распространяется под лицензией MIT. Смотрите файл `LICENSE` для подробностей (Вам нужно будет добавить файл LICENSE с текстом MIT лицензии в репозиторий).

## 🔮 Возможные будущие улучшения

*   [ ] **Переход на базу данных:** Использовать БД (например, PostgreSQL с `pg_trgm` или SQLite для простоты) вместо JSON-файлов для более эффективного хранения и поиска.
*   [ ] **Кеширование:** Внедрить кеширование (например, с помощью Redis) для API-ответов.
*   [ ] **Оценка ответов:** Добавить кнопки 👍/👎 для сбора обратной связи от пользователей.
*   [ ] **Улучшенный поиск:** Полнотекстовый поиск, учет релевантности, исправление опечаток.
*   [ ] **Админ-панель:** Простой интерфейс для управления сохраненными объяснениями.
*   [ ] **Тесты:** Написание Unit и Integration тестов.
*   [ ] **Docker-контейнеризация:** Упаковка приложения в Docker для легкого развертывания.

---

Надеюсь, этот проект будет полезен! Удачи!