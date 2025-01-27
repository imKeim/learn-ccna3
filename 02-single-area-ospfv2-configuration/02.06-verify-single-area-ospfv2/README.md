<!-- 2.6.1 -->
## Проверка соседних устройств OSPF

Если вы настроили OSPFv2 для одной области, вам необходимо проверить свои конфигурации. В этом разделе подробно описаны многие команды, которые можно использовать для проверки OSPF.

Особенно полезны для проверки маршрутизации следующие команды:

* **show ip interface brief** – проверяет, что необходимые интерфейсы активны с правильной IP-адресацией;
* **show ip route** – проверяет, что таблица маршрутизации содержит все ожидаемые маршруты.

Дополнительные команды для определения того, что OSPF работает должным образом, включают следующие:

* **show ip ospf neighbor** 
* **show ip protocols** 
* **show ip ospf** 
* **show ip ospf interface** 

На рисунке показана эталонная топология OSPF, используемая для демонстрации этих команд.

**Топология OSPFv2**

![](./assets/2.6.1.svg)
<!-- /courses/ensa-dl/ae8e6570-34fd-11eb-ba19-f1886492e0e4/aeb3a0b0-34fd-11eb-ba19-f1886492e0e4/assets/c5c0d962-1c46-11ea-af56-e368b99e9723.svg -->

<!--
стандартная топология сети OSPFv2, используемая в этом модуле, как описано в 2.1.1
-->

Используйте команду **show ip ospf neighbor**, чтобы убедиться, что роутер сформировал отношения смежности с соседними устройствами. Если идентификатор соседнего роутера не отображается, или его состояние не FULL, то между ними не установлены отношения смежности OSPFv2.

Если два устройства не установили отношения смежности, обмен данными о состоянии канала не осуществляется. Неполное заполнение баз данных состояний каналов может привести к появлению ошибочных деревьев кратчайших путей SPF и таблиц маршрутизации. Указанные маршруты к сетям назначения могут отсутствовать или быть неоптимальными.

**Примечание**. Роутер, не являющийся DR или BDR, имеющий связь с другим устнойством, не DR или BDR, будет отображать двустороннюю смежность вместо полной.

В следующих выходных данных команды отображается таблица соседей R1.

```
R1# show ip ospf neighbor 
Neighbor ID     Pri   State           Dead Time   Address         Interface
3.3.3.3           0   FULL/  -        00:00:19    10.1.1.13       GigabitEthernet0/0/1
2.2.2.2           0   FULL/  -        00:00:18    10.1.1.6        GigabitEthernet0/0/0
R1#
```

Для каждого соседнего устройства данная команда отображает следующие выходные данные:

* **neighbor ID** – идентификатор соседнего устройства;
* **pri** – приоритет интерфейса OSPFv2, используется при выборе DR и BDR;
* **state** – состояние интерфейса OSPFv2. Состояние FULL означает, что данный и соседний устройства имеют одинаковые базы данных состояния каналов OSPFv2. В сетях с множественным доступом (например, Ethernet) состояние двух смежных роутеров, может отображаться как 2WAY. Тире указывает, что использование в данном типе сети DR или BDR не требуется;
* **dead time** – время, в течение которого роутер ожидает получения пакета приветствия OSPFv2 перед тем, как объявить соседнее устройство неработающим. Оно сбрасывается при получении интерфейсом пакета приветствия;
* **address** – IPv4-адрес интерфейса соседнего устройства, к которому напрямую подключен роутер; 
* **interface** – интерфейс, на котором роутер установил отношения смежности с соседним устройством.

Два устройства могут устанавливать отношения смежности OSPFv2 при следующих условиях:

* маски подсети не совпадают, в связи с чем роутеры находятся в разных сетях;
* таймеры приветствия или простоя OSPFv2 не совпадают;
* типы сетей OSPFv2 не совпадают;
* команда OSPFv2 **network** отсутствует или содержит ошибки.

<!-- 2.6.2 -->
## Проверка настроек протокола OSPF

Команда **show ip protocols** — быстрый способ проверки важнейшей информации о конфигурации OSPF, включающей:

- идентификатор процесса OSPFv2;
- идентификатор устройства;
- сети, объявляемые роутером;
- соседние устройства, от которых роутер получает обновления;
- административное расстояние по умолчанию, равное 110 для протокола OSPF.

```
R1# show ip protocols
*** IP Routing is NSF aware ***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 1.1.1.1
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Routing Information Sources:
    Gateway         Distance      Last Update
    3.3.3.3              110      00:09:30
    2.2.2.2              110      00:09:58
  Distance: (default is 110)
R1#
```

<!-- 2.6.3 -->
## Проверка информации о процессе OSPF

Команду **show ip ospf** можно также использовать для проверки идентификаторов процесса и роутера в протоколе OSPFv2, как показано на рис. 1. Она отображает данные области OSPFv2 и показывает время последнего расчета алгоритма SPF.

```
R1# show ip ospf      
 Routing Process "ospf 10" with ID 1.1.1.1
 Start time: 00:01:47.390, Time elapsed: 00:12:32.320
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Supports Database Exchange Summary List Optimization (RFC 5243)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 EXCHANGE/LOADING adjacency limit: initial 300, process maximum 300
 Number of external LSA 1. Checksum Sum 0x00A1FF
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 10000 mbps
    Area BACKBONE(0)
        Number of interfaces in this area is 3
	Area has no authentication
	SPF algorithm last executed 00:11:31.231 ago
	SPF algorithm executed 4 times
	Area ranges are
	Number of LSA 3. Checksum Sum 0x00E77E
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
R1#
```

<!-- 2.6.4 -->
## Проверка настроек интерфейса OSPF

Подробный список для каждого интерфейса, где включен OSPFv2, показывает команда **show ip ospf interface**. Укажите интерфейс для отображения параметров только этого интерфейса, как показано в следующих выходных данных для Gigabit Ethernet 0/0/0. Команда показывает идентификатор процесса, идентификатор локального роутера, тип сети, стоимость OSPF, сведения о DR и BDR на многоканальных каналах (не показаны) и соседних соседях.

```
R1# show ip ospf interface GigabitEthernet 0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 10.1.1.5/30, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 1.1.1.1, Network Type POINT_TO_POINT, Cost: 10
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           10        no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State POINT_TO_POINT
  Timer intervals configured, Hello 5, Dead 20, Wait 20, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:01
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/2/2, flood queue length 0
  Next 0x0(0)/0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 1, Adjacent neighbor count is 1 
    Adjacent with neighbor 2.2.2.2
  Suppress hello for 0 neighbor(s)
R1#
```

Чтобы получить краткое описание интерфейсов с поддержкой OSPFv2, используйте команду **show ip ospf interface brief**, как показано в следующем выводе команды. Она полезна для просмотра важных сведений, включая следующие:

* интерфейсы, участвующие в OSPF;
* сети, которые объявляются (IP-адреса/маски);
* стоимость каждого канала;
* состояние сети;
* количество соседей по каждому каналу.

```
R1# show ip ospf interface brief
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Lo0          10    0               10.10.1.1/24       10    P2P   0/0
Gi0/0/1      10    0               10.1.1.14/30       30    P2P   1/1
Gi0/0/0      10    0               10.1.1.5/30        10    P2P   1/1
R1#
```

<!-- 2.6.5 -->
<!-- syntax -->

