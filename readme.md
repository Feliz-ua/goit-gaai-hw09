# Support Agent

Навчальний проєкт із агентом технічної підтримки на базі LangGraph і LLM через OpenRouter. Агент класифікує звернення користувача, підбирає відповідні FAQ, формує відповідь українською мовою та визначає, чи потрібна ескалація до спеціаліста.

## Можливості

- класифікація запитів на `question`, `problem`, `complaint` і `general`;
- пошук одного або двох релевантних пунктів FAQ;
- формування короткої відповіді українською мовою;
- ескалація звернень щодо шахрайства, юридичних питань та інших складних випадків;
- перевірка релевантності відповідей і діагностика результатів для п'яти тестових запитів.

## Структура

```text
support_agent.ipynb  # реалізація агента, граф LangGraph і тестування
.env                 # локальні змінні середовища (не додається до Git)
```

Граф агента виконується послідовно:

```text
classify_query -> search_faq -> draft_response -> check_escalation
```

## Вимоги

- Python 3.10 або новіший;
- API-ключ OpenRouter;
- Jupyter Notebook або JupyterLab.

## Встановлення

Створіть і активуйте віртуальне середовище, потім встановіть залежності:

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Встановлення пакетів:

```bash
python -m pip install --upgrade pip
python -m pip install langgraph langchain-openai python-dotenv jupyter
```

## Налаштування

Створіть у корені проєкту файл `.env`:

```dotenv
OPENROUTER_API_KEY=ваш_ключ_OpenRouter
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
OPENROUTER_MODEL=google/gemini-2.5-flash-lite
```

Не додавайте справжній API-ключ до Git або інших публічних файлів.

## Запуск

Запустіть Jupyter:

```bash
jupyter notebook
```

Відкрийте [`support_agent.ipynb`](./support_agent.ipynb) і виконайте комірки послідовно. Фінальна комірка запускає `test_agent()`, повертає список результатів у змінній `results`, а діагностику перевірок зберігає в `test_agent.last_diagnostics`.

> Запуск тестової комірки виконує запити до OpenRouter, які можуть бути платними відповідно до тарифу обраної моделі.

