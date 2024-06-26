# Функция создания виртуальной машины

Эта Bash-функция `create_vm` облегчает создание виртуальных машин с использованием libvirt. Она клонирует шаблонную ВМ, выполняет подготовку системы и запускает новую ВМ. Кроме того, она предоставляет IP-адрес новой ВМ и инструкции для доступа по SSH.

## Установка

1. Склонируйте этот репозиторий на свою систему:

   ```bash
   git clone https://github.com/gluteusmx/create_vm_func.git
   ```

2. Проверьте наличие директории `~/.bashrc.d/` и создайте её, если она отсутствует:

   ```bash
   if [ ! -d ~/.bashrc.d ]; then
       mkdir ~/.bashrc.d
   fi
   ```

3. Скопируйте файл функции `create_vm` в вашу директорию `~/.bashrc.d/`:

   ```bash
   cp create_vm_func/create_vm.sh ~/.bashrc.d/
   ```

4. Добавьте инструкцию include в ваш основной файл `~/.bashrc`:

   ```bash
   if [ -d ~/.bashrc.d ]; then
       for file in ~/.bashrc.d/*.sh; do
           source "$file"
       done
   fi
   ```

5. Запустите ваш файл `~/.bashrc`, чтобы применить изменения:

   ```bash
   source ~/.bashrc
   ```

## Использование

Для создания новой виртуальной машины используйте функцию `create_vm`, указав желаемое распределение и имя ВМ:

```bash
create_vm <DISTRO> <VMNAME>
```

Например:

```bash
create_vm centos8 student
```

Это создаст виртуальную машину с именем `student`, используя шаблон CentOS 8.

## Дополнительные замечания

- Убедитесь, что у вас есть необходимые права для выполнения команд `sudo`.
- Функция предполагает, что шаблонные ВМ имеют имена в формате `<DISTRO>_template`.
- После создания функция предоставляет IP-адрес новой ВМ и инструкции для доступа по SSH.

## Лицензия

Этот скрипт распространяется под [лицензией MIT](https://github.com/git/git-scm.com/blob/main/MIT-LICENSE.txt).
