# Скрипт бекапу логів

## 1. Створення файлу скрипта

```bash
cd ~
mkdir -p scripts && cd scripts
nano backup.sh
```

## 2. Код скрипта

```bash
#!/bin/bash

# ==============================================================================
# Скрипт для автоматичного створення резервних копій (бекапу) логів
# Використання: ./backup.sh <каталог_логів> <каталог_бекапів>
# ==============================================================================

# Шлях до файлу блокування (захист від паралельного запуску)
LOCK_FILE="/tmp/backup.lock"

# --- Крок 1: Перевірка аргументів ---
# Перевіряємо, чи передано рівно 2 аргументи
if [ "$#" -ne 2 ]; then
    echo "Usage: ./backup.sh <log_dir> <backup_dir>"
    exit 1
fi

LOG_DIR=$1
BACKUP_DIR=$2

# Перевіряємо, чи є перший аргумент існуючим каталогом
if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Log directory '$LOG_DIR' does not exist."
    echo "Usage: ./backup.sh <log_dir> <backup_dir>"
    exit 1
fi

# Перевіряємо, чи є другий аргумент існуючим каталогом
if [ ! -d "$BACKUP_DIR" ]; then
    echo "Error: Backup directory '$BACKUP_DIR' does not exist."
    echo "Usage: ./backup.sh <log_dir> <backup_dir>"
    exit 1
fi

# --- Крок 2: Захист від паралельного запуску ---
# Якщо lock-файл вже існує, завершуємо роботу, щоб уникнути конфліктів
if [ -f "$LOCK_FILE" ]; then
    echo "Backup already running"
    exit 1
fi

# Створюємо lock-файл (фіксуємо, що процес бекапу почався)
touch "$LOCK_FILE"

# Гарантуємо видалення lock-файлу при будь-якому завершенні скрипта (навіть при помилці чи Ctrl+C)
trap 'rm -f "$LOCK_FILE"' EXIT

# --- Крок 3: Створення архіву логів ---
# Формуємо ім'я файлу з поточною датою та часом
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M")
ARCHIVE_NAME="logs_backup_${TIMESTAMP}.tar.gz"
FULL_BACKUP_PATH="${BACKUP_DIR}/${ARCHIVE_NAME}"

# Створюємо стиснений архів tar.gz
# Флаг -C дозволяє перейти в каталог логів, щоб в архіві не зберігалися повні абсолютні шляхи
tar -czf "$FULL_BACKUP_PATH" -C "$LOG_DIR" .

# --- Крок 4: Перевірка результату архівації ---
if [ $? -eq 0 ]; then
    echo "Backup created: $FULL_BACKUP_PATH"
    exit 0
else
    echo "Backup failed"
    exit 2
fi
```

## 3. Надання дозволу скрипту на виконання

```bash
chmod +x backup.sh
```

## 4. Створення тестової папки та файлів для перевірки

```bash
$ mkdir -p ~/test_logs ~/test_backups
$ echo "log data 1" > ~/test_logs/app.log
$ echo "log data 2" > ~/test_logs/error.log
```

## 5. Перевірка на помилки

```bash
# Запуск скрипту без аргументів
$ ./backup.sh
# Скрипт миттєво завершився
Usage: ./backup.sh <log_dir> <backup_dir>

# Запуск скрипту з вигаданими папками
$ ./backup.sh /wrong/path1 /wrong/path2
# Скрипт вказує, що директорії не існує
Error: Log directory '/wrong/path1' does not exist.
Usage: ./backup.sh <log_dir> <backup_dir>
```

## 6. Створення бекапу (запуск з реальними тестовими папками)

```bash
# Введення
$ ./backup.sh ~/test_logs ~/test_backups
# Виведення
Backup created: /home/ernest/test_backups/logs_backup_2026-06-16_12-45.tar.gz
```

## 7. Перевірка захисту від паралельного запуску (`Lock-файл`)

```bash
# Створюємо файл блокування для симуляції ситуації, ніби бекап уже робиться в іншому вікні
$ touch /tmp/backup.lock

# Знову запускаємо правильний бекап
$ ./backup.sh ~/test_logs ~/test_backups

# Скрипт блокує роботу
Backup already running

# Видаляємо файл, щоб скрипт знову міг працювати
$ rm /tmp/backup.lock
```