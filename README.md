# 🏢 Bitrix Integration Suite

**Комплексное решение для интеграции с Bitrix24 и сопутствующими сервисами**

## 📋 Описание

Bitrix Integration Suite — это объединенная платформа для работы с Bitrix24, включающая REST API клиент, интеграции с внешними сервисами, автоматизацию бизнес-процессов и обширную базу знаний.

### 🔥 Объединенные проекты:
- ✅ **bitrixdock** (TypeScript) - REST API клиент
- ✅ **bitrix-dadata-integration** (Python) - интеграция с DaData
- ✅ **everest-dedupe-bot** (Python) - дедупликация компаний
- ✅ **awesome-bitrix** - база знаний и ресурсы

## ⭐ Основные возможности

### 🔌 REST API Клиент
- **Современный TypeScript клиент** для Bitrix24 REST API
- **Типизированные методы** для всех основных сущностей
- **Автоматическая пагинация** и обработка ошибок
- **Batch операции** для массовых действий
- **WebHook поддержка** для событий

### 🏢 Интеграция с DaData
- **Проверка контрагентов по ИНН** - получение данных компаний
- **Валидация адресов** - стандартизация адресной информации
- **Банковские реквизиты** - проверка БИК и счетов
- **Автоматическое обогащение** CRM данных

### 🔄 Дедупликация и очистка
- **Поиск дублей компаний** по ИНН, названию, телефону
- **Автоматическое слияние** дублирующихся записей
- **Telegram бот** для управления процессом
- **Настраиваемые правила** дедупликации

### 📚 База знаний
- **Статьи и гайды** по настройке Bitrix24
- **Примеры кода** для разработчиков
- **Best practices** интеграций
- **Готовые решения** для типовых задач

## 🛠 Технический стек

### Core
- **TypeScript** - основной язык разработки
- **Node.js** - серверная среда
- **Python** - для специфических интеграций

### Integrations
- **Bitrix24 REST API** - основная интеграция
- **DaData API** - обогащение данных
- **Telegram Bot API** - управление через бот
- **Redis** - кэширование запросов

### Infrastructure
- **Docker** - контейнеризация
- **GitHub Actions** - CI/CD
- **Vercel/Railway** - хостинг
- **PostgreSQL** - база данных

## 🚀 Быстрый старт

### 1. Установка
```bash
git clone https://github.com/EvaCoreBot/bitrix-integration-suite.git
cd bitrix-integration-suite
npm install
```

### 2. Настройка окружения
```bash
cp .env.example .env
# Заполните переменные окружения
```

### 3. Запуск
```bash
# Разработка
npm run dev

# Продакшен
npm run build
npm start
```

## ⚙️ Переменные окружения

### Bitrix24
| Переменная | Описание | Обязательная |
|------------|----------|--------------|
| `BITRIX_DOMAIN` | Домен Bitrix24 портала | ✅ |
| `BITRIX_CLIENT_ID` | ID приложения | ✅ |
| `BITRIX_CLIENT_SECRET` | Секрет приложения | ✅ |
| `BITRIX_ACCESS_TOKEN` | Токен доступа | ✅ |

### DaData
| Переменная | Описание | Обязательная |
|------------|----------|--------------|
| `DADATA_API_KEY` | API ключ DaData | ⚠️ |
| `DADATA_SECRET_KEY` | Секретный ключ | ⚠️ |

### Telegram
| Переменная | Описание | Обязательная |
|------------|----------|--------------|
| `TELEGRAM_BOT_TOKEN` | Токен бота для дедупликации | ⚠️ |
| `TELEGRAM_ADMIN_ID` | ID администратора | ⚠️ |

### Дополнительные
| Переменная | Описание | Обязательная |
|------------|----------|--------------|
| `DATABASE_URL` | URL базы данных | ❌ |
| `REDIS_URL` | URL Redis | ❌ |
| `LOG_LEVEL` | Уровень логирования | ❌ |

## 📁 Структура проекта

```
bitrix-integration-suite/
├── packages/
│   ├── api-client/        # TypeScript REST API клиент
│   │   ├── src/
│   │   │   ├── entities/  # CRM сущности
│   │   │   ├── methods/   # API методы
│   │   │   └── types/     # TypeScript типы
│   │   └── package.json
│   ├── dadata-integration/ # DaData интеграция
│   │   ├── src/
│   │   │   ├── services/  # Сервисы интеграции
│   │   │   └── utils/     # Утилиты
│   │   └── requirements.txt
│   └── dedupe-bot/        # Telegram бот дедупликации
│       ├── src/
│       │   ├── handlers/  # Обработчики команд
│       │   └── services/  # Бизнес-логика
│       └── requirements.txt
├── docs/                  # Документация
│   ├── api/              # API документация
│   ├── guides/           # Руководства
│   └── examples/         # Примеры кода
├── knowledge-base/        # База знаний
│   ├── articles/         # Статьи
│   ├── solutions/        # Готовые решения
│   └── best-practices/   # Лучшие практики
├── examples/             # Примеры использования
├── tests/                # Тесты
└── scripts/              # Служебные скрипты
```

## 🎯 Использование

### REST API Клиент
```typescript
import { BitrixClient } from '@bitrix-suite/api-client';

const client = new BitrixClient({
  domain: 'your-portal.bitrix24.ru',
  accessToken: 'your-access-token'
});

// Получение списка лидов
const leads = await client.crm.lead.list({
  select: ['ID', 'TITLE', 'STATUS_ID'],
  filter: { 'STATUS_ID': 'NEW' }
});

// Создание компании
const company = await client.crm.company.add({
  fields: {
    TITLE: 'ООО "Рога и копыта"',
    PHONE: [{ VALUE: '+7 (495) 123-45-67', VALUE_TYPE: 'WORK' }]
  }
});
```

### DaData интеграция
```python
from bitrix_suite.dadata import DaDataService

service = DaDataService(api_key='your-api-key')

# Проверка компании по ИНН
company_info = await service.find_by_inn('7707083893')

# Обогащение записи в Bitrix24
await service.enrich_company(company_id=123, inn='7707083893')
```

### Дедупликация через Telegram
1. Запустите бота: `/start`
2. Выберите тип дедупликации: `/dedupe_companies`
3. Настройте правила: `/settings`
4. Запустите процесс: `/run_dedupe`

## 🧪 Тестирование

```bash
# Все тесты
npm test

# Тесты с покрытием
npm run test:coverage

# Интеграционные тесты
npm run test:integration

# Линтинг
npm run lint
```

## 📚 Документация

### Основная документация
- [Руководство пользователя](docs/user-guide.md)
- [API Reference](docs/api/README.md)
- [Примеры интеграций](docs/examples/README.md)

### База знаний
- [Настройка Bitrix24](knowledge-base/articles/setup.md)
- [REST API гайды](knowledge-base/articles/rest-api.md)
- [Готовые решения](knowledge-base/solutions/README.md)
- [Лучшие практики](knowledge-base/best-practices/README.md)

## 🚀 Деплой

### Docker
```bash
docker build -t bitrix-suite .
docker run -p 3000:3000 bitrix-suite
```

### Vercel
```bash
npm run deploy:vercel
```

### Railway
```bash
npm run deploy:railway
```

## 🤝 Участие в разработке

1. Форкните репозиторий
2. Создайте ветку (`git checkout -b feature/new-integration`)
3. Внесите изменения и добавьте тесты
4. Зафиксируйте (`git commit -am 'Add new integration'`)
5. Отправьте (`git push origin feature/new-integration`)
6. Создайте Pull Request

## 📄 Лицензия

MIT License - см. файл [LICENSE](LICENSE)

## 🆘 Поддержка

- 📧 Email: support@evacorebot.com
- 💬 Telegram: [@BitrixIntegrationBot](https://t.me/BitrixIntegrationBot)
- 🐛 Issues: [GitHub Issues](https://github.com/EvaCoreBot/bitrix-integration-suite/issues)
- 📖 Wiki: [GitHub Wiki](https://github.com/EvaCoreBot/bitrix-integration-suite/wiki)

## 🏆 Авторы

- **EvaCoreBot Team** - *Основная разработка*
- **Community Contributors** - *Вклад и улучшения*

## 📈 Статистика

- ⭐ **4 проекта объединено** в один
- 🚀 **Полная экосистема** для Bitrix24
- 📦 **Монорепозиторий** с пакетами
- 🔧 **TypeScript + Python** решения
- 📚 **Обширная база знаний** включена

## 🎁 Дополнительные возможности

### 🔄 Автоматизация
- **Webhook обработчики** для событий Bitrix24
- **Scheduled jobs** для регулярных задач
- **Batch операции** для массовых изменений

### 📊 Аналитика
- **Отчеты по использованию** API
- **Мониторинг интеграций** в реальном времени
- **Алерты** при ошибках

### 🛡️ Безопасность
- **OAuth 2.0** аутентификация
- **Rate limiting** для API запросов
- **Валидация данных** на всех уровнях

---

**Bitrix Integration Suite** - всё для работы с Bitrix24 в одном месте! 🏢🚀

