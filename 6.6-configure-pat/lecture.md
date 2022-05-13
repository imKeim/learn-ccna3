<!-- 6.6.1 -->
## Сценарий  PAT

В этом разделе вы узнаете, как настроить и проверить PAT. Раздел включает задание в Packet Tracer для проверки ваших навыков и знаний. В зависимости от способа выделения публичных IPv4-адресов интернет-провайдером существуют два способа настройки PAT. В первом случае поставщик услуг Интернета выделяет один общедоступный IPv4-адрес, который требуется организации для подключения к поставщику услуг Интернета, а в другом случае он выделяет более одного общедоступного адреса IPv4 для организации.

Оба метода будут продемонстрированы с использованием сценария, показанного на рисунке.

![](./assets/6.6.1.png)
<!-- /courses/ensa-dl/ae8e8c86-34fd-11eb-ba19-f1886492e0e4/aeb54e64-34fd-11eb-ba19-f1886492e0e4/assets/c63dd192-1c46-11ea-af56-e368b99e9723.svg -->

<!--
На рисунке изображен процесс преобразования адресов порта. Внутренняя сеть из двух ПК с PC1 по адресу 192.168.10.10 и PC2 по адресу 192.168.11.10, подключенных к маршрутизатору R1 на последовательном подключении S0/1/0 к маршрутизатору R2. На внешнем подключении к Интернету R2 у вас есть два сервера Svr1 по адресу 209.165.201.1 и Srvr2 по адресу 209.165.202.129. Существует таблица NAT с четырьмя столбцами: Внутренний локальный адрес, Внутренний глобальный адрес, Внешний локальный адрес и Внешний глобальный адрес. PC1 имеет внутренний локальный IP-адрес 192.168.10. 10:1444 сопоставлен с внутренним глобальным адресом 209.165.200. 225:1444. Внешний локальный IP-адрес — это адрес назначения 209.165.201. 1:80, сопоставленный с 209.165.201. 1:80. PC2 имеет внутренний локальный IP-адрес 192.168.11. 10:1444 сопоставлен с внутренним глобальным IP-адресом 209.165.200. 226:1445. Адрес назначения PC2s — внешний глобальный IP-адрес 209.165.202. 129:80 сопоставлен с внешним глобальным IP-адресом 209.165.202. 129:80
-->

<!-- 6.6.2 -->
## Настройка PAT для использования одного адреса IPv4

Чтобы настроить PAT на использование одного IPv4-адреса, просто добавьте ключевое слово **overload** в **ip nat inside source** команду. Остальная часть конфигурации аналогична статической и динамической конфигурации NAT, за исключением того, что при использовании PAT несколько узлов могут использовать один и тот же публичный IPv4 адрес для доступа в Интернет.

В этом примере для всех узлов сети 192.168.0.0/16 (соответствующей ACL-списку 1), отправляющих трафик в Интернет через маршрутизатор R2, будет выполняться преобразование в IPv4-адрес 209.165.200.225 (IPv4-адрес интерфейса S0/1/1). Потоки трафика будут определяться номерами портов в таблице NAT, поскольку было использовано ключевое слово **overload**.

```
R2(config)# ip nat inside source list 1 interface serial 0/1/1 overload
R2(config)# access-list 1 permit 192.168.0.0 0.0.255.255
R2(config)# interface serial0/1/0
R2(config-if)# ip nat inside
R2(config-if)# exit
R2(config)# interface Serial0/1/1
R2(config-if)# ip nat outside
```

<!-- 6.6.3 -->
## Настройка PAT с использованием пула адресов

Интернет-провайдер может выделить организации более одного публичного адреса IPv4. В этом случае организация может настроить PAT для использования пула публичных адресов IPv4 для преобразования.

Если объекту было выделено несколько публичных IPv4-адресов, то эти адреса могут быть частью пула, используемого PAT. Небольшой пул адресов распределяется между большим количеством устройств, при этом несколько хостов используют один и тот же публичный IPv4 адрес для доступа в Интернет. Чтобы настроить PAT для динамического пула адресов NAT, просто добавьте ключевое слово **overload** в **ip nat inside source** команду.

Топология для этого сценария повторяется на рисунке для удобства.

![](./assets/6.6.3.png)
<!-- /courses/ensa-dl/ae8e8c86-34fd-11eb-ba19-f1886492e0e4/aeb54e64-34fd-11eb-ba19-f1886492e0e4/assets/c63ebbf2-1c46-11ea-af56-e368b99e9723.svg -->

<!--
На рисунке изображен процесс преобразования адресов порта. Внутренняя сеть из двух ПК с PC1 по адресу 192.168.10.10 и PC2 по адресу 192.168.11.10, подключенных к маршрутизатору R1 на последовательном подключении S0/1/0 к маршрутизатору R2. На внешнем подключении к Интернету R2 у вас есть два сервера Svr1 по адресу 209.165.201.1 и Srvr2 по адресу 209.165.202.129. Существует таблица NAT с четырьмя столбцами: Внутренний локальный адрес, Внутренний глобальный адрес, Внешний локальный адрес и Внешний глобальный адрес. PC1 имеет внутренний локальный IP-адрес 192.168.10. 10:1444 сопоставлен с внутренним глобальным адресом 209.165.200. 225:1444. Внешний локальный IP-адрес — это адрес назначения 209.165.201. 1:80, сопоставленный с 209.165.201. 1:80. PC2 имеет внутренний локальный IP-адрес 192.168.11. 10:1444 сопоставлен с внутренним глобальным IP-адресом 209.165.200. 226:1445. Адрес назначения PC2s — внешний глобальный IP-адрес 209.165.202. 129:80 сопоставлен с внешним глобальным IP-адресом 209.165.202. 129:80
-->

В этом примере NAT-POOL2 привязан к ACL, чтобы разрешить преобразование 192.168.0.0/16. Эти узлы могут совместно использовать IPv4 адрес из пула, так как PAT включен с помощью ключевого слова **overload**.

```
R2(config)# ip nat pool NAT-POOL2 209.165.200.226 209.165.200.240 netmask 255.255.255.224
R2(config)# access-list 1 permit 192.168.0.0 0.0.255.255
R2(config)# ip nat inside source list 1 pool NAT-POOL2 overload
R2(config)# 
R2(config)# interface serial0/1/0
R2(config-if)# ip nat inside
R2(config-if)# exit
R2(config)# interface serial0/1/1
R2(config-if)# ip nat outside
R2(config-if)# end
R2#
```

<!-- 6.6.4 -->
## Анализ PAT - c ПК на сервер

Процесс преобразования NAT с перегрузкой является одинаковым как при использовании пула адресов, так и при использовании одного адреса. На этом рисунке PAT настроен на использование одного общедоступного адреса IPv4 вместо пула адресов. PC1 хочет взаимодействовать с веб-сервером Svr1. Одновременно другому клиенту, ПК 2, нужно установить аналогичный сеанс с веб-сервером Сервер 2. И для ПК 1, и для ПК 2 настроены частные IPv4-адреса, а на маршрутизаторе R2 включено преобразование PAT.

![](./assets/6.6.4.png)
<!-- /courses/ensa-dl/ae8e8c86-34fd-11eb-ba19-f1886492e0e4/aeb54e64-34fd-11eb-ba19-f1886492e0e4/assets/c63fa652-1c46-11ea-af56-e368b99e9723.svg -->

На рисунке показаны следующие шаги.

1.  Оба PC1 и PC2 отправляют пакеты на Svr1 и Svr2 соответственно. ПК 1 использует IPv4-адрес 192.168.10.10 и порт TCP источника 1444. ПК 2 использует IPv4-адрес 192.168.10.11 источника и, по случайному совпадению, тот же порт TCP источника — 1444.
2.  Пакет компьютера ПК 1 первым достигает маршрутизатора R2. Используя PAT, R2 изменяет IPv4-адрес источника на 209.165.200.225 (внутренний глобальный адрес). В таблице NAT отсутствуют другие устройства, использующие порт 1444, поэтому PAT сохраняет этот же номер порта. Затем пакет пересылается серверу Сервер 1 по адресу 209.165.201.1.
3.  Далее на маршрутизатор R2 приходит пакет с ПК 2. Настройка PAT обеспечивает использование для всех преобразований одного внутреннего глобального IPv4-адреса — 209.165.200.225. Аналогично процессу преобразования для ПК 1, PAT изменяет IPv4-адрес источника ПК 2 на внутренний глобальный адрес 209.165.200.225. Однако в этом пакете ПК 2 используется номер порта источника, уже содержащийся в текущей записи PAT, обеспечивающей преобразование для ПК 1. PAT увеличивает номер порта источника, пока его значение не окажется уникальным для данной таблицы. В данном случае записи порта источника в таблице NAT и пакету от ПК 2 назначается номер 1445.

<!--
На рисунке изображен анализ PAT от ПК к серверу. Внутренняя сеть из двух ПК с PC1 по адресу 192.168.10.10 и PC2 по адресу 192.168.11.10, подключенных к маршрутизатору R1 на последовательном подключении S0/1/0 к маршрутизатору R2. На внешнем подключении к Интернету R2 у вас есть два сервера Svr1 по адресу 209.165.201.1 и Srvr2 по адресу 209.165.202.129. Существует таблица NAT с четырьмя столбцами: Внутренний локальный адрес, Внутренний глобальный адрес, Внешний локальный адрес и Внешний глобальный адрес. PC1 имеет внутренний локальный IP-адрес 192.168.10. 10:1444 сопоставлен с внутренним глобальным адресом 209.165.200. 225:1444. Внешний локальный IP-адрес — это адрес назначения 209.165.201. 1:80, сопоставленный с 209.165.201. 1:80. PC2 имеет внутренний локальный IP-адрес 192.168.11. 10:1444 сопоставлен с внутренним глобальным IP-адресом 209.165.200. 226:1445. Адрес назначения PC2s — внешний глобальный IP-адрес 209.165.202. 129:80 сопоставлен с внешним глобальным IP-адресом 209.165.202. 129:80
-->

<!-- 6.6.5 -->
## Анализ PAT - с сервера к ПК

Хотя ПК 1 и ПК 2 используют одинаковый преобразованный адрес - внутренний глобальный адрес 209.165.200.225, и одинаковый номер порта источника — 1444, измененный номер порта для ПК 2 (1445) делает уникальной каждую запись в таблице NAT. Это становится очевидным при отправке серверами ответных пакетов клиентам, как показано на рисунке.

![](./assets/6.6.5.png)
<!-- /courses/ensa-dl/ae8e8c86-34fd-11eb-ba19-f1886492e0e4/aeb54e64-34fd-11eb-ba19-f1886492e0e4/assets/c64090b0-1c46-11ea-af56-e368b99e9723.svg -->

На втором рисунке шаги от серверов к ПК следующие:

4.  Серверы используют для обратного трафика порт источника из полученного пакета в качестве порта назначения и адрес источника — в качестве адреса назначения. Серверы ведут себя так, как если бы они взаимодействовали с одним узлом 209.165.200.225, однако это не так.
5.  Получив пакеты, маршрутизатор R2 находит уникальную запись в таблице NAT, используя адрес назначения и порт назначения каждого пакета. В случае получения пакета от сервера Сервер 1 адресу назначения IPv4 209.165.200.225 соответствует несколько записей, но только одна из них содержит порт назначения 1444. Используя эту запись таблицы, маршрутизатор R2 изменяет IPv4-адрес назначения пакета на 192.168.10.10. Изменение порта назначения в данном случае не требуется. Затем пакет пересылается компьютеру ПК 1.
6.  Получив пакет от сервера Сервер 2, маршрутизатор R2 выполняет аналогичное преобразование. Маршрутизатор снова находит адрес назначения IPv4 209.165.200.225 с несколькими записями. Однако, используя порт назначения 1445, R2 может уникально идентифицировать запись преобразования. IPv4-адрес назначения меняется на 192.168.10.11. В этом случае порт назначения также необходимо изменить обратно на первоначальное значение 1444, сохраненное в таблице NAT. Затем пакет пересылается компьютеру ПК 2.

<!--
На рисунке изображен анализ PAT от сервера к ПК. Внутренняя сеть из двух ПК с PC1 по адресу 192.168.10.10 и PC2 по адресу 192.168.11.10, подключенных к маршрутизатору R1 на последовательном подключении S0/1/0 к маршрутизатору R2. На внешнем подключении к Интернету R2 у вас есть два сервера Svr1 по адресу 209.165.201.1 и Srvr2 по адресу 209.165.202.129. Существует таблица NAT с четырьмя столбцами: Внутренний локальный адрес, Внутренний глобальный адрес, Внешний локальный адрес и Внешний глобальный адрес. PC1 имеет внутренний локальный IP-адрес 192.168.10. 10:1444 сопоставлен с внутренним глобальным адресом 209.165.200. 225:1444. Внешний локальный IP-адрес — это адрес назначения 209.165.201. 1:80, сопоставленный с 209.165.201. 1:80. PC2 имеет внутренний локальный IP-адрес 192.168.11. 10:1444 сопоставлен с внутренним глобальным IP-адресом 209.165.200. 226:1445. Адрес назначения PC2s — внешний глобальный IP-адрес 209.165.202. 129:80 сопоставлен с внешним глобальным IP-адресом 209.165.202. 129:80
-->

<!-- 6.6.6 -->
## Проверка PAT

Маршрутизатор R2 настроен на предоставление PAT клиентам из сети 192.168.0.0/16. Когда внутренние узлы выходят через маршрутизатор R2 в Интернет, выполняется преобразование их адресов в IPv4-адрес из пула PAT с уникальным номером порта источника.

Для проверки PAT используются те же команды, что и для проверки статического и динамического NAT, как показано в примере вывода. Команда **show ip nat translations** выводит преобразования для трафика от двух различных узлов к различным веб-серверам. Обратите внимание, что двум различным внутренним узлам выделяется один и тот же IPv4-адрес 209.165.200.226 (внутренний глобальный адрес). Для различения этих двух транзакций в таблице NAT используются номера портов источников.

```
R2# show ip nat translations
Pro Inside global          Inside local         Outside local      Outside global
tcp 209.165.200.225:1444  192.168.10.10:1444  209.165.201.1:80   209.165.201.1:80
tcp 209.165.200.225:1445  192.168.11.10:1444  209.165.202.129:80 209.165.202.129:80
R2#
```

Как показано в примере, команда **show ip nat statistics** позволяет проверить, что в пуле NAT-POOL2 выделен один адрес для обоих преобразований. В выходных данных команды содержатся сведения о количестве и типе активных преобразований, параметрах настройки NAT, количестве адресов в пуле и количестве выделенных адресов.

```
R2# show ip nat statistics 
Total active translations: 4 (0 static, 2 dynamic; 2 extended)
Peak translations: 2, occurred 00:31:43 ago
Outside interfaces:
  Serial0/1/1
Inside interfaces: 
  Serial0/1/0
Hits: 4  Misses: 0
CEF Translated packets: 47, CEF Punted packets: 0
Expired translations: 0
Dynamic mappings:
-- Inside Source
[Id: 3] access-list 1 pool NAT-POOL2 refcount 2
 pool NAT-POOL2: netmask 255.255.255.224
	start 209.165.200.225 end 209.165.200.240
	type generic, total addresses 15, allocated 1 (6%), misses 0
(output omitted)
R2#
```

<!-- 6.6.7 -->
## Packet Tracer - Настройка PAT

В рамках данного упражнения Packet Tracer необходимо решить следующие задачи:

* Часть 1: Настройка динамического NAT с перегрузкой
* Часть 2: Проверка динамического NAT с реализацией перегрузки
* Часть 3: Настройка PAT с помощью интерфейса
* Часть 4: Проверка реализации интерфейса PAT

[Настройка PAT (pdf)](./assets/6.6.7-packet-tracer---configure-pat-instructions.pdf)

[Настройка PAT (pka)](./assets/6.6.7-packet-tracer---configure-pat.pka)
