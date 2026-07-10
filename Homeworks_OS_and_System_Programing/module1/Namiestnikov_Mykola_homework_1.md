# Завдання 1. Базові команди

## 1. Вміст домашнього каталогу

```bash
# Введення
$ ls
# Виведення
LICENSE.txt        cmd/  git-bash.exe*  proc/         unins000.exe*
ReleaseNotes.html  dev/  git-cmd.exe*   tmp/          unins000.msg
bin/               etc/  mingw64/       unins000.dat  usr/
```

## 2. Перехід у каталог Downloads та показ вмісту

```bash
# Введення
$ cd ~/Downloads
$ ls
# Виведення
OperaGXSetup.exe*  desktop.ini
```

## 3. Створення порожнього файлу (без touch)

```bash
# Введення
$ echo -n > myfile.txt
```

## 4. Перегляд вмісту файлу

```bash
# Введення
$ cat myfile.txt
# Виведення
```

## 5. Перехід у домашній каталог абсолютним шляхом

```bash
# Введення
$ cd /c/Users/Ernest
```

## 6. Перехід у домашній каталог відносним шляхом

```bash
# Введення
$ cd ~
```

# Завдання 2. Робота з документацією

**1. Який ключ ls показує приховані файли?**  
*Ключ ```-a``` (або ```--all```). Він відображає всі файли, включно з тими, що починаються з крапки.*  
**2. Який ключ у cat нумерує рядки?**  
*Ключ ```-n``` (або ```--number```).*  
**3. Чим відрізняються man і --help?**  
*```man``` (manual) — це повноцінний довідник, який відкривається в окремому інтерфейсі (pager). Він містить детальний опис, приклади та структуру команди.  
```--help``` — це короткий витяг (флаг самої команди), який виводить список доступних опцій та синтаксис прямо в консоль. Це зручно для швидкого нагадування ключа.*  

# Завдання 3. Міні-сценарій

## Сценарій:

```bash
# 1. Переходимо в каталог /tmp
$ cd /tmp

# 2. Створюємо там робочу папку для тесту
$ mkdir homework_test

# 3. Переходимо в створену папку
$ cd homework_test

# 4. Створюємо порожній файл
$ echo "Hello, Linux" > test_file.txt

# 5. Переглядаємо список файлів
$ ls -l
## Виведення
total 1
-rw-r--r-- 1 Ernest 197121 13 Apr 14 19:19 test_file.txt

# 6. Переходимо в інше місце (корінь системи)
$ cd /

# 7. Повертаємось назад у попередній каталог
$ cd -
## Виведення
/tmp/homework_test

# 8. Переглядаємо вміст файлу
$ cat test_file.txt
## Виведення
Hello, Linux

# 9. Переглядаємо документацію команди mkdir
$ mkdir --help
## Виведення
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

Mandatory arguments to long options are mandatory for short options too.
  -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
  -p, --parents     no error if existing, make parent directories as needed
  -v, --verbose     print a message for each created directory
  -Z                   set SELinux security context of each created directory
                         to the default type
      --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                         or SMACK security context to CTX
      --help     display this help and exit
      --version  output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Report any translation bugs to <https://translationproject.org/team/>
Full documentation <https://www.gnu.org/software/coreutils/mkdir>
or available locally via: info '(coreutils) mkdir invocation'

# 10. Виходимо з папки
$ cd ..
```