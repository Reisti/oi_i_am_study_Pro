# Настроить EIGRP named-mode для IPv4 и IPv6 в офисе С.-Петербург.
##  Задание:

 1. В офисе С.-Петербург настроить EIGRP.
 2. R32 получает только маршрут по умолчанию.
 3. R16-17 анонсируют только суммарные префиксы
 4. Использовать EIGRP named-mode для настройки сети.
  



## Топология:
- **AS 2042**: С.-Петербург
  ![Топология](image1.png)

## Адресация: Устройств Используемых в данном Примере

#### Таблица адресации сетевых устройств "С.-Петербург (AS 2042)":
| Устройство    | Интерфейс    | IP-адресс          |
|--------------:|:-------------|-------------------:|
| R16           | loopback     | 10.21.37.8/32      | 
| R16           | e0/0.21      | 10.21.14.1/29      | 
| R16           | e0/1.22      | 10.21.14.129/29    | 
| R16           | e0/2.24      | 10.21.14.193/29    | 
| R16           | e0/2.12      | 10.21.144.33/26    | 
| R16           | e0/3.23      | 10.21.14.65/29     | 
| R17           | loopback     | 10.21.37.9/32      | 
| R17           | e0/0.24      | 10.21.14.194/29    | 
| R17           | e0/1.23      | 10.21.14.66/29     | 
| R17           | e0/2.12      | 10.21.144.34/26    | 
| R17           | e0/2.21      | 10.21.14.2/29      | 
| R18           | loopback     | 10.21.37.10/32     | 
| R18           | e0/0.22      | 10.21.14.130/29    | 
| R18           | e0/1.23      | 10.21.14.67/29     | 
| R18           | e0/2.24      | 10.21.16.14/30     | 
| R18           | e0/3.21      | 10.21.16.45/30     | 
| R32           | loopback     | 10.21.37.11/32     | 
| R32           | e0/0.23      | 10.21.14.68/29     | 
| SW9           | Vlan 37      | 10.37.2.2/24       | 
| SW9           | Vlan 24      | 10.21.14.196/29    | 
| SW10          | Vlan 37      | 10.37.2.3/24       | 
| SW10          | Vlan 21      | 10.21.14.4/29      | 
| VPC8          | Vlan 12      | 10.21.144.35/26    | 
| VPC           | Vlan 12      | 10.21.144.36/26    |  
  

## Принятые решения

| Параметр | Значение | Обоснование |
|:---------|:---------|:------------|
| Режим EIGRP | named-mode, процесс `SPB` | Требование задания 4 |
| Номер AS | 2042 | AS офиса С.-Петербург |
| Router-ID | адрес loopback | Стабильный идентификатор, удобен при диагностике |
| `passive-interface default` | включён | Соседства только на нужных интерфейсах |
| Суммаризация R16, R17 | `10.21.14.0/24`, `10.21.144.0/24`, `10.21.37.0/24` | Требование задания 3 |
| Маршрут по умолчанию для R32 | `summary-address 0.0.0.0 0.0.0.0` на `e0/3.23` R16 | Требование задания 2 |
| Внешние линки R18 (`10.21.16.x/30`) | не входят в EIGRP | Не попадают под `network`, интерфейсы пассивные |
| Коммутаторы SW9, SW10 | EIGRP не используется | Работают на L2, SVI только для управления |

## Конфигурация

### [R16]

```
router eigrp SPB
 address-family ipv4 unicast autonomous-system 2042
  af-interface default
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/0.21
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/1.22
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/2.24
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/2.12
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/3.23
   no passive-interface
   summary-address 0.0.0.0 0.0.0.0
  exit-af-interface
  !
  topology base
  exit-af-topology
  network 10.21.14.0 0.0.0.255
  network 10.21.144.0 0.0.0.255
  network 10.21.37.8 0.0.0.0
  eigrp router-id 10.21.37.8
 exit-address-family
```

### [R17]  
   
```
router eigrp SPB
 address-family ipv4 unicast autonomous-system 2042
  af-interface default
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/0.24
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/1.23
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/2.12
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  af-interface Ethernet0/2.21
   no passive-interface
   summary-address 10.21.14.0 255.255.255.0
   summary-address 10.21.144.0 255.255.255.0
   summary-address 10.21.37.0 255.255.255.0
  exit-af-interface
  !
  topology base
  exit-af-topology
  network 10.21.14.0 0.0.0.255
  network 10.21.144.0 0.0.0.255
  network 10.21.37.9 0.0.0.0
  eigrp router-id 10.21.37.9
 exit-address-family
```

### [R18]

```
router eigrp SPB
 address-family ipv4 unicast autonomous-system 2042
  af-interface default
   passive-interface
  exit-af-interface
  af-interface Ethernet0/0.22
   no passive-interface
  exit-af-interface
  af-interface Ethernet0/1.23
   no passive-interface
  exit-af-interface
  !
  topology base
  exit-af-topology
  network 10.21.14.0 0.0.0.255
  network 10.21.37.10 0.0.0.0
  eigrp router-id 10.21.37.10
 exit-address-family
```

### [R32]

Входящий prefix-list служит дополнительной защитой: даже при появлении других соседей R32 примет только маршрут по умолчанию.

```
ip prefix-list ONLY-DEFAULT seq 5 permit 0.0.0.0/0

router eigrp SPB
 address-family ipv4 unicast autonomous-system 2042
  af-interface default
   passive-interface
  exit-af-interface
  af-interface Ethernet0/0.23
   no passive-interface
  exit-af-interface
  !
  topology base
   distribute-list prefix ONLY-DEFAULT in Ethernet0/0.23
  exit-af-topology
  network 10.21.14.64 0.0.0.7
  network 10.21.37.11 0.0.0.0
  eigrp router-id 10.21.37.11
 exit-address-family
```

## Назначение основных команд

| Команда | Назначение |
|:--------|:-----------|
| `router eigrp SPB` | Создаёт процесс EIGRP в named-mode (имя локально, с соседями не согласуется) |
| `address-family ipv4 unicast autonomous-system 2042` | Включает семейство IPv4 и задаёт номер AS (должен совпадать у соседей) |
| `af-interface default` + `passive-interface` | Делает все интерфейсы пассивными: нет Hello и соседств |
| `af-interface <имя>` + `no passive-interface` | Включает соседства на нужном интерфейсе |
| `summary-address <сеть> <маска>` | Анонсирует на интерфейс суммарный префикс вместо специфичных маршрутов |
| `summary-address 0.0.0.0 0.0.0.0` | Подавляет все маршруты, остаётся только default (для R32) |
| `topology base` | Базовая топология, в ней задаются фильтры и метрики |
| `distribute-list prefix ... in` | Фильтрует входящие маршруты по prefix-list |
| `network <адрес> <wildcard>` | Включает EIGRP на интерфейсах, адреса которых попадают в диапазон |
| `eigrp router-id` | Фиксирует идентификатор роутера |

## Проверка

```
show eigrp address-family ipv4 neighbors
show ip eigrp topology
show ip route eigrp
show running-config | section eigrp
```

Ожидаемый результат:

- Между R16, R17, R18 и R32 установлены EIGRP-соседства.
- На R32 в таблице EIGRP только `D* 0.0.0.0/0`.
- На R18 присутствуют суммарные маршруты `10.21.14.0/24`, `10.21.144.0/24` и `10.21.37.0/24`.
- На R16 и R17 созданы суммарные маршруты с выходом на `Null0` (AD 5).
- Связность между VPC8 и VPC в VLAN 12 сохраняется.

## Результаты проверки

### R32: только маршрут по умолчанию (задание 2) — выполнено

```
R32#show eigrp address-family ipv4 neighbors
0   10.21.14.65             Et0/0.23

R32#show ip route eigrp
Gateway of last resort is 10.21.14.65 to network 0.0.0.0
D*    0.0.0.0/0 [90/1024640] via 10.21.14.65, Ethernet0/0.23
```

Единственный сосед R32 — R16. В таблице EIGRP только маршрут по умолчанию.

### R16 и R17: суммарные префиксы (задание 3) — выполнено

На R16 и R17 созданы суммарные маршруты на `Null0`:

```
R16#show ip route eigrp
D*    0.0.0.0/0 is a summary, Null0
D        10.21.14.0/24 is a summary, Null0
D        10.21.37.0/24 is a summary, Null0
D        10.21.144.0/24 is a summary, Null0

R17#show ip route eigrp
D        10.21.14.0/24 is a summary, Null0
D        10.21.37.0/24 is a summary, Null0
D        10.21.144.0/24 is a summary, Null0
```

R18 получает от R16 и R17 только суммарные `10.21.14.0/24`, `10.21.37.0/24` и `10.21.144.0/24`, по два равнозначных пути (ECMP). Отдельные /29, /26 и /32 R16 и R17 на R18 не попадают:

```
R18#show ip route eigrp
D        10.21.14.0/24 [90/1536000] via 10.21.14.129, Ethernet0/0.22
                       [90/1536000] via 10.21.14.66, Ethernet0/1.23
D        10.21.37.0/24 [90/1024640] via 10.21.14.129, Ethernet0/0.22
                       [90/1024640] via 10.21.14.66, Ethernet0/1.23
D        10.21.144.0/24 [90/1536000] via 10.21.14.129, Ethernet0/0.22
                         [90/1536000] via 10.21.14.66, Ethernet0/1.23
```

[R16]: conf/base_conf16.md 
[R17]: conf/base_conf17.md  
[R18]: conf/base_conf18.md 
[R32]: conf/base_conf32.md  

