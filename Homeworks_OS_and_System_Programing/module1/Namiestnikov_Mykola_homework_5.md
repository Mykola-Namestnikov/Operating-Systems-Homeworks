# Завдання 1. Мережева діагностика

## 1. Виведення IP-адрес та мережевих інтерфейсів

```bash
$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host proto kernel_lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:1f:c8:e0 brd ff:ff:ff:ff:ff:ff
    altname enx00155d1fc8e0
    inet 172.30.56.185/20 brd 172.30.63.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:fe1f:c8e0/64 scope link proto kernel_ll
       valid_lft forever preferred_lft forever
```

Команда відобразила два мережеві інтерфейси: локальну петлю `lo` з адресою `127.0.0.1` та основний віртуальний інтерфейс `eth0`. Інтерфейс `eth0` успішно піднятий (`state UP`) та отримав приватну IP-адресу `172.30.56.185` у підмережі з маскою `/20`.

## 2. Перевірка доступності публічного вузла

```bash
$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=116 time=36.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=116 time=35.6 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=116 time=34.6 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=116 time=53.9 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 34.567/40.204/53.859/7.922 ms
```

Команда успішно відправила та отримала всі 4 пакети від публічного DNS-сервера Google (`8.8.8.8`) без жодних втрат (`0% packet loss`). Середній час відгуку (`rtt`) склав близько 35–40 мс, що підтверджує стабільне та активне підключення системи до інтернету.

## 3. Перевірка відкритих listening-портів

```bash
$ sudo ss -tulpn
Netid  State   Recv-Q   Send-Q     Local Address:Port     Peer Address:Port  Process
udp    UNCONN  0        0              127.0.0.1:323           0.0.0.0:*      users:(("chronyd",pid=203,fd=4))
udp    UNCONN  0        0              127.0.0.1:323           0.0.0.0:*
udp    UNCONN  0        0             127.0.0.54:53            0.0.0.0:*      users:(("systemd-resolve",pid=64,fd=18))
udp    UNCONN  0        0          127.0.0.53%lo:53            0.0.0.0:*      users:(("systemd-resolve",pid=64,fd=16))
udp    UNCONN  0        0                  [::1]:323              [::]:*
udp    UNCONN  0        0                  [::1]:323              [::]:*      users:(("chronyd",pid=203,fd=5))
tcp    LISTEN  0        4096          127.0.0.54:53            0.0.0.0:*      users:(("systemd-resolve",pid=64,fd=19))
tcp    LISTEN  0        4096       127.0.0.53%lo:53            0.0.0.0:*      users:(("systemd-resolve",pid=64,fd=17))
```

Команда відобразила активні мережеві сокети UDP та TCP, що очікують на підключення. У системі слухають два основні сервіси: логгер точного часу `chronyd` (на портах `323`) та системний DNS-резолвер `systemd-resolve` (на портах `53`), які прив'язані виключно до локального інтерфейсу зворотного зв'язку (`127.0.0.1` / `127.0.0.53`).

# Завдання 2. SSH-доступ з ключами та config

## 1. Генерація SSH-ключа

```bash
$ ssh-keygen -t ed25519 -C "ernest@homework"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/ernest/.ssh/id_ed25519):
Created directory '/home/ernest/.ssh'.
Enter passphrase for "/home/ernest/.ssh/id_ed25519" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ernest/.ssh/id_ed25519
Your public key has been saved in /home/ernest/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:5O5W1qmqPzYCSNMGEiYvc+rAv+TnymNwkF8GBeRID2M ernest@homework
The key's randomart image is:
+--[ED25519 256]--+
|oE.oo.           |
|*.B.             |
|oo+=.   .        |
|.Bo oo o         |
|ooo+o   S  . .   |
|o.oo.  .  o o    |
| .oo .  .o .     |
|  +o....= .      |
|  .==..*++       |
+----[SHA256]-----+
```

Створено пару ключів (приватний та публічний) за сучасним та безпечним алгоритмом Ed25519. Ключі збереглися у директорії `~/.ssh/`.

## 2. Копіювання ключа на сервер

```bash
$ ssh-copy-id ernest@127.0.0.1
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ernest/.ssh/id_ed25519.pub"
The authenticity of host '127.0.0.1 (127.0.0.1)' can't be established.
ED25519 key fingerprint is: SHA256:SLfI2bBHIADAy7fCnCanzhdGuNRuzL4/Wj0E9vPaJn4
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ernest@127.0.0.1's password:

Number of key(s) added: 1

Now try logging into the machine, with: "ssh 'ernest@127.0.0.1'"
and check to make sure that only the key(s) you wanted were added.
```

Публічний ключ успішно скопійовано та записано у файл `~/.ssh/authorized_keys` на стороні сервера. Тепер сервер розпізнаватиме мій ПК без пароля.

## 3. Налаштування файлу конфігурації `~/.ssh/config`

```bash
# Введення
$ nano ~/.ssh/config
# Вміст файлу
Host myserver
    HostName 127.0.0.1
    User ernest
    IdentityFile ~/.ssh/id_ed25519
```

Створено файл конфігурації, де для хоста з псевдонімом `myserver` чітко визначено IP-адресу, логін користувача та шлях до приватного ключа.

## 4. Підключення короткою командою та перевірка пароля

```bash
$ ssh myserver
Welcome to Ubuntu 26.04 LTS (GNU/Linux 6.18.33.1-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://docs.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Tue Jun 16 09:32:52 CEST 2026

  System load:  0.0                 Processes:             34
  Usage of /:   0.2% of 1006.85GB   Users logged in:       0
  Memory usage: 25%                 IPv4 address for eth0: 172.30.56.185
  Swap usage:   0%
```

Підключення відбулося миттєво за допомогою імені **Host: myserver**. Автентифікація пройшла успішно за допомогою SSH-ключа, **пароль система не запитувала**.

# Завдання 3. Копіювання файлів між машинами

## 1. Створення локального тестового файлу

```bash
echo "test" > test.txt
```

У поточному робочому каталозі успішно створено текстовий файл `test.txt` із вмістом "test".

## 2. Передача файлу на сервер через scp:

```bash
$ scp test.txt myserver:/home/ernest/
test.txt                               100%    5    18.2KB/s   00:00
```

Завдяки налаштованому раніше файлу `config`, файл `test.txt` успішно скопійовано у домашню директорію на сервері без введення повного IP та пароля.

## 3. Створення на сервері директорії для синхронізації

```bash
$ ssh myserver "mkdir -p ~/sync_folder"
```

Через віддалену команду SSH на сервері було створено цільову папку `sync_folder`.

## 4. Синхронізація локальної папки

```bash
$ mkdir -p ~/local_sync && cp test.txt ~/local_sync/
$ rsync -avz ~/local_sync/ myserver:/home/ernest/sync_folder/
sending incremental file list
./
test.txt

sent 139 bytes  received 38 bytes  118.00 bytes/sec
total size is 5  speedup is 0.03
```

Утиліта `rsync` синхронізувала вміст локальної папки з віддаленою. Прапорці `-avz` забезпечили архівний режим, візуалізацію процесу та стиснення даних під час передачі.

## 5. Перевірка файлів через SFTP

```bash
$ sftp myserver
Connected to myserver.
sftp> cd sync_folder
sftp> ls -l
-rw-rw-r--    ? ernest   ernest          5 Jun 16 09:45 test.txt
sftp> exit
```

Через протокол SFTP було здійснено вхід у папку `sync_folder` на сервері. За допомогою команди `ls -l` підтверджено, що файл `test.txt` присутній на сервері за шляхом `/home/ernest/sync_folder/test.txt`.