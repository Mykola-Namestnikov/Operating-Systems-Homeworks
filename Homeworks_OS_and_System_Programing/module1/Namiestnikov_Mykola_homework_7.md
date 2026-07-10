## Аналіз життєвого циклу контейнера

## 1. Запуск контейнера

Для аналізу було обрано легковаговий веб-сервер `Nginx` на базі дистрибутиву Alpine Linux.

**Виконана команда запуску:**

```bash
# Введення
$ sudo docker run -d --name my_web_app -p 8080:80 nginx:alpine
# Виведення
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
de1b677d8c00: Pull complete
6a0ac1617861: Pull complete
a5008f4a4b25: Pull complete
43f834d60d8a: Pull complete
fbaed3f7fcbe: Pull complete
94d083cf706a: Pull complete
e654dbbbb9e1: Pull complete
abaae85d1626: Pull complete
ab556c9e4280: Download complete
2d8223aa4623: Download complete
Digest: sha256:8b1e78743a03dbb2c95171cc58639fef29abc8816598e27fb910ed2e621e589a
Status: Downloaded newer image for nginx:alpine
5b968309a4444867e08d57074ffdcd68edbe3fba504459ce01b9e6e585005bdc
```

* Флаг `-d` (detached) запускає контейнер у фоновому режимі як демона.
* `--name my_web_app` задає зрозуміле ім'я для ідентифікації.
* `-p 8080:80` налаштовує Port Mapping (прокидає порт 8080 хост-машини на порт 80 всередині ізольованого контейнера).

## 2. Аналіз процесів усередині контейнера (PID 1)

Для перегляду дерева процесів всередині ізольованого простору імен (PID namespace) було виконано команду:

```bash
# Введення
$ sudo docker exec -it my_web_app ps aux
# Виведення
PID   USER     TIME  COMMAND
    1 root      0:00 nginx: master process nginx -g daemon off;
   30 nginx     0:00 nginx: worker process
   31 nginx     0:00 nginx: worker process
   32 nginx     0:00 nginx: worker process
   33 nginx     0:00 nginx: worker process
   34 nginx     0:00 nginx: worker process
   35 nginx     0:00 nginx: worker process
   36 nginx     0:00 nginx: worker process
   37 nginx     0:00 nginx: worker process
   38 nginx     0:00 nginx: worker process
   39 nginx     0:00 nginx: worker process
   40 nginx     0:00 nginx: worker process
   41 nginx     0:00 nginx: worker process
   42 root      0:00 ps aux
```

* Процесом PID 1 всередині контейнера є головний майстер-процес веб-сервера (`nginx: master process`).
* В архітектурі контейнеризації Docker контейнер не є повноцінною ОС із власним важким ядром чи класичною системою ініціалізації на кшталт `systemd` (PID 1 у звичайному Linux). Контейнер — це лише ізольована група процесів. Відповідно, той бінарний файл, який прописаний в інструкції `ENTRYPOINT` або `CMD` всередині Dockerfile, автоматично стає першим процесом (PID 1). Він бере на себе роль "ініціатора" середовища та відповідає за керування дочірніми процесами (worker processes).

## 3. Логування роботи програми

**Виконана команда перегляду логів:**

```bash
# Введення
$ sudo docker logs my_web_app
# Виведення
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/06/16 16:13:02 [notice] 1#1: using the "epoll" event method
2026/06/16 16:13:02 [notice] 1#1: nginx/1.31.1
2026/06/16 16:13:02 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0)
2026/06/16 16:13:02 [notice] 1#1: OS: Linux 6.18.33.1-microsoft-standard-WSL2
2026/06/16 16:13:02 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1024:1048576
2026/06/16 16:13:02 [notice] 1#1: start worker processes
2026/06/16 16:13:02 [notice] 1#1: start worker process 30
2026/06/16 16:13:02 [notice] 1#1: start worker process 31
2026/06/16 16:13:02 [notice] 1#1: start worker process 32
2026/06/16 16:13:02 [notice] 1#1: start worker process 33
2026/06/16 16:13:02 [notice] 1#1: start worker process 34
2026/06/16 16:13:02 [notice] 1#1: start worker process 35
2026/06/16 16:13:02 [notice] 1#1: start worker process 36
2026/06/16 16:13:02 [notice] 1#1: start worker process 37
2026/06/16 16:13:02 [notice] 1#1: start worker process 38
2026/06/16 16:13:02 [notice] 1#1: start worker process 39
2026/06/16 16:13:02 [notice] 1#1: start worker process 40
2026/06/16 16:13:02 [notice] 1#1: start worker process 41
```

* У контейнеризованих додатках логування реалізовано за принципом **Twelve-Factor App**. Застосунок не пише логи у файли (як було реалізовано в 4-й домашній роботі через `>> timestamp.log`). Натомість, головний процес виводить усю діагностику безпосередньо в стандартні потоки виведення: `stdout` (стандартний вивід) та `stderr` (потік помилок).
* Контейнерний рушій (Docker Engine) перехоплює ці потоки `stdout/stderr` від процесу PID 1 і записує їх у спеціальні JSON-файли на хост-системі (за замовчуванням у папку `/var/lib/docker/containers/...`). Команда `docker logs` просто читає цей локальний файл та виводить його вміст на екран користувача.

## 4. Завершення роботи контейнера

**Виконана команда зупинки:**

```bash
# Введення
$ sudo docker stop my_web_app
# Виведення
my_web_app
```

* Коли виконується команда `docker stop`, демон Docker надсилає процесу з PID 1 (нашому майстер-процесу Nginx) сигнал `SIGTERM` (Signal 15, Termination). Це є сигналом для "м'якої" (graceful) зупинки: процес починає закривати активні мережеві з'єднання, скидати кеш на диск та завершувати дочірні воркери.
* Час життя контейнера жорстко прив'язаний до життєвого циклу його процесу PID 1. Як тільки головний процес завершує роботу, контейнер миттєво переходить у статус `Exited`.
* Якщо процес PID 1 зависає, ігнорує `SIGTERM` або розроблений некоректно (не вміє обробляти сигнали системи), Docker чекає стандартний таймаут (за замовчуванням 10 секунд). Після закінчення цього часу Docker Engine надсилає на рівні ядра жорсткий сигнал `SIGKILL` (Signal 9). Цей сигнал неможливо перехопити або проігнорувати — ядро Linux примусово та миттєво знищує процес у пам'яті, що може призвести до пошкодження даних.

## Логічні висновки:
Контейнер — це не віртуальна машина, а ізольований на рівні ядра Linux процес хост-системи. Його існування цілком і повністю підпорядковане статусу процесу **PID 1**: якщо додаток усередині падає або завершує виконання, ізольований простір імен знищується, а контейнер зупиняється.