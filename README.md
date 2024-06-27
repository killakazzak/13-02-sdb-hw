# Домашнее задание к занятию "`Защита хоста`" - `Тен Денис`

### Задание 1

1. Установите **eCryptfs**.
2. Добавьте пользователя cryptouser.
3. Зашифруйте домашний каталог пользователя с помощью eCryptfs.


*В качестве ответа  пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.*  


Установка eCryptfs 

```sh
sudo apt install ecryptfs-utils
```
Создание пользователя cryptouser

```sh
adduser --encrypt-home   cryptouser
```
Вывод
```sh
Adding user `cryptouser' ...
Adding new group `cryptouser' (1001) ...
Adding new user `cryptouser' (1001) with group `cryptouser' ...
Creating home directory `/home/cryptouser' ...
Setting up encryption ...

************************************************************************
YOU SHOULD RECORD YOUR MOUNT PASSPHRASE AND STORE IT IN A SAFE LOCATION.
  ecryptfs-unwrap-passphrase ~/.ecryptfs/wrapped-passphrase
THIS WILL BE REQUIRED IF YOU NEED TO RECOVER YOUR DATA AT A LATER TIME.
************************************************************************


Done configuring.

Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for cryptouser
Enter the new value, or press ENTER for the default
        Full Name []: Denis
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] Y
```
Проверка

```sh

root@ubuntu22-client:~# su cryptouser
Signature not found in user keyring
Perhaps try the interactive 'ecryptfs-mount-private'
cryptouser@ubuntu22-client:/root$ ecryptfs-mount-private
Enter your login passphrase:
Inserted auth tok with sig [4a7b4a15dfe61cac] into the user session keyring
cryptouser@ubuntu22-client:/root$ cd
cryptouser@ubuntu22-client:~$ touch test_file.txt
cryptouser@ubuntu22-client:~$ ls -la
total 88
drwx------ 2 cryptouser cryptouser 4096 Jun 27 14:41 .
drwxr-xr-x 5 root       root       4096 Jun 27 14:33 ..
-rw-rw-r-- 1 cryptouser cryptouser    0 Jun 27 14:35 123
-rw-rw-r-- 1 cryptouser cryptouser    0 Jun 27 14:35 345,
-rw-r--r-- 1 cryptouser cryptouser  220 Jun 27 14:33 .bash_logout
-rw-r--r-- 1 cryptouser cryptouser 3771 Jun 27 14:33 .bashrc
lrwxrwxrwx 1 cryptouser cryptouser   36 Jun 27 14:33 .ecryptfs -> /home/.ecryptfs/cryptouser/.ecryptfs
lrwxrwxrwx 1 cryptouser cryptouser   35 Jun 27 14:33 .Private -> /home/.ecryptfs/cryptouser/.Private
-rw-r--r-- 1 cryptouser cryptouser  807 Jun 27 14:33 .profile
-rw-rw-r-- 1 cryptouser cryptouser    0 Jun 27 14:41 test_file.txt
-rw-rw-r-- 1 cryptouser cryptouser    4 Jun 27 14:37 test.txt
cryptouser@ubuntu22-client:~$ pwd
/home/cryptouser
cryptouser@ubuntu22-client:~$ exit
exit
root@ubuntu22-client:~# ls -la /home/cryptouser/
total 8
dr-x------ 2 cryptouser cryptouser 4096 Jun 27 14:33 .
drwxr-xr-x 5 root       root       4096 Jun 27 14:33 ..
lrwxrwxrwx 1 cryptouser cryptouser   56 Jun 27 14:33 Access-Your-Private-Data.desktop -> /usr/share/ecryptfs-utils/ecryptfs-mount-private.desktop
lrwxrwxrwx 1 cryptouser cryptouser   36 Jun 27 14:33 .ecryptfs -> /home/.ecryptfs/cryptouser/.ecryptfs
lrwxrwxrwx 1 cryptouser cryptouser   35 Jun 27 14:33 .Private -> /home/.ecryptfs/cryptouser/.Private
lrwxrwxrwx 1 cryptouser cryptouser   52 Jun 27 14:33 README.txt -> /usr/share/ecryptfs-utils/ecryptfs-mount-private.txt
```


### Задание 2

1. Установите поддержку **LUKS**.
2. Создайте небольшой раздел, например, 100 Мб.
3. Зашифруйте созданный раздел с помощью LUKS.

*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*


## Дополнительные задания (со звёздочкой*)

Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале

```sh
sudo apt install gparted
apt install cryptsetup
root@ubuntu22-client:~# cryptsetup --version
cryptsetup 2.4.3

```


### Задание 3 *

1. Установите **apparmor**.
2. Повторите эксперимент, указанный в лекции.
3. Отключите (удалите) apparmor.


*В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.*
