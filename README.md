New line

https://github.com/Solmyr88/branching/network

https://github.com/Solmyr88/branching

end homework112

Домашнее задание к занятию "Работа в терминале, лекция 1"

https://github.com/Solmyr88/devops-netology

1. Установите средство виртуализации Oracle VirtualBox.

2. Установите средство автоматизации Hashicorp Vagrant.

3. В вашем основном окружении подготовьте удобный для дальнейшей работы терминал. Можно предложить:

iTerm2 в Mac OS X
Windows Terminal в Windows
выбрать цветовую схему, размер окна, шрифтов и т.д.
почитать о кастомизации PS1/применить при желании.
Несколько популярных проблем:

Добавьте Vagrant в правила исключения перехватывающих трафик для анализа антивирусов, таких как Kaspersky, если у вас возникают связанные с SSL/TLS ошибки,
MobaXterm может конфликтовать с Vagrant в Windows,
Vagrant плохо работает с директориями с кириллицей (может быть вашей домашней директорией), тогда можно либо изменить VAGRANT_HOME, либо создать в системе профиль пользователя с английским именем,
VirtualBox конфликтует с Windows Hyper-V и его необходимо отключить,
WSL2 использует Hyper-V, поэтому с ним VirtualBox также несовместим,
аппаратная виртуализация (Intel VT-x, AMD-V) должна быть активна в BIOS,
в Linux при установке VirtualBox может дополнительно потребоваться пакет linux-headers-generic (debian-based) / kernel-devel (rhel-based).
С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

4. Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните vagrant init. Замените содержимое Vagrantfile по умолчанию следующим:

 Vagrant.configure("2") do |config|
 	config.vm.box = "bento/ubuntu-20.04"
 end
 Выполнение в этой директории vagrant up установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

vagrant suspend выключит виртуальную машину с сохранением ее состояния (т.е., при следующем vagrant up будут запущены все процессы внутри, которые работали на момент вызова suspend), vagrant halt выключит виртуальную машину штатным образом.

5. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. 
Какие ресурсы выделены по-умолчанию?
ОП - 1024 мб
видеопамять 4 мб
процессоры 2 
порт удаленного дисплея 5902


6. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. 
Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
Указать/поменять слудующие значения в файле Vagrantfile:
  v.memory = 1024
  v.cpus = 2

7. Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

8. Ознакомиться с разделами man bash, почитать о настройках самого bash:

9. какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?
переменная size (HISTSIZE)        
int size;             /* Number of slots allocated to this array. */
 Manual page history(3readline) line 87 (press h for help or q to quit)

что делает директива ignoreboth в bash?
не записывать команду, которая начинается с пробела, либо команду, которая дублирует предыдущую.

В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
строка 229-234 в сценариях когда необходимо указать конкретное слово, а не часть слова, разграниченное пробелом или другими символами.

10. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?
Для создания файлов - touch {000001..100000}.txt

Создать 300000 файлов не получилось - 
touch {000001..300000}.txt
-bash: /usr/bin/rm: Argument list too long
максисмум что получилось 110000

11. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

Проверяет наличие директории tmp.
Конструкция [[ ... ]] более точная, так как избегает некоторые логические ошибки.

12. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:

bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash
(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

13. Чем отличается планирование команд с помощью batch и at?
at      выполняет команды в указанное время
batch   выполняет команды когда определенная загрузка системы
