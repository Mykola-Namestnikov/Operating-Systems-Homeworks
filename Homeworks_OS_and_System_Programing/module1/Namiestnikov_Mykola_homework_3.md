# Завдання 1. Огляд активних процесів

## 1. Виведення списку усіх процесів у системі

```bash
# Введення
$ ps aux
# Виведення
      PID    PPID    PGID     WINPID   TTY         UID    STIME COMMAND
       91      69      91      18240  pty0      197609 02:35:39 /usr/bin/ps
       69      68      69      19896  pty0      197609 02:35:28 /usr/bin/bash
       68       1      68      15908  ?         197609 02:35:28 /usr/bin/mintty
```

## 2. Інтерактивний монітор `top`

```bash
# Введення
$ top
# Виведення
21348 opera
```

## 3. Знаходження PID процесу поточної оболонки

```bash
# Введення
$ echo $$
# Виведення
69
```

# Завдання 2. Робота у фоні та керування процесами

## 1. Запуск довгої команди у фоновому режимі

```bash
# Введення
$ sleep 1000 &
# Виведення
[1] 112
```

## 2. Перевірка списку фонових завдань

```bash
# Введення
$ jobs
# Виведення
[1]+  Running                 sleep 1000 &
```

## 3. Повернення процесу з фону на передній план

```bash
# Введення
$ fg %1
# Виведення
sleep 1000
# Ctrl + Z
[1]+  Stopped                 sleep 1000
```

## 4. Примусове завершення процесу за допомогою `kill`

```bash
# Введення
$ kill -9 112
# Виведення
[1]+  Killed                  sleep 1000
```

## 5. Запуск команди за допомогою nohup, щоб вона працювала після закриття терміналу

```bash
# Введення
$ nohup sleep 2000 &
# Виведення
[1] 128
nohup: ignoring input and appending output to 'nohup.out'
```

# Завдання 3. Пріоритети та обмеження

## 1. Запуск нової команди з підвищеним значенням nice (нижчим пріоритетом)

```bash
# Введення
$ nice -n 10 sleep 500 &
# Виведення
[2] 132
```

## 2. Зміна пріоритету вже запущеного процесу (renice)

```bash
$ pidof sleep
$ renice -n 15 -p 132
```

## 3. Перегляд поточних обмежень ресурсів користувача

```bash
# Введення
$ ulimit -a
# Виведення
core file size              (blocks, -c) 0
data seg size               (kbytes, -d) unlimited
file size                   (blocks, -f) unlimited
open files                          (-n) 3200
pipe size                (512 bytes, -p) 8
stack size                  (kbytes, -s) 2032
cpu time                   (seconds, -t) unlimited
max user processes                  (-u) 256
virtual memory              (kbytes, -v) unlimited
```

# Завдання 4. Моніторинг ресурсів

## 1. Виведення інформації про використання дискового простору

```bash
# Введення
$ df -h
# Виведення
Filesystem      Size  Used Avail Use% Mounted on
D:/Git          318G  205G  113G  65% /
C:              159G   94G   66G  59% /c

```

## 2. Відображення обсягу вільної та використаної оперативної пам'яті

```bash
# Введення
$ free -h
# Виведення
TotalVisibleMemorySize FreePhysicalMemory
---------------------- ------------------
              14459592            3893580


[2]+  Done                    nice -n 10 sleep 500
```