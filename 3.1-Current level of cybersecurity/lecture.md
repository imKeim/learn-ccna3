# Текущий уровень кибербезопасности

<!-- 3.1.1 -->
## Текущее состояние дел
Киберпреступники теперь обладают опытом и инструментами, необходимыми для уничтожения критически важной инфраструктуры и систем. Их инструменты и методы продолжают развиваться.

Киберпреступники переносят вредоносное ПО на беспрецедентный уровень сложности и воздействия. Они становятся более искусными в использовании методов скрытности и уклонения, чтобы скрыть свою деятельность. Наконец, киберпреступники используют незащищенные пробелы в безопасности.

Проникновения в безопасность сети могут нарушить электронную коммерцию, привести к потере бизнес-данных, поставить под угрозу конфиденциальность людей и целостность информации. Эти проникновения могут привести к потере доходов корпораций, краже интеллектуальной собственности, судебным искам и даже могут угрожать общественной безопасности.

Поддержание сетевой безопасности обеспечивает защиту пользователей сети и коммерческих интересов. Организациям нужны люди, которые могут распознать скорость и масштаб, с которым противники накапливают и совершенствуют свое кибер-оружие. Все пользователи должны знать термины безопасности, представленные в таблице.

| **Термины в сфере безопасности** | **Описание** |
| --- | --- |
| **Ресурсы** | Ресурс - это что-то ценное для организации. Он включает людей, оборудование, и данные. |
| **Уязвимость** | Уязвимость - это слабое место в системе или ее архитектуре, которое может быть использовано злоумышленниками. |
| **Угроза** | Угроза - это потенциальная опасность для ресурсов, данных или сетевых функций компании. |
| **Эксплойт** | Эксплойт - механизм для использования уязвимости в целях взлома ресурса. |
| **Устранение** | Устранение является контрмерой, которая уменьшает вероятность или серьезность потенциальной угрозы или риска. Сетевая безопасность включает в себя несколько методов уменьшения риска. |
| **Риски** | Риск - вероятность того, что определенная угроза выразится в использовании уязвимости ресурса и приведет к нежелательным для организации последствиям. Величину риска определяет вероятность возникновения события и его последствий. |

Ресурсы должны быть идентифицированы и защищены. Уязвимости должны быть устранены до того, как они станут угрозой и будут использованы. Техники по уменьшению риска необходимы до, во время и после атаки.

<!-- 3.1.2 -->
## Векторы сетевых атак
Вектор атаки – это путь (или какой-либо другой способ), по которому злоумышленник проникает на сервер, хост или в сеть. Большинство векторов атак идут извне корпоративной сети. Например, злоумышленники могут через Интернет нацелиться на сеть, чтобы прервать ее нормальную работу, и для этого создают атаку типа «отказ в обслуживании» (DoS).
External and Internal Threats

![](./assets/3.1.2.PNG)

**Примечание:** При DoS-атаке сеть становится неработоспособной и больше не может реагировать на запросы легитимных пользователей.

Внутренний пользователь, например сотрудник, может случайно или намеренно:

1. украсть и скопировать конфиденциальные данные на съемный носитель, в электронную почту, ПО для обмена сообщениями или в любую другую среду передачи данных;
2. скомпрометировать внутренние серверы или устройства сетевой инфраструктуры;
3. отключить критически важные сетевые подключения, что приведет к выходу сети из строя;
4. подключить инфицированный USB-диск к корпоративной вычислительной системе.

Ущерб, вызванный действиями внутренних пользователей, обладающих прямым доступом к зданию и его инфраструктуре, может оказаться значительно выше, чем от внешних угроз. Сотрудники также обладают информацией о своей корпоративной сети, ее ресурсах и конфиденциальных данных.

Специалисты по сетевой безопасности должны внедрять инструменты и техники для нейтрализации внешних и внутренних угроз.

<!-- 3.1.3 -->
## Потеря данных
Можно сказать, что данные – это наиболее ценный актив организации. Данные организации могут включать в себя данные исследований и разработок, данные продаж, финансовые данные, юридические и кадровые данные, данные о сотрудниках, подрядчиках и клиентах.

Под потерей или утечкой данных подразумевается намеренная или ненамеренная потеря, кража или утечка данных во внешний мир. Потеря данных может привести к следующим последствиям:

1. ущерб для бренда и репутации
2. потеря конкурентного преимущества
3. потеря заказчиков
4. потеря прибыли
5. разбирательства в суде/юридические последствия, которые могут привести к штрафам и административным санкциям
6. значительные затраты и усилия по уведомлению пострадавших сторон и восстановлению после утечки

В таблице представлены общие векторы, характерные для потери данных.

| **Векторы потери данных** | **Описание** |
| --- | --- |
| **Электронная почта/социальные сети** | Перехваченные электронные письма или мгновенные сообщения могут быть захвачены и таким образом будет раскрыта конфиденциальная информация. |
| **Незашифрованные устройства** | Если для хранения данных не используется алгоритм шифрования, то злоумышленник может получить доступ к ценным конфиденциальным данным. |
| **Устройства облачного хранения данных** | Конфиденциальные данные могут быть потеряны, если доступ к облаку будет скомпрометирован вследствие слабых настроек безопасности. |
| **Съемные носители** | Одним из рисков также является то, что сотрудник может несанкционированным образом скопировать данные на USB-накопитель. Другой риск заключается в возможной потере USB-накопителя с ценными корпоративными данными. |
| **Бумажные носители** | Конфиденциальные данные должны быть уничтожены, когда они больше не нужны. |
| **Некорректное управление доступом** | Украденные или ненадежные пароли, которые были скомпрометированы, могут предоставить злоумышленнику простой доступ к корпоративным данным. |

Специалисты по сетевой безопасности должны защищать данные организации. Необходимо внедрять различные техники предотвращения потери данных (Data Loss Prevention, DLP), которые бы включали в себя стратегические, операционные и тактические задачи.

<!-- 3.1.4 -->
## Проверьте свои знания текущего состояния кибербезопасности

<!-- остался квиз 3.1.4 -->