<!-- 5.2.1 -->
## Два метода изменения списка ACL
После настройки списка управления доступом, возможно, потребуется изменить его. Списки ACL с большим количеством ACE могут быть сложными для настройки. Иногда настроенные ACE не дают ожидаемого поведения. По этим причинам для достижения желаемого результата фильтрации списки ACL может потребоваться немного проб и ошибок.

В этом разделе рассматриваются два метода, которые следует использовать при изменении списка ACL:

* Использование текстового редактора
* Использование порядковых номеров

<!-- 5.2.2 -->
## Метод с использованием текстового редактора
ACL с несколькими ACE следует создавать в текстовом редакторе. Таким образом можно создать или отредактировать список контроля доступа (ACL), после чего вставить его в интерфейс маршрутизатора. Это также упрощает задачи редактирования и исправления ACL.

Например предположим, что ACL 1 был введен неправильно, используя **19** вместо **192** первого октета, как показано в текущей конфигурации.

```
R1# show run | section access-list 
access-list 1 deny 19.168.10.10
access-list 1 permit 192.168.10.0 0.0.0.255
R1#
```

В этом примере первый ACE должен был запретить хост в 192.168.10.10. Тем не менее запись ACE была введена неправильно.

Чтобы исправить ошибку:

* Скопируйте список ACL из текущей конфигурации и вставьте его в текстовый редактор.
* Внесите необходимые изменения.
* Удалите ранее настроенный список ACL на маршрутизаторе, вставьте отредактированные команды, иначе ACL будет только добавлять (т. е. добавлять) к существующим ACE ACL на маршрутизаторе.
* Скопируйте и вставьте отредактированный список ACL обратно в маршрутизатор.

Предположим, что ACL 1 теперь исправлена. Поэтому недопустимый список ACL должен быть удален и исправленные инструкции ACL 1 должны быть вставлены в режиме глобальной конфигурации, как показано в выходных данных.

```
R1(config)# no access-list 1
R1(config)#
R1(config)# access-list 1 deny 19.168.10.10
R1(config)# access-list 1 permit 192.168.10.0 0.0.0.255
R1(config)#
```

<!-- 5.2.3 -->
## Метод с использованием порядковых номеров
ACL ACE также можно удалить или добавить с помощью порядкового номера ACL. Последовательные номера присваиваются автоматически при вводе ACE. Эти номера перечислены в команде **show access-lists**. Команда **show running-config** не отображает порядковые номера.

В предыдущем примере неправильная ACE для ACL 1 использует порядковый номер 10, как показано в примере.

```
R1# show access-lists 
Standard IP access list 1 
    10 deny 19.168.10.10 
    20 permit 192.168.10.0, wildcard bits 0.0.0.255
R1#
```

Используйте команду **ip access-list standard** для редактирования списка управления доступом. Записи нельзя перезаписать с теми же порядковыми номерами, что и у существующих записей. Таким образом, текущие инструкции должен быть сначала удалены с помощью команды **no 10**. Затем правильный ACE может быть добавлен, используя номер последовательности 10 настроен. Проверьте изменения с помощью команды **show access-lists**, как показано в примере.

```
R1# conf t
R1(config)# ip access-list standard 1
R1(config-std-nacl)# no 10
R1(config-std-nacl)# 10 deny host 192.168.10.10
R1(config-std-nacl)# end
R1# show access-lists
Standard IP access list 1
    10 deny   192.168.10.10
    20 permit 192.168.10.0, wildcard bits 0.0.0.255
R1#
```

<!-- 5.2.4 -->
## Пример изменения именованного списка ACL
Именованные ACL также могут использовать порядковые номера для удаления и добавления ACE. См. пример **ACL NO-ACCESS**.

```
R1# show access-lists
Standard IP access list NO-ACCESS
    10 deny   192.168.10.10
    20 permit 192.168.10.0, wildcard bits 0.0.0.255
```

Предположим, что узел 192.168.10.5 из сети 192.168.10.0/24 также должен быть запрещен. Если вы ввели новый ACE, он будет добавлен в конец ACL. Таким образом узел никогда не будет блокирован, так как инструкция ACE 20 разрешает все узлы из этой сети.

Решение заключается в добавлении ACE, запрещающего хост 192.168.10.5 между ACE 10 и ACE 20, например ACE 15, как показано в примере. Также обратите внимание, что новый ACE был введен без использования ключевого слова **host**. Ключевое слово является необязательным при указании хоста назначения.

Используйте эту команду **show access-lists**, чтобы убедиться, что ACL теперь имеет новый ACE 15, вставленный соответствующим образом перед инструкцию permit.

Обратите внимание, что порядковый номер 15 отображается перед порядковым номером 10. Можно ожидать, что в выходных данных записи будут отображены в том же порядке, в котором они были введены. Но IOS располагает утверждения для хостов с помощью специальной функции хеширования. Результирующий порядок оптимизирует поиск записи ACL хоста, а затем выполняет поиск операторов диапазона.

**Примечание:** функция расстановки применяется только к хостовым инструкциям стандартного списка доступа IPv4. Подробные сведения о функции расстановки не рассматривается в этой учебной программе.

```
R1# configure terminal
R1(config)# ip access-list standard NO-ACCESS
R1(config-std-nacl)# 15 deny 192.168.10.5
R1(config-std-nacl)# end
R1#
R1# show access-lists
Standard IP access list NO-ACCESS
    15 deny   192.168.10.5
    10 deny   192.168.10.10
    20 permit 192.168.10.0, wildcard bits 0.0.0.255
R1#
```

<!-- 5.2.5 -->
## ACL-статистика
Обратите внимание, что команда **show access-lists** в примере показывает статистику для каждой инструкции, которые сработали. Запрещающий ACE в ACL NO-ACCESS сработал 20 раз, а разрешающий ACE - 64 раза.

Обратите внимание, что подразумеваемый неявный deny any не показывает никакой статистики. Чтобы отслеживать, сколько неявных отклоненных пакетов было сопоставлено, необходимо вручную настроить команду **deny any** в конце списка ACL.

Используйте команду **clear access-list counters** для очистки статистики ACL. Эту команду можно применять отдельно или с указанием номера или имени конкретного ACL-списка.

```
R1# show access-lists
Standard IP access list NO-ACCESS
    10 deny   192.168.10.10  (20 matches) 
    20 permit 192.168.10.0, wildcard bits 0.0.0.255  (64 matches) 
R1# clear access-list counters NO-ACCESS
R1# show access-lists
Standard IP access list NO-ACCESS
    10 deny   192.168.10.10
    20 permit 192.168.10.0, wildcard bits 0.0.0.255
R1#
```

<!-- 5.2.6 Проверка синтаксиса - изменение списков ACL IPv4
Измените список ACL с помощью порядкового номера.

![](./assets/5.2.6.PNG) здесь задание 5.2.6-->

<!-- 5.2.7 -->
## Packet Tracer. Настройка и модификация стандартных списков контроля доступа для IPv4
В рамках данного упражнения Packet Tracer необходимо решить следующие задачи.

* Часть 1: Настройка устройств и проверка подключения.
* Часть 2: Настройка и проверка стандартных нумерованных ACL-списков и стандартных именованных ACL-списков.
* Часть 3: Изменение стандартного ACL-списка.


[Настройка и модификация стандартных списков контроля доступа для IPv4 (pdf)](./assets/5.2.7-packet-tracer---configure-and-modify-standard-ipv4-acls_ru-RU.pdf)

[Настройка и модификация стандартных списков контроля доступа для IPv4 (pka)](./assets/5.2.7-packet-tracer---configure-and-modify-standard-ipv4-acls_ru-RU.pka)