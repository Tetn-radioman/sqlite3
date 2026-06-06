
```markdown

# SQLite3 — краткое руководство

## Установка

```bash
# Установка на Ubuntu/Debian
sudo apt update && sudo apt install sqlite3 sqlitebrowser -y

# Для разработки (заголовочные файлы)
sudo apt install libsqlite3-dev -y
```

## Основные команды

### Запуск и работа с базой

```bash
sqlite3 mybase.db          # Создать/открыть БД
.exit                      # Выйти из SQLite
.quit                      # Альтернативный выход
.tables                    # Показать все таблицы
.schema                    # Показать структуру всех таблиц
.schema table_name         # Показать структуру конкретной таблицы
.databases                 # Показать путь к открытым БД
```

### Работа с таблицами

```sql
-- Создать таблицу
CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER);

-- Вставить данные
INSERT INTO users (name, age) VALUES ('Анна', 25);
INSERT INTO users (name, age) VALUES ('Макс', 30);

-- Выбрать данные
SELECT * FROM users;                      -- всё
SELECT name, age FROM users WHERE age > 26;   -- с условием

-- Обновить данные
UPDATE users SET age = 26 WHERE name = 'Анна';

-- Удалить данные
DELETE FROM users WHERE name = 'Макс';

-- Удалить таблицу полностью
DROP TABLE users;
```

### Экспорт и импорт

```bash
# Экспорт всей БД в SQL-файл (из терминала)
sqlite3 mybase.db .dump > backup.sql

# Импорт из SQL-файла
sqlite3 mybase.db < backup.sql

# Экспорт таблицы в CSV
sqlite3 -csv mybase.db "SELECT * FROM users;" > users.csv
```

## 🔍 Полезные примеры

```sql
-- Создать таблицу с автоинкрементом
CREATE TABLE games (id INTEGER PRIMARY KEY AUTOINCREMENT, score INTEGER, date TEXT);

-- Вставить дату автоматически
INSERT INTO games (score, date) VALUES (100, datetime('now'));

-- Выбрать последние 5 записей
SELECT * FROM games ORDER BY id DESC LIMIT 5;

-- Посчитать количество записей
SELECT COUNT(*) FROM games;

-- Среднее значение
SELECT AVG(score) FROM games;
```

## 🗑️ Удаление БД

```bash
rm mybase.db
```

---

*SQLite хранит всю БД в одном файле. Можете скопировать его и открыть на другом компьютере.*
```
