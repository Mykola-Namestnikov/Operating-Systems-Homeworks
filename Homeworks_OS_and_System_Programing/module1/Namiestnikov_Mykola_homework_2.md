# Завдання 1. Ієрархія каталогів Linux

## 1. Перехід у кореневий каталог `/` з демонстрацією вмісту

```bash
# Введення
$ cd / && ls
# Виведення
LICENSE.txt        cmd/  git-bash.exe*  proc/         unins000.exe*
ReleaseNotes.html  dev/  git-cmd.exe*   tmp/          unins000.msg
bin/               etc/  mingw64/       unins000.dat  usr/
```

## 2. Перехід у каталог `/etc` з демонстрацією вмісту

```bash
# Введення
$ cd /etc && ls
# Виведення
DIR_COLORS       inputrc              nsswitch.conf         services
bash.bashrc      install-options.txt  package-versions.txt  ssh/
docx2txt.config  msystem              pkcs11/               tigrc
fstab            msystem.d/           pki/                  vimrc
gitattributes    mtab@                profile
gitconfig        nanorc               profile.d/
hosts            networks             protocols
```

## 3. Перехід у каталог `/home` з демонстрацією списку користувачів

```bash
# Введення
$  cd /c/Users && ls
# Виведення
'All Users'@  'Default User'@   Public/      'Все пользователи'@
 Default/      Ernest/          desktop.ini
```

# Завдання 2. Файли, каталоги та посилання

## 1. Створюємо новий каталог у домашньому каталозі та переходимо в нього

```bash
$ cd ~
$ mkdir lab2
$ cd lab2
```

## 2. Створюємо всередині файл за допомогою перенаправлення потоку

```bash
$ echo "Linux Homework 2" > file.txt
```

## 3. Копіюємо файл у нове ім’я

```bash
$ cp file.txt file_copy.txt
```

## 4. Перейменовуємо копію

```bash
$ mv file_copy.txt renamed_file.txt
```

## 5. Створюємо жорстке посилання (Hard Link)

```bash
$ ln file.txt hard_link.txt
```

## 6. Створюємо символічне посилання (Symbolic Link / Soft Link)

```bash
$ ln -s file.txt soft_link.txt
```

## 7. Знаходимо файл за іменем у поточному каталозі

```bash
# Введення
$ find . -name "file.txt"
# Виведення
./file.txt
```

# Завдання 3. Права доступу

## 1. Перегляд прав файлу, який було створено

```bash
# Введення
$ ls -l file.txt
# Виведення
-rw-r--r-- 2 Ernest 197121 17 Jun 14 01:55 file.txt
```

## 2. Надання файлу права лише на читання

```bash
$ chmod 444 file.txt
```

## 3. Надання власнику права на запис

```bash
$ chmod u+w file.txt
```

## 4. Перегляд значення Umask

```bash
# Введення
$ umask
# Виведення
0022
```

## 5. Встановлення нового значення Umask (022)

```bash
$ umask 022
```

# Завдання 4. Користувачі

## 1. Створення нового користувача

```bash
$ sudo useradd -m junior
```

## 2. Додавання його до sudo-групи (надання адмін-прав)

```bash
$ sudo usermod -aG sudo junior
```

## 3. Перевірка, що користувач існує в системі

```bash
# Введення
$ grep "junior" /etc/passwd
# Виведення
junior:x:1001:1001::/home/junior:/bin/bash
```