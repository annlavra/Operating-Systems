# 3. Thread Syncronization

## Theme: "Thread Syncronization"

### Overview

#### Задача
Написать программу для консольного процесса, который состоит из потока _main_ и нескольких экземпляров потока _marker_.
#### Поток main
Поток _main_ должен выполнять следующие действия:
1. Захватить память под массив целых чисел, размерность которого вводится с консоли. 
2. Инициализировать элементы массива нулями. 
3. Запросить количество потоков _marker_, которые требуется запустить. 
4. Запустить заданное количество экземпляров потока _marker_. В качестве параметра каждому экземпляру потока _marker_ передать его порядковый номер в запуске. 
5. Дать сигнал на начало работы всех потоков _marker_. 
6. Выполнять в цикле следующие действия: 
    + Ждать, пока все потоки _marker_ не подадут сигналы о невозможности продолжения своей работы. 
    + Вывести содержимое массива на консоль. 
    + Запросить с консоли порядковый номер потока marker, которому будет подан сигнал на завершение своей работы. 
    + Подать потоку _marker_, номер которого получен в подпункте 3, сигнал на завершение работы. 
    + Ждать завершение работы потока _marker_, которому был подан сигнал на завершение работы в подпункте 4. 
    + Вывести содержимое массива на консоль. 
    + Подать сигнал на продолжение работы, оставшимся потокам _marker_. 
7. Завершить свою работу после завершения работы всех потоков _marker_.

#### Поток marker
Поток _marker_ должен выполнять следующие действия: 
1. Начать работу по сигналу от потока _main_. 
2. Инициализировать генерацию последовательности случайных чисел. Для этого использовать функцию _srand_, которой передать в качестве аргумента свой порядковый номер. 
3. Работать циклически, выполняя на каждом цикле следующие действия: 
    + Генерировать случайное число, используя функцию rand. 
    + Разделить это число по модулю на размерность массива. 
    + Если элемент массива, индекс которого равен результату деления, равен нулю, то выполнить следующие действия: 
        - Поспать 5 миллисекунд. 
        - Занести в элемент, индекс которого вычислен, свой порядковый номер. 
        - Поспать 5 миллисекунд. 
        - Продолжить исполнение цикла 3. 
    + В противном случае: 
        - Вывести на консоль следующую информацию: 
            - свой порядковый номер; 
            - количество помеченных элементов; 
            - индекс элемента массива, который невозможно пометить. 
        - Дать сигнал потоку _main_ на невозможность продолжения своей работы. 
        - Ждать ответный сигнал на продолжение или завершение работы от потока _main_. 
4. Если получен сигнал на завершение работы, то выполнить следующие действия: 
    - Заполнить нулями в массиве все элементы, которые он пометил. 
    - Завершить работу. 
5. Если получен сигнал на продолжение работы, то продолжить исполнение цикла из пункта 3.