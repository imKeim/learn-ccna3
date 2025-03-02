<!-- 13.6.2 -->
## Облачные вычисления

Облачные вычисления предполагают наличие большого числа подключенных через сеть компьютеров, которые физически могут размещаться в любой точке земного шара. Облачные вычисления помогают сократить операционные расходы за счет более эффективного использования ресурсов. Облачные вычисления решают различные проблемы управления данными:

* повсеместный доступ к данным организации в любое время;
* оптимизпция IT-операций организации, из-за подписок только на необходимые услуги;
* исключение или снижение необходимости развертывания и обслуживания IT-оборудования в местах эксплуатации;
* сокращение затрат на оборудование и электроэнергию, уменьшение требований к материальной части и потребности в обучении персонала;
* оперативное реагирование на рост требований к обработке больших объемов данных.

Три основные службы облачных вычислений, определенные Национальным институтом стандартов и технологий (NIST): 

* программное обеспечение как услуга (SaaS); 
* платформа как услуга (PaaS); 
* инфраструктура как услуга (IaaS). 

С SaaS поставщик облачных сервисов отвечает за доступ к онлайн-приложениям и услугам, таким как электронная почта, обмен данными или Office 365. 

С PaaS поставщик облачных сервисов отвечает за доступ к средствам разработки и сервисам, используемым для предоставления приложений. 

С IaaS поставщик облачных сервисов отвечает за предоставление IT-менеджерам доступа к сетевому оборудованию, виртуализированным сетевым сервисам и поддержке сетевой инфраструктуры. 

Четыре типа облаков: 

* публичные — приложения и сервисы доступны неограниченному кругу лиц; 
* частные — приложения и сервисы доступны сотрудникам определенного предприятия или организации; 
* гибридные — состоят из двух или более отдельных облаков, связанных в рамках единой архитектуры; 
* облака сообщества — создаются для исключительного использования определенным сообществом. 

## Виртуализация

Многие путают «облачные вычисления» и «виртуализацию». Виртуализация — основа облачных вычислений. Она отделяет операционную систему от аппаратного обеспечения. 

Исторически корпоративные серверы состояли из серверной операционной системы, установленной на специфическое аппаратное обеспечение. Оперативная память, процессорная мощность и дисковое пространство выделялись для предоставляемых сервисов. При сбое на каком-либо компоненте предоставляемый этим сервером сервис становится недоступным. Это называется конфигурацией с единой точкой отказа. Другая проблема с выделенными серверами в том, что часто они подолгу простаивают, ожидаязапрос. Это тратит энергию и ресурсы (развал серверов). 

Виртуализация снижает затраты, поскольку требуется меньше оборудования, энергии и места. Она обеспечивает простое создание прототипов, быструю подготовку серверов, дольшую безотказную работу сервера, улучшенное аварийное восстановление и поддержку устаревших компонентов. 

Компьютерная система состоит из следующих уровней абстракции: 
* сервисы, 
* ОС, 
* микропрограммы, 
* оборудование. 

Гипервизоры типа 1 устанавливаются непосредственно на физическом сервере или сетевом оборудовании. Гипервизор типа 2 — это программное обеспечение, которое создает и обеспечивает работу экземпляров виртуальных машин. Он может быть установлен поверх ОС или между прошивкой и ОС. Гипервизор типа 2 — это программное обеспечение, которое создает и обеспечивает работу экземпляров виртуальных машин.

## Инфраструктура виртуальной сети

В гипервизорах типа 1 используется подход bare metal (без ОС). Он называется так потому, что гипервизор устанавливается непосредственно на аппаратную часть. У гипервизоров типа 1 прямой доступ к аппаратным ресурсам. Они оказываются эффективнее размещенных архитектур и улучшают масштабируемость, производительность и отказоустойчивость. 

Для управления гипервизорами типа 1 требуется «консоль управления». Управляющее ПО позволяет управлять несколькими серверами, использующими один гипервизор. Консоль управления может автоматически объединять, включать и выключать серверы по мере необходимости. Консоль управления обеспечивает восстановление после аппаратного сбоя. Некоторые консоли управления также позволяют серверу настраивать переподписку ресурсов. 

Виртуализация серверов скрывает серверные ресурсы (например, количество и идентификаторы физических серверов, процессоров и ОС) от пользователей. В этом случае могут возникать проблемы, если центр обработки данных использует традиционные сетевые архитектуры. Другая проблема в том, что потоки трафика значительно отличаются от традиционной модели типа «клиент-сервер». Обычно в центре обработки данных имеется значительный объем трафика, которым обмениваются виртуальные серверы. Эти потоки называются движением «Восток-Запад» и могут изменяться в местоположении и интенсивности с течением времени. Трафик «Север-Юг» происходит между распределением и основным уровнями и обычно предназначен для удаленных местоположений, таких как другой центр обработки данных, другие поставщики облачных услуг или Интернет.

## Программно-определяемые сети

Для поддержки виртуализации сети разработали сетевые архитектуры: 

* программно-определяемая сеть (SDN),
* Cisco Application Centric Infrastructure (ACI). 

SDN — это метод удаленного программирования сетей. Компоненты SDN могут включать OpenFlow, OpenStack и другие. Контроллер SDN — логическая сущность, которая позволяет сетевым администраторам определять, как уровень передачи данных на коммутаторах и маршрутизаторах будет обрабатывать сетевой трафик. Сетевое устройство содержит уровень управления и передачи данных. 

* **Уровень управления** — «мозг» устройства. Принимает решения о пересылке данных. Содержит механизмы пересылки уровня 2 и уровня 3. Передаваемые данные обрабатываются ЦП. 
* **Уровень передачи данных** (пересылки) — коммутационная структура, которая связывает разные сетевые порты на устройстве. На каждом устройстве используется для пересылки потоков трафика. 

Маршрутизаторы и коммутаторы используют данные уровня управления для пересылки входящего трафика на соответствующий выходной интерфейс. Информация в плоскости данных обычно обрабатывается специальным процессором плоскости данных без участия ЦП. 

Технология Cisco Express Forwarding (CEF) использует уровень управления и уровень передачи данных для обработки пакетов. Обеспечивает пересылку пакетов на уровне передачи данных без обращения к уровню управления. 

SDN — разделение плоскости управления и плоскости данных. Для виртуализации сети с каждого устройства удаляется функция уровня управления, которую начинает исполнять один централизованный контроллер. Централизованный контроллер передает команды уровня управления каждому устройству. Уровень управления отвечает за управление устройством через его подключение к сети. 

Сетевые администраторы используют такие приложения, как Secure Shell (SSH), Trivial File Transfer Protocol (TFTP), Secure FTP и Secure Hypertext Transfer Protocol (HTTPS) для доступа к уровню управления и настройки устройства. Такие протоколы, как SNMP, используют уровень управления.

## Контроллеры

Контроллер SDN — это логическая сущность, которая позволяет сетевым администраторам определять, как уровень передачи данных на коммутаторах и маршрутизаторах будет обрабатывать сетевой трафик. Контроллер SDN определяет потоки данных между централизованным уровнем управления и уровнями передачи данных на отдельных маршрутизаторах и коммутаторах. 

Каждый из потоков, проходящих по сети, сначала должен получить разрешение от контроллера SDN, который проверяет, разрешен ли такой обмен данными в соответствии с сетевыми политиками. Если контроллер разрешает поток, он рассчитывает для него маршрут и добавляет запись для этого потока в каждом из коммутаторов на пути. Контроллер заполняет таблицы потоков, а коммутаторы ими управляют. Таблица потоков сопоставляет входящие пакеты с определенными потоками и указывает функции, которые необходимо выполнить над пакетами. Возможно наличие нескольких таблиц потоков, которые работают как конвейер. Таблица потоков может направлять поток в таблицу групп, которая может запускать различные действия, влияющие на один или несколько потоков. Таблица счетчиков используется для запуска различных действий, связанных с производительностью потока, включая возможность ограничения скорости трафика. 

Компания Cisco разработала ориентированную на приложения инфраструктуру (ACI), чтобы решать задачи более современными и инновационными способами, чем основаные на SDN. Архитектура Cisco ACI — это специализированное аппаратное решение для интеграции облачных вычислений и управления ЦОД. На верхнем уровне элемент управления политиками сети удаляется из уровня передачи данных. Это упрощает создание сетей центра обработки данных. 

Основные компоненты архитектуры ACI: 
* ANP, 
* APIC, 
* коммутаторы Cisco Nexus серии 9000. 

Структура Cisco ACI состоит из контроллера APIC и коммутаторов Cisco Nexus серии 9000, использующих двухуровневую топологию «ствол и листья». В отличие от SDN, контроллер APIC напрямую не управляет каналом данных. Вместо этого APIC обеспечивает централизованное хранение определений политик и программирует листовые коммутаторы на пересылку трафика с учетом определенных политик. 

Существует три базовых типа контроллеров SDN: 
* SDN на основе устройств — устройства программируются приложениями, работающими на самом устройстве или на сервере в сети;
* SDN на базе контроллера — используется централизованный контроллер, который знает обо всех устройствах в сети; 
* SDN на основе политик — аналогичны сетям SDN на основе контроллера, но включают дополнительный уровень политик, который работает на более высоком уровне абстракции. 

SDN на базе политик — наиболее надежный тип, предоставляющий простой механизм контроля и управления политиками во всей сети. Cisco APIC-EM — пример SDN на базе политик. Cisco APIC-EM предоставляет единый интерфейс для управления сетью, включая обнаружение и доступ к списку устройств и хостов, просмотр топологии, трассировку пути между конечными точками и настройку политик. APIC-EM Path Trace позволяют администратору легко визуализировать потоки трафика и обнаруживать любые конфликтующие, дублированные или теневые записи ACL. Этот инструмент исследует конкретные ACL-списки на пути между двумя конечными узлами и показывает все возможные неполадки.

<!-- 13.6.3 -->
<!-- quiz -->

