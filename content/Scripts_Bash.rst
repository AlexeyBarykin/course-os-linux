Скрипты и переменные в bash
===========================

Теоретическое введение
~~~~~~~~~~~~~~~~~~~~~~

Оболочка, или шелл (shell) — это программа, принимает ваши команды и
передаёт их операционной системе. BASH расшифровывается как Bourne-Again
SHell (что может переводится как «перерожденный шел»).

Bash – это универсальный инструмент для выполнения различных задач,
который в некоторых случаях позволяет избежать установки
специализированного программного обеспечения. Одновременно, это
скриптовый язык программирования, позволяющий создавать сценарии для
автоматизации различных операций.

Скрипт или как его еще называют - сценарий, это последовательность
команд, которые по очереди считывает и выполняет
программа-интерпретатор, в нашем случае это программа командной строки -
bash

Скрипт - это обычный текстовый файл, в котором перечислены обычные
команды, которые мы привыкли вводить вручную, а также указана программа,
которая будет их выполнять. Загрузчик, который будет выполнять скрипт не
умеет работать с переменными окружения, поэтому ему нужно передать
точный путь к программе, которую нужно запустить. А дальше он уже
передаст ваш скрипт этой программе и начнется выполнение.

Простейший пример скрипта для командной оболочки Bash:

.. code:: bash

    # !/bin/bash
    echo "Please I want a good grade"




Итак, любой bash-скрипт должен начинаться со строки:

.. code:: bash

    #!/bin/bash

В этой строке после #! указывается путь к bash-интерпретатору, поэтому
если вдруг он находится в другой директории – необходимо поменять путь.
Проверить, где он находится можно, набрав whereis bash

Команды оболочки отделяются знаком перевода строки, комментарии выделяют
знаком решётки. Как и в командной строке, в Bash можно записывать
команды в одной строке, разделяя точкой с запятой.

Нужно отметить, что перед тем как запустить скрипт Сейчас осталось лишь
сделать этот файл исполняемым, иначе, попытавшись его запустить, вы
столкнётесь с ошибкой Permission denied.

Чтобы сделать файл исполняемым, необходимо набрать

.. code:: bash

    chmod +x ./myscript




Теперь, после настройки разрешений, все будет работать как надо.

Основные команды.
~~~~~~~~~~~~~~~~~

В Linux файлы и каталоги имеют иерархическую организацию, то есть
существует некий начальный каталог, называемый корневым. В нём
содержатся файлы и подкаталоги, которые в свою очереди содержат файлы и
свои подкаталоги.

.. code:: bash

    pwd



Команда pwd (сокращение от print working directory) отображает текущее
местоположение в структуре каталогов.

.. code:: bash

    cd

Команда cd позволяет перейти в новый каталог.

Для некоторых часто используемых директорий существуют сокращения,
позволяющие не писать полный путь. Например:

cd ~ позволяет перейти в домашний каталог

cd .. позволяет перейти на 1 уровень выше

.. code:: bash

    mkdir

Команда mkdir создаёт новый каталог в текущем каталоге.

.. code:: bash

    echo

Команда echo выводит свои аргументы по стандартному каналу вывода

.. code:: bash

    cat


Если вам необходимо проверить содержимое определенного файла, к примеру
hosting.txt, достаточно воспользоваться командой cat. Это выглядит
примерно так:

cat hosting.txt

.. code:: bash

    ssh

Данная команда является протоколом подключения к серверу.

Пример использования команды на занятии:

.. code:: bash

    ssh -p 55078 b0690613@remote.vdi.mipt.ru

.. code:: bash

    head

Команда head читает первые 10 строк любого переданного текста и выводит
их по стандартному каналу.

.. code:: bash

    tail


.. code:: bash

    Команда tail работает аналогично команде head, но читает строки с конца

.. code:: bash

    ps

Команда ps выводит информацию о запущенных процессах.

Выводится четыре элемента:

• ID процесса (PID),

• тип терминала (TTY),

• время работы процесса (TIME),

• имя команды, запустившей процесс (CMD).

.. code:: bash

    awk

Команда awk находит и заменяет текст в файлах по заданному шаблону:

.. code:: bash

    awk 'pattern {action}' test.txt

.. code:: bash

    wget

Команда wget скачивает файлы из Сети и помещает их в текущий каталог.

Существует также большое количество других команд, применяемых в циклах,
условных и других конструкциях в скриптах. Некоторые из них перечислены
ниже.

break - выход из цикла for, while или until

continue - выполнение следующей итерации цикла for, while или until

echo - вывод аргументов, разделенных пробелами, на стандартное
устройство вывода

exit - выход из оболочки

export - отмечает аргументы как переменные для передачи в дочерние
процессы в среде

hash - запоминает полные имена путей команд, указанных в качестве
аргументов, чтобы не искать их при следующем обращении

kill - посылает сигнал завершения процессу

pwd - выводит текущий рабочий каталог

read - читает строку из ввода оболочки и использует ее для присвоения
значений указанным переменным.

return - заставляет функцию оболочки выйти с указанным значением

shift - перемещает позиционные параметры налево

test - вычисляет условное выражение

times - выводит имя пользователя и системное время, использованное
оболочкой и ее потомками

trap - указывает команды, которые должны выполняться при получении
оболочкой сигнала

unset - вызывает уничтожение переменных оболочки

wait - ждет выхода из дочернего процесса и сообщает выходное состояние.

Переменные.
~~~~~~~~~~~

Написание скриптов на Bash редко обходится без сохранения временных
данных, а значит создания переменных. Без переменных не обходится ни
один язык программирования и наш примитивный язык командной оболочки
тоже.

Существуют два типа переменных, которые можно использовать в
bash-скриптах:

1. Переменные среды

2. Пользовательские переменные

.. code:: bash

    #!/bin/bash 
    # display user home 
    echo "Home for the current user is: $HOME"


В этом коротком скрипте HOME является переменной среды. Можно заметить,
что она находится в двойных кавычках, это не помешает системе её
распознать.

Наоборот, для того чтобы вывести на экран именно значок доллара, а не
значение переменной – понадобится использование управляющего символа,
обратной косой черты, перед знаком доллара:

.. code:: bash

    echo "I have \$1 in my pocket"

В дополнение к переменным среды, bash-скрипты позволяют задавать и
использовать в сценарии собственные переменные. Подобные переменные
хранят значение до тех пор, пока не завершится выполнение сценария.

Как и в случае с системными переменными, к пользовательским переменным
можно обращаться, используя знак доллара:

.. code:: bash

    #!/bin/bash 
    # testing variables 
    grade=7
    student="Alexey" 
    echo "$student worked hard this semester, his grade will be $grade or more"


Одна из самых полезных возможностей bash-скриптов — это возможность
извлекать информацию из вывода команд и назначать её переменным, что
позволяет использовать эту информацию где угодно в файле сценария.

Сделать это можно двумя способами.

• С помощью значка обратного апострофа «`»

• С помощью конструкции $()

Приведем пример скрипта, содержащего вторую конструкцию

.. code:: bash

    #!/bin/bash 
    mydir=$(pwd) 
    echo $mydir


В ходе его работы вывод команды pwd будет сохранён в переменной mydir,
содержимое которой, с помощью команды echo, попадёт в консоль.

Bash не различает типов переменных так, как языки высокого уровня,
например, С++, вы можете присвоить переменной как число, так и строку.
Одинаково все это будет считаться строкой. Оболочка поддерживает только
слияние строк, для этого просто запишите имена переменных подряд:

.. code:: bash

    #!/bin/bash
    string1="hello "
    string2= "world"
    string=$string1$string2


Параметры скрипта
~~~~~~~~~~~~~~~~~

Не всегда можно создать bash скрипт, который не зависит от ввода
пользователя. В большинстве случаев нужно спросить у пользователя какое
действие предпринять или какой файл использовать. При вызове скрипта мы
можем передавать ему параметры. Все эти параметры доступны в виде
переменных с именами в виде номеров.

Переменная с именем 1 содержит значение первого параметра, переменная 2,
второго и так далее. Этот bash скрипт выведет значение первого параметра

.. code:: bash

    #!/bin/bash
    echo $1


Примеры конструкций, используемых в скриптах.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

В скриптах можно использовать многие элементы программирования, уже
знакомые нам по изучению языка программирования Python. К примеру,
управляющие конструкции или циклы. Ниже будет приведен синтаксис этих
конструкций.

Условная конструкция:
^^^^^^^^^^^^^^^^^^^^^

if команда_условие

then

команда

else

команда

fi

Эта команда проверяет код завершения команды условия, и если 0 (успех)
то выполняет команду или несколько команд после слова then, если код
завершения 1 выполняется блок else, fi означает завершение блока команд

Цикл for:
^^^^^^^^^

for переменная in список

do

команда

done

Перебирает весь список, и присваивает по очереди переменной значение из
списка, после каждого присваивания выполняет команды, расположенные
между do и done.

Например, переберем пять цифр:

#!/bin/bash

for index in 1 2 3 4 5

do

echo $index

done

А еще можно перечислить все файлы из текущей директории:

.. code:: bash

    $  for file in $(ls -l); do echo "$file"; done

Цикл while:
^^^^^^^^^^^

while команда условие

do

команда

done

.. code:: bash

    !/bin/bash
    index=1
    while [[ $index < 5 ]]
    do
    echo $index
    let "index=index+1"
    done


При этом команда let просто выполняет указанную математическую операцию,
в нашем случае увеличивает значение переменной на единицу.




