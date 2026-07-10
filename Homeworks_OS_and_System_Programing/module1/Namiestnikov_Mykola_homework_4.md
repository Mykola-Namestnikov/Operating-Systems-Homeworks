# Завдання 1. Менеджери пакетів

## 1. Оновлення списку пакетів у системі

```bash
# Введення
$ sudo apt update
# Виведення
Get:1 http://security.ubuntu.com/ubuntu resolute-security InRelease [137 kB]
Get:2 http://archive.ubuntu.com/ubuntu resolute InRelease [136 kB]
Get:3 http://security.ubuntu.com/ubuntu resolute-security/main amd64 Packages [203 kB]
Get:4 http://archive.ubuntu.com/ubuntu resolute-updates InRelease [137 kB]
Get:5 http://security.ubuntu.com/ubuntu resolute-security/main Translation-en [54.8 kB]
Get:6 http://security.ubuntu.com/ubuntu resolute-security/main amd64 Components [31.1 kB]
Get:7 http://security.ubuntu.com/ubuntu resolute-security/main amd64 c-n-f Metadata [3332 B]
Get:8 http://security.ubuntu.com/ubuntu resolute-security/universe amd64 Packages [110 kB]
Get:9 http://security.ubuntu.com/ubuntu resolute-security/universe Translation-en [34.6 kB]
Get:10 http://security.ubuntu.com/ubuntu resolute-security/universe amd64 Components [42.9 kB]
Get:11 http://security.ubuntu.com/ubuntu resolute-security/universe amd64 c-n-f Metadata [2996 B]
Get:12 http://security.ubuntu.com/ubuntu resolute-security/restricted amd64 Packages [201 kB]
Get:13 http://archive.ubuntu.com/ubuntu resolute-backports InRelease [136 kB]
Get:14 http://archive.ubuntu.com/ubuntu resolute/main amd64 Packages [1480 kB]
Get:15 http://security.ubuntu.com/ubuntu resolute-security/restricted Translation-en [35.1 kB]
Get:16 http://security.ubuntu.com/ubuntu resolute-security/restricted amd64 c-n-f Metadata [396 B]
Get:17 http://security.ubuntu.com/ubuntu resolute-security/multiverse amd64 Components [212 B]
Get:18 http://security.ubuntu.com/ubuntu resolute-security/multiverse amd64 c-n-f Metadata [120 B]
Get:19 http://archive.ubuntu.com/ubuntu resolute/main Translation-en [524 kB]
Get:20 http://archive.ubuntu.com/ubuntu resolute/main amd64 Components [395 kB]
Get:21 http://archive.ubuntu.com/ubuntu resolute/main amd64 c-n-f Metadata [32.4 kB]
Get:22 http://archive.ubuntu.com/ubuntu resolute/universe amd64 Packages [16.0 MB]
Get:23 http://archive.ubuntu.com/ubuntu resolute/universe Translation-en [6329 kB]
Get:24 http://archive.ubuntu.com/ubuntu resolute/universe amd64 Components [4556 kB]
Get:25 http://archive.ubuntu.com/ubuntu resolute/universe amd64 c-n-f Metadata [313 kB]
Get:26 http://archive.ubuntu.com/ubuntu resolute/restricted amd64 Packages [152 kB]
Get:27 http://archive.ubuntu.com/ubuntu resolute/restricted Translation-en [25.8 kB]
Get:28 http://archive.ubuntu.com/ubuntu resolute/restricted amd64 Components [556 B]
Get:29 http://archive.ubuntu.com/ubuntu resolute/multiverse amd64 Packages [290 kB]
Get:30 http://archive.ubuntu.com/ubuntu resolute/multiverse Translation-en [127 kB]
Get:31 http://archive.ubuntu.com/ubuntu resolute/multiverse amd64 Components [50.0 kB]
Get:32 http://archive.ubuntu.com/ubuntu resolute/multiverse amd64 c-n-f Metadata [8276 B]
Get:33 http://archive.ubuntu.com/ubuntu resolute-updates/main amd64 Packages [213 kB]
Get:34 http://archive.ubuntu.com/ubuntu resolute-updates/main Translation-en [57.7 kB]
Get:35 http://archive.ubuntu.com/ubuntu resolute-updates/main amd64 Components [37.1 kB]
Get:36 http://archive.ubuntu.com/ubuntu resolute-updates/main amd64 c-n-f Metadata [3572 B]
Get:37 http://archive.ubuntu.com/ubuntu resolute-updates/universe amd64 Packages [119 kB]
Get:38 http://archive.ubuntu.com/ubuntu resolute-updates/universe Translation-en [37.9 kB]
Get:39 http://archive.ubuntu.com/ubuntu resolute-updates/universe amd64 Components [55.8 kB]
Get:40 http://archive.ubuntu.com/ubuntu resolute-updates/universe amd64 c-n-f Metadata [3220 B]
Get:41 http://archive.ubuntu.com/ubuntu resolute-updates/restricted amd64 Packages [201 kB]
Get:42 http://archive.ubuntu.com/ubuntu resolute-updates/restricted Translation-en [35.1 kB]
Get:43 http://archive.ubuntu.com/ubuntu resolute-updates/restricted amd64 c-n-f Metadata [392 B]
Get:44 http://archive.ubuntu.com/ubuntu resolute-updates/multiverse amd64 Packages [3328 B]
Get:45 http://archive.ubuntu.com/ubuntu resolute-updates/multiverse Translation-en [772 B]
Get:46 http://archive.ubuntu.com/ubuntu resolute-updates/multiverse amd64 Components [216 B]
Get:47 http://archive.ubuntu.com/ubuntu resolute-updates/multiverse amd64 c-n-f Metadata [256 B]
Get:48 http://archive.ubuntu.com/ubuntu resolute-backports/main amd64 Components [212 B]
Get:49 http://archive.ubuntu.com/ubuntu resolute-backports/main amd64 c-n-f Metadata [112 B]
Get:50 http://archive.ubuntu.com/ubuntu resolute-backports/universe amd64 Components [216 B]
Get:51 http://archive.ubuntu.com/ubuntu resolute-backports/universe amd64 c-n-f Metadata [116 B]
Get:52 http://archive.ubuntu.com/ubuntu resolute-backports/restricted amd64 Components [216 B]
Get:53 http://archive.ubuntu.com/ubuntu resolute-backports/restricted amd64 c-n-f Metadata [120 B]
Get:54 http://archive.ubuntu.com/ubuntu resolute-backports/multiverse amd64 Components [216 B]
Get:55 http://archive.ubuntu.com/ubuntu resolute-backports/multiverse amd64 c-n-f Metadata [120 B]
Fetched 32.3 MB in 26s (1244 kB/s)
38 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

## 2. Встановлення утиліти `tree`

```bash
# Введення
$ sudo apt install tree -y
# Виведення
Installing:
  tree

Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 38
  Download size: 53.5 kB
  Space needed: 125 kB / 1025 GB available

Get:1 http://archive.ubuntu.com/ubuntu resolute/universe amd64 tree amd64 2.3.1-1 [53.5 kB]
Fetched 53.5 kB in 0s (244 kB/s)
Selecting previously unselected package tree.
(Reading database ... 35923 files and directories currently installed.)
Preparing to unpack .../tree_2.3.1-1_amd64.deb ...
Unpacking tree (2.3.1-1) ...
Setting up tree (2.3.1-1) ...
Processing triggers for man-db (2.13.1-1build1) ...
```

## 3. Перевірка встановлення та версії пакету

```bash
# Введення
$ tree --version
# Виведення
tree v2.3.1 © 1996 - 2026 by Steve Baker, Thomas Moore, Francesc Rocher, Florian Sesser, Kyosuke Tokoro
```

## 4. Видалення встановленого пакета

```bash
# Введення
$ sudo apt remove tree -y
# Виведення
REMOVING:
  tree

Summary:
  Upgrading: 0, Installing: 0, Removing: 1, Not Upgrading: 38
  Freed space: 125 kB

(Reading database ... 35928 files and directories currently installed.)
Removing tree (2.3.1-1) ...
Processing triggers for man-db (2.13.1-1build1) ...
```

# Завдання 2. Керування сервісами через `systemctl`

## 1. Перевірка статусу сервісу `cron`

```bash
# Введення
$ sudo systemctl status cron
# Виведення
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Mon 2026-06-15 10:25:50 CEST; 15min ago
 Invocation: 6d44e8ae587346bc8ad478410dbab8e0
       Docs: man:cron(8)
   Main PID: 157 (cron)
      Tasks: 1 (limit: 8176)
     Memory: 408K (peak: 2.2M)
        CPU: 10ms
     CGroup: /system.slice/cron.service
             └─157 /usr/sbin/cron -f -P

Jun 15 10:25:50 DESKTOP-KF9NMIG systemd[1]: Started cron.service - Regular background program processing daemon.
Jun 15 10:25:50 DESKTOP-KF9NMIG (cron)[157]: cron.service: Referenced but unset environment variable evaluates to an em>
Jun 15 10:25:50 DESKTOP-KF9NMIG cron[157]: (CRON) INFO (pidfile fd = 3)
Jun 15 10:25:50 DESKTOP-KF9NMIG cron[157]: (CRON) INFO (Running @reboot jobs)
```

## 2. Зупинка сервісу та перевірка, що він не активний

```bash
# Введення
$ sudo systemctl stop cron
$ sudo systemctl status cron
# Виведення
○ cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: inactive (dead) since Mon 2026-06-15 10:43:25 CEST; 13s ago
   Duration: 17min 35.068s
 Invocation: 6d44e8ae587346bc8ad478410dbab8e0
       Docs: man:cron(8)
    Process: 157 ExecStart=/usr/sbin/cron -f -P $EXTRA_OPTS (code=killed, signal=TERM)
   Main PID: 157 (code=killed, signal=TERM)
   Mem peak: 2.2M
        CPU: 10ms

Jun 15 10:25:50 DESKTOP-KF9NMIG systemd[1]: Started cron.service - Regular background program processing daemon.
Jun 15 10:25:50 DESKTOP-KF9NMIG (cron)[157]: cron.service: Referenced but unset environment variable evaluates to an em>
Jun 15 10:25:50 DESKTOP-KF9NMIG cron[157]: (CRON) INFO (pidfile fd = 3)
Jun 15 10:25:50 DESKTOP-KF9NMIG cron[157]: (CRON) INFO (Running @reboot jobs)
Jun 15 10:43:25 DESKTOP-KF9NMIG systemd[1]: Stopping cron.service - Regular background program processing daemon...
Jun 15 10:43:25 DESKTOP-KF9NMIG systemd[1]: cron.service: Deactivated successfully.
Jun 15 10:43:25 DESKTOP-KF9NMIG systemd[1]: Stopped cron.service - Regular background program processing daemon.
```

## 3. Повторний запуск сервісу

```bash
$ sudo systemctl start cron
```

## 4. Додавання сервісу до автозавантаження

```bash
# Введення
$ sudo systemctl enable cron
# Виведення
Synchronizing state of cron.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable cron
```

# Завдання 3. Робота з логами

## 1. Перехід в директорію `/var/log` і виведення останніх 10 рядків файлу `syslog`

```bash
# Введення
$ cd /var/log
/var/log$ tail -n 10 syslog
# Виведення
2026-06-15T10:44:53.806380+02:00 DESKTOP-KF9NMIG cron[1235]: (CRON) INFO (Skipping @reboot jobs -- not system startup)
2026-06-15T10:46:23.917518+02:00 DESKTOP-KF9NMIG systemd[1]: Reload requested from client PID 1254 ('systemctl') (unit init.scope)...
2026-06-15T10:46:23.918602+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading...
2026-06-15T10:46:24.084640+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading finished in 166 ms.
2026-06-15T10:46:24.138044+02:00 DESKTOP-KF9NMIG systemd[1]: Reload requested from client PID 1295 ('systemctl') (unit init.scope)...
2026-06-15T10:46:24.138123+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading...
2026-06-15T10:46:24.256333+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading finished in 117 ms.
2026-06-15T10:46:24.286384+02:00 DESKTOP-KF9NMIG systemd[1]: Reload requested from client PID 1250 ('systemctl') (unit init.scope)...
2026-06-15T10:46:24.286476+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading...
2026-06-15T10:46:24.411226+02:00 DESKTOP-KF9NMIG systemd[1]: Reloading finished in 124 ms.
```

## 2. Перегляд лише помилок через journalctl (рівень "err")

```bash
# Введення
$ sudo journalctl -p err -b
# Виведення
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: PCI: Fatal: No config space access function found
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: hv_balloon: Cold memory discard hypercall failed with status 1b00000005
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: hv_balloon: Underlying Hyper-V does not support order less than 9. Hypercall fa>
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: hv_balloon: Defaulting to page_reporting_order 9
Jun 15 10:25:50 DESKTOP-KF9NMIG unknown: WSL (163) ERROR: CheckConnection: getaddrinfo() failed: -5
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: misc dxg: dxgk: dxgkio_is_feature_enabled: Ioctl failed: -22
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Jun 15 10:25:50 DESKTOP-KF9NMIG kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -2
```

## 3. Пошук записів про запуск/зупинку сервісу `cron`:

```bash
# Введення
$ sudo journalctl -u cron | grep -E "Started|Stopped"
# Виведення
Jun 15 10:25:50 DESKTOP-KF9NMIG systemd[1]: Started cron.service - Regular background program processing daemon.
Jun 15 10:43:25 DESKTOP-KF9NMIG systemd[1]: Stopped cron.service - Regular background program processing daemon.
Jun 15 10:44:53 DESKTOP-KF9NMIG systemd[1]: Started cron.service - Regular background program processing daemon.
```

# Завдання 4. Створення власного сервісу

## 1. Створення bash-скрипту

```bash
# Створення файлу date_logger.sh
$ nano date_logger.sh
# Скрипт оновлення дати щосекунди
#!/bin/bash
while true
do
    echo $(date) >> /home/ernest/timestamp.log
    sleep 1
done
# Надання прав на виконання скрипту
$ chmod +x date_logger.sh
```

## 2. Створення файлу конфігурації сервісу

```bash
$ sudo nano /etc/systemd/system/myscript.service
```

## 3. Налаштування файлу на запуск bash-скрипту

```bash
[Unit]
Description=My Custom Date Logger Service
After=network.target

[Service]
Type=simple
ExecStart=/bin/bash /home/ernest/date_logger.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

## 4. Запуск та перевірка `.service`

```bash
# Оновлення конфігурації systemd, щоб система побачила новий сервіс
$ sudo systemctl daemon-reload
# Запуск сервісу
$ sudo systemctl start myscript.service
# Перевірка статусу сервісу
$ sudo systemctl status myscript.service
● myscript.service - My Custom Date Logger Service
     Loaded: loaded (/etc/systemd/system/myscript.service; disabled; preset: enabled)
     Active: active (running) since Mon 2026-06-15 11:11:55 CEST; 15s ago
 Invocation: 710be3f39f584c29996de25a5f7b8dd6
   Main PID: 1649 (bash)
      Tasks: 2 (limit: 8176)
     Memory: 2.7M (peak: 3.4M)
        CPU: 131ms
     CGroup: /system.slice/myscript.service
             ├─1649 /bin/bash /home/ernest/date_logger.sh
             └─1687 sleep 1

Jun 15 11:11:55 DESKTOP-KF9NMIG systemd[1]: Started myscript.service - My Custom Date Logger Se>
# Перевірка, що дані дійсно щосекунди записуються у файл
$ tail -f ~/timestamp.log
Mon Jun 15 11:12:18 CEST 2026
Mon Jun 15 11:12:19 CEST 2026
Mon Jun 15 11:12:20 CEST 2026
Mon Jun 15 11:12:21 CEST 2026
Mon Jun 15 11:12:22 CEST 2026
Mon Jun 15 11:12:23 CEST 2026
Mon Jun 15 11:12:24 CEST 2026
Mon Jun 15 11:12:25 CEST 2026
Mon Jun 15 11:12:26 CEST 2026
Mon Jun 15 11:12:27 CEST 2026
Mon Jun 15 11:12:28 CEST 2026
Mon Jun 15 11:12:29 CEST 2026
Mon Jun 15 11:12:30 CEST 2026
Mon Jun 15 11:12:31 CEST 2026
Mon Jun 15 11:12:33 CEST 2026
Mon Jun 15 11:12:34 CEST 2026
Mon Jun 15 11:12:35 CEST 2026
Mon Jun 15 11:12:36 CEST 2026
Mon Jun 15 11:12:37 CEST 2026
Mon Jun 15 11:12:38 CEST 2026
Mon Jun 15 11:12:39 CEST 2026
```