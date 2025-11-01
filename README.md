# Django Shop Application

![Python](https://img.shields.io/badge/Python-3.9-3776AB?style=for-the-badge&logo=python&logoColor=white) ![Django](https://img.shields.io/badge/Django-5-092E20?style=for-the-badge&logo=django&logoColor=white) ![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

## Автор

**Розробник:** Сергій Щербаков
**Email:** sergiyscherbakov@ukr.net
**Telegram:** @s_help_2010

### 💰 Підтримати розробку
Задонатити на каву USDT (BINANCE SMART CHAIN):
**`0xDFD0A23d2FEd7c1ab8A0F9A4a1F8386832B6f95A`**

---

Навчальний проєкт інтернет-магазину на Django з базовою функціональністю управління товарами через адміністративну панель.

## Опис проєкту

**Shop Application** - це базовий веб-додаток для управління каталогом товарів інтернет-магазину. Проєкт демонструє основні можливості Django framework, включаючи роботу з моделями, міграціями бази даних, адміністративною панеллю та системою автентифікації.

### Основна функціональність

- **Модель Product** з атрибутами:
  - `name` - назва товару (CharField, max 100 символів)
  - `description` - опис товару (TextField, необов'язкове)
  - `price` - ціна (DecimalField, 10 цифр, 2 знаки після коми)
  - `available` - доступність (BooleanField, за замовчуванням True)

- **Адміністративна панель Django** для CRUD операцій над товарами
- **Система автентифікації** для доступу до адмін-панелі
- **База даних SQLite3** для зберігання даних
- **Система міграцій** для управління схемою БД

## Технологічний стек

- **Python 3.x**
- **Django 5.2.6** - веб-фреймворк
- **SQLite3** - база даних
- **Django Admin** - вбудована адміністративна панель

## Структура проєкту

```
django/
├── myproject/              # Головний Django проєкт
│   ├── myproject/         # Конфігураційна директорія
│   │   ├── settings.py    # Налаштування проєкту
│   │   ├── urls.py        # URL маршрути
│   │   ├── wsgi.py        # WSGI конфігурація
│   │   └── asgi.py        # ASGI конфігурація
│   ├── shop/              # Додаток магазину
│   │   ├── models.py      # Моделі (Product)
│   │   ├── admin.py       # Реєстрація моделей в адмін-панелі
│   │   ├── views.py       # Представлення
│   │   ├── tests.py       # Тести
│   │   └── migrations/    # Міграції БД
│   ├── manage.py          # Утиліта управління Django
│   └── db.sqlite3         # База даних (не в Git)
├── myenv/                 # Віртуальне середовище (не в Git)
├── .gitignore            # Файли для ігнорування Git
├── КОМАНДИ.txt           # Документація команд
└── README.md             # Цей файл
```

## Встановлення та налаштування

### Передумови

- Python 3.8 або вище
- pip (менеджер пакетів Python)
- Git

### Крок 1: Клонування репозиторію

```bash
git clone <repository-url>
cd django
```

### Крок 2: Створення віртуального середовища

**Windows:**
```bash
python -m venv myenv
myenv\Scripts\activate
```

**Linux/macOS:**
```bash
python3 -m venv myenv
source myenv/bin/activate
```

### Крок 3: Оновлення pip

```bash
python -m pip install --upgrade pip
```

### Крок 4: Встановлення залежностей

```bash
pip install django
```

Перевірка версії Django:
```bash
python -m django --version
# Має вивести: 5.2.6 (або схожу версію)
```

### Крок 5: Перехід до директорії проєкту

```bash
cd myproject
```

### Крок 6: Застосування міграцій бази даних

```bash
python manage.py migrate
```

Ця команда створить файл `db.sqlite3` та налаштує всі необхідні таблиці в базі даних.

### Крок 7: Створення суперкористувача

**Інтерактивний метод:**
```bash
python manage.py createsuperuser
```

Введіть:
- Username: `admin`
- Email: `zavulon602@gmail.com` (або ваш email)
- Password: `1234` (або складніший пароль)

**Автоматичний метод (однорядковий):**
```bash
python -c "import os; os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings'); import django; django.setup(); from django.contrib.auth import get_user_model; User = get_user_model(); User.objects.filter(username='admin').delete(); User.objects.create_superuser('admin','zavulon602@gmail.com','1234')"
```

## Запуск проєкту

### Запуск сервера розробки

```bash
python manage.py runserver
```

Сервер буде доступний за адресою: `http://127.0.0.1:8000/`

### Доступ до адміністративної панелі

1. Перейдіть за адресою: `http://127.0.0.1:8000/admin/`
2. Введіть облікові дані:
   - **Username:** `admin`
   - **Password:** `1234`

### Робота з товарами

В адмін-панелі ви можете:
- Переглядати список товарів
- Додавати нові товари
- Редагувати існуючі товари
- Видаляти товари
- Фільтрувати товари за доступністю

## Робота з базою даних

### Створення нових міграцій

Після внесення змін в `models.py`:

```bash
python manage.py makemigrations shop
```

### Застосування міграцій

```bash
python manage.py migrate
```

### Перегляд SQL коду міграції

```bash
python manage.py sqlmigrate shop 0001
```

### Скидання бази даних (розробка)

```bash
# Видалити db.sqlite3
del db.sqlite3  # Windows
rm db.sqlite3   # Linux/macOS

# Видалити файли міграцій (крім __init__.py)
# Потім повторити migrate та createsuperuser
```

## Розробка

### Додавання нових полів до моделі Product

1. Відредагуйте `myproject/shop/models.py`
2. Створіть міграцію: `python manage.py makemigrations`
3. Застосуйте міграцію: `python manage.py migrate`

### Налаштування відображення в адмін-панелі

Редагуйте файл `myproject/shop/admin.py`:

```python
from django.contrib import admin
from .models import Product

@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ('name', 'price', 'available')
    list_filter = ('available',)
    search_fields = ('name', 'description')
```

### Запуск тестів

```bash
python manage.py test shop
```

## Корисні команди

### Django shell

Інтерактивна консоль для роботи з моделями:

```bash
python manage.py shell
```

Приклад використання:
```python
from shop.models import Product

# Створити новий товар
product = Product.objects.create(
    name="Ноутбук",
    description="Потужний ноутбук для роботи",
    price=25000.00,
    available=True
)

# Отримати всі товари
products = Product.objects.all()

# Фільтрація
available_products = Product.objects.filter(available=True)
```

### Перевірка проєкту на помилки

```bash
python manage.py check
```

### Створення резервної копії БД

```bash
python manage.py dumpdata > backup.json
```

### Відновлення з резервної копії

```bash
python manage.py loaddata backup.json
```

## Вихід з віртуального середовища

```bash
deactivate
```

## Налаштування для production

> ⚠️ **ВАЖЛИВО:** Цей проєкт налаштований тільки для розробки!

Для production необхідно:

1. **Змінити SECRET_KEY** в `settings.py`
2. **Встановити DEBUG = False**
3. **Налаштувати ALLOWED_HOSTS**
4. **Використовувати PostgreSQL** замість SQLite
5. **Налаштувати статичні файли** (collectstatic)
6. **Використовувати gunicorn/uwsgi**
7. **Налаштувати HTTPS**
8. **Використовувати змінні оточення** для секретів

## Troubleshooting

### Помилка: "No module named django"

Переконайтесь, що віртуальне середовище активоване і Django встановлено:
```bash
pip install django
```

### Помилка: "You have unapplied migrations"

Виконайте:
```bash
python manage.py migrate
```

### Не можу увійти в адмін-панель

Створіть нового суперкористувача:
```bash
python manage.py createsuperuser
```

### Порт 8000 вже використовується

Запустіть на іншому порті:
```bash
python manage.py runserver 8080
```

## Подальший розвиток

Можливі напрямки розширення проєкту:

- [ ] Додати категорії товарів
- [ ] Реалізувати публічний каталог товарів
- [ ] Додати зображення товарів
- [ ] Реалізувати кошик покупок
- [ ] Додати систему замовлень
- [ ] Інтегрувати платіжну систему
- [ ] Додати відгуки та рейтинги
- [ ] Реалізувати пошук по товарам
- [ ] Додати API (Django REST Framework)
- [ ] Налаштувати email-сповіщення

## Ліцензія

Цей проєкт створено в освітніх цілях.
