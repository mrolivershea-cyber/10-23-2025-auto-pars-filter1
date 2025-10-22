# 🚀 CONNEXA - Универсальная Установка

## 📋 О скрипте

`universal_install.sh` - это полностью автоматический установочный скрипт, который:

✅ **Клонирует репозиторий** с GitHub  
✅ **Устанавливает все зависимости** (Python, Node.js, системные пакеты)  
✅ **Настраивает окружение** (PPTP, Supervisor, базу данных)  
✅ **Запускает сервисы** (Backend FastAPI + Frontend React)  
✅ **Проводит поэтапное тестирование** после каждого шага  
✅ **Создаёт админ-пользователя** (admin/admin)  

---

## 🎯 Быстрая установка (одна команда)

### На новом чистом сервере:

```bash
sudo curl -sSL https://raw.githubusercontent.com/mrolivershea-cyber/10-16-2025-final-fix-auto/main/universal_install.sh | sudo bash
```

### Или скачать и запустить:

```bash
# Скачать скрипт
wget https://raw.githubusercontent.com/mrolivershea-cyber/10-16-2025-final-fix-auto/main/universal_install.sh

# Дать права на выполнение
chmod +x universal_install.sh

# Запустить установку
sudo ./universal_install.sh
```

---

## 📦 Что делает скрипт?

### Шаг 1: Системные пакеты
- Python 3, pip, venv
- pptp-linux, ppp (для VPN туннелей)
- SQLite3 (база данных)
- Git, curl, wget
- Supervisor (управление процессами)
- Сетевые утилиты (iptables, net-tools)

**Тесты после шага:**
- ✅ Python3 установлен
- ✅ pip установлен
- ✅ pppd установлен
- ✅ git установлен
- ✅ supervisor установлен

### Шаг 2: Node.js и Yarn
- Node.js версии 18.x
- Yarn package manager

**Тесты после шага:**
- ✅ Node.js версия >= 18
- ✅ Yarn доступен

### Шаг 3: Клонирование репозитория
- Клонирование из GitHub: `https://github.com/mrolivershea-cyber/10-16-2025-final-fix-auto.git`
- Установка в `/app`
- Если `/app` уже существует - создаётся бэкап

**Тесты после шага:**
- ✅ backend директория существует
- ✅ frontend директория существует
- ✅ requirements.txt существует
- ✅ package.json существует

### Шаг 4-5: PPTP настройка
- Создание `/dev/ppp` устройства
- Настройка конфигурации PPTP в `/etc/ppp/`

**Тесты после шага:**
- ✅ /dev/ppp существует
- ✅ /dev/ppp доступен для записи
- ✅ PPTP config создан

### Шаг 6: Python зависимости
- Создание виртуального окружения
- Установка всех пакетов из `requirements.txt`
- FastAPI, SQLAlchemy, uvicorn, и др.

**Тесты после шага:**
- ✅ Virtual environment активирован
- ✅ FastAPI установлен
- ✅ SQLAlchemy установлен
- ✅ uvicorn установлен

### Шаг 7: Frontend зависимости
- Установка всех пакетов через Yarn
- React, React Router, и др.

**Тесты после шага:**
- ✅ node_modules создан
- ✅ React установлен

### Шаг 8: Проверка .env файлов
- Проверка существующих `.env`
- Создание базовых `.env` если отсутствуют
- Генерация SECRET_KEY

**Тесты после шага:**
- ✅ Backend .env существует
- ✅ Frontend .env существует

### Шаг 9: Инициализация базы данных
- Создание SQLite базы `connexa.db`
- Создание всех таблиц
- Создание админ-пользователя (admin/admin)

**Тесты после шага:**
- ✅ База данных создана
- ✅ База данных доступна для записи
- ✅ Таблица users существует

### Шаг 10: Настройка Supervisor
- Создание конфигурации для backend
- Создание конфигурации для frontend
- Регистрация сервисов в Supervisor

**Тесты после шага:**
- ✅ Backend supervisor config создан
- ✅ Frontend supervisor config создан

### Шаг 11: Запуск сервисов
- Запуск backend (FastAPI на порту 8001)
- Запуск frontend (React на порту 3000)
- Ожидание 30 секунд для инициализации

**Тесты после шага:**
- ✅ Backend процесс запущен
- ✅ Frontend процесс запущен
- ✅ Backend слушает порт 8001
- ✅ Frontend слушает порт 3000

### Шаг 12: Финальное тестирование API
- Проверка `/api/stats` endpoint
- Тестирование логина admin/admin
- Проверка доступности frontend

**Тесты после шага:**
- ✅ GET /api/stats работает
- ✅ Логин admin/admin работает
- ✅ Frontend отвечает

---

## 💻 Системные требования

- **ОС:** Ubuntu 20.04+ / Debian 10+
- **RAM:** Минимум 1GB (рекомендуется 2GB)
- **Диск:** Минимум 2GB свободного места
- **Права:** Root доступ (sudo)
- **Сеть:** Доступ к интернету для скачивания зависимостей

---

## 🎯 После установки

### 1. Откройте админку

```
http://ВАШ_IP:3000
```

### 2. Войдите в систему

```
Username: admin
Password: admin
```

### 3. Импортируйте узлы

Нажмите кнопку **"Import"** и вставьте список узлов в одном из форматов:

**Формат 7 (IP:Login:Pass):**
```
5.78.10.1:admin:password1
5.78.10.2:admin:password2
5.78.10.3:admin:password3
```

**Формат 4 (полный с локацией):**
```
123.45.67.89:admin:pass123:US:New York:10001
```

### 4. Запустите тесты

1. Выберите узлы из таблицы (checkbox)
2. Нажмите **"Testing"**
3. Выберите тип теста:
   - **Ping Only** - быстрая проверка доступности (PING LIGHT)
   - **Speed Only** - полная проверка скорости
   - **Both** - оба теста

### 5. Запустите SOCKS прокси

1. Выберите узлы со статусом `ping_ok` или `speed_ok`
2. Нажмите **"Start Services"**
3. Подождите 10-20 секунд для создания PPTP туннелей
4. Нажмите **"SOCKS"** → **"Открыть текстовый файл"**
5. Скопируйте список прокси

---

## 🔧 Полезные команды

### Проверить статус сервисов
```bash
sudo supervisorctl status
```

### Перезапустить backend
```bash
sudo supervisorctl restart backend
```

### Перезапустить frontend
```bash
sudo supervisorctl restart frontend
```

### Перезапустить всё
```bash
sudo supervisorctl restart all
```

### Посмотреть логи backend
```bash
tail -f /var/log/supervisor/backend.err.log
```

### Посмотреть логи frontend
```bash
tail -f /var/log/supervisor/frontend.err.log
```

### Обновить из GitHub
```bash
cd /app
git pull origin main
sudo supervisorctl restart all
```

### Проверить базу данных
```bash
sqlite3 /app/backend/connexa.db "SELECT * FROM users;"
```

### Пересоздать админа
```bash
cd /app/backend
source venv/bin/activate
python3 -c "
from database import SessionLocal
from models import User
from auth import hash_password

db = SessionLocal()
admin = db.query(User).filter(User.username == 'admin').first()

if admin:
    admin.password = hash_password('admin')
else:
    admin = User(username='admin', password=hash_password('admin'))
    db.add(admin)

db.commit()
print('✅ Admin пароль сброшен на: admin')
"
deactivate
```

---

## 🐛 Устранение неполадок

### Backend не запускается

1. Проверьте логи:
```bash
tail -100 /var/log/supervisor/backend.err.log
```

2. Попробуйте запустить вручную:
```bash
cd /app/backend
source venv/bin/activate
uvicorn server:app --host 0.0.0.0 --port 8001
```

3. Проверьте зависимости:
```bash
cd /app/backend
source venv/bin/activate
pip install -r requirements.txt
```

### Frontend не запускается

1. Проверьте логи:
```bash
tail -100 /var/log/supervisor/frontend.err.log
```

2. Переустановите зависимости:
```bash
cd /app/frontend
rm -rf node_modules
yarn install
sudo supervisorctl restart frontend
```

### PPTP туннели не работают

1. Проверьте `/dev/ppp`:
```bash
ls -la /dev/ppp
```

2. Если Docker контейнер, добавьте capability:
```bash
docker run --cap-add=NET_ADMIN ...
```

3. Проверьте логи PPTP:
```bash
cat /tmp/pptp_node_*.log
```

### Не могу войти admin/admin

1. Пересоздайте админа (см. команду выше)

2. Или проверьте наличие пользователя:
```bash
sqlite3 /app/backend/connexa.db "SELECT * FROM users WHERE username='admin';"
```

### База данных пустая / таблицы не созданы

```bash
cd /app/backend
source venv/bin/activate
python3 -c "from database import Base, engine; Base.metadata.create_all(bind=engine); print('✅ Таблицы созданы')"
```

---

## 📊 Формат прокси

После запуска SOCKS, прокси доступны в формате:

```
your-domain.com:1083:socks_2:PASSWORD
your-domain.com:1084:socks_3:PASSWORD
your-domain.com:1086:socks_5:PASSWORD
```

### Использование прокси

**cURL:**
```bash
curl -x socks5://socks_2:PASSWORD@your-domain.com:1083 https://ifconfig.me
```

**Python requests:**
```python
import requests

proxies = {
    'http': 'socks5://socks_2:PASSWORD@your-domain.com:1083',
    'https': 'socks5://socks_2:PASSWORD@your-domain.com:1083'
}

response = requests.get('https://ifconfig.me', proxies=proxies)
print(response.text)
```

---

## 📁 Структура проекта

```
/app/
├── backend/
│   ├── venv/                    # Python виртуальное окружение
│   ├── server.py                # FastAPI приложение
│   ├── database.py              # SQLAlchemy models
│   ├── auth.py                  # Аутентификация
│   ├── pptp_tunnel_manager.py   # PPTP управление
│   ├── socks_server.py          # SOCKS5 прокси сервер
│   ├── requirements.txt         # Python зависимости
│   ├── connexa.db               # SQLite база данных
│   └── .env                     # Переменные окружения
│
├── frontend/
│   ├── node_modules/            # Node.js зависимости
│   ├── src/
│   │   ├── App.js               # Главный компонент
│   │   ├── components/          # React компоненты
│   │   └── contexts/            # React контексты
│   ├── package.json             # Node.js зависимости
│   └── .env                     # Frontend переменные
│
└── universal_install.sh         # Этот скрипт установки
```

---

## 🔐 Безопасность

⚠️ **ВАЖНО:** После установки:

1. **Смените пароль админа:**
   - Войдите как admin/admin
   - Перейдите в настройки профиля
   - Измените пароль на надёжный

2. **Обновите ADMIN_SERVER_IP:**
   ```bash
   nano /app/backend/.env
   ```
   Измените `ADMIN_SERVER_IP=localhost` на ваш реальный домен/IP

3. **Используйте HTTPS:**
   - Настройте Nginx как reverse proxy
   - Установите SSL сертификат (Let's Encrypt)

4. **Ограничьте доступ:**
   - Настройте файрвол (ufw/iptables)
   - Разрешите только необходимые порты

---

## 📞 Поддержка

Если возникли проблемы:

1. Проверьте логи (см. раздел "Полезные команды")
2. Убедитесь что все тесты пройдены (скрипт показывает результаты)
3. Попробуйте переустановить компонент вручную

---

## 📝 Changelog

### v2.0 (Текущая версия)
- ✅ Полностью автоматическая установка с GitHub
- ✅ Поэтапное тестирование (12 этапов, 30+ тестов)
- ✅ Автоматическое создание админа
- ✅ Умная обработка существующих файлов
- ✅ Детальная отчётность об ошибках
- ✅ Цветной вывод для удобства

---

## 🎉 Готово!

После успешной установки система готова к использованию. Откройте админку и начните работу с PPTP/SOCKS5 прокси!

**Приятной работы! 🚀**
