# *Demo2025 - Модуль 1*

### **[Задание](https://github.com/trichh-ayou/instruction/blob/main/%D0%9A%D0%9E%D0%94%2009.02.06-1-2025%20%D0%A2%D0%BE%D0%BC%201%20(%D1%81%D0%BE%D0%BA%D1%80).pdf)**

#

### Содержание

1. **[Произведите базовую настройку устройств](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)**

2. **[Настройка ISP](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2)**
  
3. **[Создание локальных учетных записей](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-3)**
  
4. **[Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-4)**
   
5. **[Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)**
  
6. **[Между офисами HQ и BR необходимо сконфигурировать IP-туннель](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-6)**

7. **[Обеспечьте динамическую маршрутизацию](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-7)**

8. **[Настройка динамической трансляции адресов](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-8)**

9. **[Настройка протокола динамической конфигурации хостов](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-9)**

10. **[Настройка DNS для офисов HQ и BR](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-10)**

11. **[Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-11)**

<br/>

<br/>

<p align="center">
  ![image](https://github.com/user-attachments/assets/b4717a91-da11-457f-8fff-40d00362571c)

<p\>
<p align="center"><strong>Топология</strong></p>

<br/>

## Задание 1

### Произведите базовую настройку устройств

- Настройте имена устройств согласно топологии. Используйте полное доменное имя

- На всех устройствах необходимо сконфигурировать IPv4

- IP-адрес должен быть из приватного диапазона, в случае, если сеть локальная, согласно RFC1918

- Локальная сеть в сторону HQ-SRV(VLAN100) должна вмещать не более 64 адресов

- Локальная сеть в сторону HQ-CLI(VLAN200) должна вмещать не более 16 адресов

- Локальная сеть в сторону BR-SRV должна вмещать не более 32 адресов

- Локальная сеть для управления(VLAN999) должна вмещать не более 8 адресов

- Сведения об адресах занесите в отчёт, в качестве примера используйте Таблицу 3

<br/>

<details>
<summary>Решение</summary>
<br/>

**Полное доменное имя можно посмотреть в таблице для [Задания 10](https://github.com/trichh-ayou/instruction/blob/main/module1/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-10)**

<br/>

#### Настройка имен устройств на ALT Linux
```yml
hostnamectl set-hostname isp && exec bash
hostnamectl set-hostname hq-rtr.au-team.irpo && exec bash
hostnamectl set-hostname br-rtr.au-team.irpo && exec bash
hostnamectl set-hostname hq-srv.au-team.irpo && exec bash
hostnamectl set-hostname hq-cli.au-team.irpo && exec bash
hostnamectl set-hostname br-srv.au-team.irpo && exec bash
```
---

#### Диапазоны IP-адресов по RFC1918

| Диапазон             | CIDR           | Количество адресов | Пример диапазона                  |
|----------------------|----------------|--------------------|-----------------------------------|
| Класс A              | 10.0.0.0/8     | 16 777 216         | 10.0.0.0 – 10.255.255.255           |
| Класс B              | 172.16.0.0/12  | 1 048 576          | 172.16.0.0 – 172.31.255.255          |
| Класс C              | 192.168.0.0/16 | 65 536             | 192.168.0.0 – 192.168.255.255        |

---

#### Разделение IP-адресов по VLAN

| VLAN ID | Назначение      | Сеть         | Маска | Количество адресов | Диапазон IP-адресов            |
|---------|-----------------|--------------|-------|--------------------|--------------------------------|
| 100     | Офис HQ-SRV     | 192.168.100.0 | /26   | 64                 | 192.168.10.0 – 192.168.10.63    |
| 200     | Офис HQ-CLI     | 192.168.200.0 | /28   | 16                 | 192.168.20.0 – 192.168.20.15    |
| 999     | Сеть управления | 192.168.99.0 | /29   | 8                  | 192.168.99.0 – 192.168.99.7     |

---

#### Адресация и шлюзы для настройки ISP

| Подключение         | Сеть           | IP-адрес (устройство)    | IP-адрес (ISP)   | Шлюз по умолчанию (для устройства внутри сети) |
|---------------------|----------------|--------------------------|------------------|-------------------------------------------------|
| HQ-RTR – ISP        | 172.16.4.0/28  | 172.16.4.2 (HQ-RTR)      | 172.16.4.1       | 172.16.4.2                                      |
| BR-RTR – ISP        | 172.16.5.0/28  | 172.16.5.2 (BR-RTR)      | 172.16.5.1       | 172.16.5.2                                      |

---

#### Табличка адресов ip 
| Имя              | IP                               | Шлюз         |
|------------------|-----------------------------------|--------------|
| ISP-HQ           | 172.16.4.2/28                     | 172.16.4.1/28 |
| ISP-BR           | 172.16.5.2/28                     | 172.16.5.1/28 |
| HQ-RTR (VLAN100)  | 192.168.100.1/26                 | 192.168.100.1 | 
| HQ-RTR (VLAN200)  | 192.168.200.1/29                 | 192.168.200.1 |
| HQ-RTR (VLAN999)  | 192.168.99.1/29                  | 192.168.99.1 | 
| HQ-CLI           | 192.168.200.2/29                  | 192.168.20.1/29 |
| HQ-SRV           | 192.168.100.2/26, 192.168.99.2/29 | 192.168.10.1/26, 192,168,99,1/29 |
| BR-RTR           | 192.168.0.1/27                    | 172.16.5.2/28 |
| BR-SRV           | 192.168.0.62/27                   | 192.168.0.1/27 |

https://jodies.de/ipcalc - ip-калькулятор

![image](https://github.com/user-attachments/assets/da181112-1d6d-4da9-bc8c-7bacc63d12d5)

---

<br/>

#### Наcтройка IP-адресации на устройствах

Приводим файлы **`options`**, **`ipv4address`**, **`ipv4route`**, **`resolv.conf`** в директории **`/etc/net/ifaces/*имя интерфейса*/`** к следующему виду:

---

### 1)ISP

### /etc/net/ifacec/ens192
> **`options`**
```yml
BOOTPROTO=dhcp
TYPE=eth
DISABLED=no
CONFIG_IPV4=yes
```
---

### /etc/net/ifacec/ens224
> **`options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```
> **`ipv4address`**
```yml
172.16.4.1/28
```
---

### /etc/net/ifacec/ens256
> **`options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
172.16.5.1/28
```
---

Отредактируйте файл `/etc/net/sysctl.conf`:

Измените строку:
```yml
net.ipv4.ip_forward = 0
```
на:
```yml
net.ipv4.ip_forward = 1
```
Примените изменения:
```yml
systemctl restart network
```
---

### NAT

```yml
iptables -t nat -A POSTROUTING -o ens192 -s 172.16.4.0/28 -j MASQUERADE
iptables -t nat -A POSTROUTING -o ens192 -s 172.16.5.0/28 -j MASQUERADE
```
```yml
iptables-save > /etc/sysconfig/iptables
systemctl enable --now iptables
```
---
### 2)HQ-RTR

### /etc/net/ifacec/ens192
> **`options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```
> **`ipv4address`**
```yml
172.16.4.2/28
```

> **`ipv4route`**
```yml
default via 172.16.4.1
```

> **`resolv.conf`**
```yml
nameserver 77.88.8.8
```
---

### /etc/net/ifacec/ens224.100
> **`options`**
```yml
TYPE=vlan
HOST=ens224
VID=100
DISABLED=no
BOOTPROTO=static
ONBOOT=yes
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
192.168.100.1/26
```
---

### /etc/net/ifacec/ens224.999
> **`options`**
```yml
TYPE=vlan
HOST=ens224
VID=999
DISABLED=no
BOOTPROTO=static
ONBOOT=yes
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
192.168.99.1/29
```
---

### /etc/net/ifacec/ens256.200
> **`options`**
```yml
TYPE=vlan
HOST=ens224
VID=200
DISABLED=no
BOOTPROTO=static
ONBOOT=yes
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
192.168.200.1/28
```
---

Отредактируйте файл `/etc/net/sysctl.conf`:

Измените строку:
```yml
net.ipv4.ip_forward = 0
```
на:
```yml
net.ipv4.ip_forward = 1
```
Примените изменения:
```yml
systemctl restart network
```
---

### NAT

```yml
iptables -t nat -A POSTROUTING -o ens192 -s 192.168.200.1/28 -j MASQUERADE
iptables -t nat -A POSTROUTING -o ens192 -s 192.168.99.1/29 -j MASQUERADE
iptables -t nat -A POSTROUTING -o ens192 -s 192.168.100.1/26 -j MASQUERADE
```
```yml
iptables-save > /etc/sysconfig/iptables
systemctl enable --now iptables
```
---

### 3)BR-RTR

### /etc/net/ifacec/ens192
> **`options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
172.16.5.2/28
```

> **`ipv4route`**
```yml
default via 172.16.5.1
```

> **`resolv.conf`**
```yml
nameserver 77.88.8.8
```
---

### /etc/net/ifacec/ens224
> **`options`**
```yml
DISABLED=no
TYPE=eth
BOOTPROTO=static
CONFIG_IPV4=yes
```

> **`ipv4address`**
```yml
192.168.0.1/27
```
---

Отредактируйте файл `/etc/net/sysctl.conf`:

Измените строку:
```yml
net.ipv4.ip_forward = 0
```
на:
```yml
net.ipv4.ip_forward = 1
```
Примените изменения:
```yml
systemctl restart network
```
---
### NAT

```yml
iptables -t nat -A POSTROUTING -o ens192 -s 192.168.0.0/27 -j MASQUERADE
```
```yml
iptables-save > /etc/sysconfig/iptables
systemctl enable --now iptables
```
---
</details>

<br/>

## Задание 2

### Настройка ISP

- Настройте адресацию на интерфейсах:

  - Интерфейс, подключенный к магистральному провайдеру, получает адрес по DHCP

  - Настройте маршруты по умолчанию там, где это необходимо

  - Интерфейс, к которому подключен HQ-RTR, подключен к сети 172.16.4.0/28

  - Интерфейс, к которому подключен BR-RTR, подключен к сети 172.16.5.0/28

  - На ISP настройте динамическую сетевую трансляцию в сторону HQ-RTR и BR-RTR для доступа к сети Интернет

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка интерфейса, который получает IP-адрес по DHCP

Файл **`options`** (в директории интерфейса) приводим к следующему виду:
```yml
BOOTPROTO=dhcp
TYPE=eth
DISABLED=no
CONFIG_IPV4=yes
```
> **`BOOTPROTO=dhcp`** - заменили статический способ настройки адреса на динамическое получение

<br/>

#### Настройка маршрута по умолчанию

Прописываем шлюз по умолчанию:
```yml
default via *адрес шлюза*
```

<br/>

#### Настройка интерфейсов, смотрящих в сторону HQ-RTR и BR-RTR происходит аналогично настройке в [Задании 1](https://github.com/damh66/demo2025/tree/main/module1#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)

<br/>

#### Включение маршрутизации

В файле **`/etc/net/sysctl.conf`** изменяем строку:
```yml
net.ipv4.ip_forward = 1
```

<br/>

Изменения в файле **`sysctl.conf`** применяем следующей командой:
```yml
sysctl -p /etc/sysctl.conf
```

</details>

<br/>

## Задание 3

### Создание локальных учетных записей

- Создайте пользователя sshuser на серверах HQ-SRV и BR-SRV

  - Пароль пользователя sshuser с паролем P@ssw0rd

  - Идентификатор пользователя 1010

  - Пользователь sshuser должен иметь возможность запускать sudo без дополнительной аутентификации.

- Создайте пользователя net_admin на маршрутизаторах HQ-RTR и BR-RTR

  - Пароль пользователя net_admin с паролем P@$$word

  - При настройке на EcoRouter пользователь net_admin должен обладать максимальными привилегиями

  - При настройке ОС на базе Linux, запускать sudo без дополнительной аутентификации

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание пользователя `sshuser` на серверах

Создаем самого пользователя:
```yml
useradd sshuser -u 1010
```
> опция **`-u`** позволяет указать идентификатор пользователя сразу при создании

<br/>

Задаем пароль:
```yml
passwd sshuser
```

<br/>

Добавляем в группу **wheel**:
```yml
usermod -aG wheel sshuser
```

<br/>

Добавляем строку в **`/etc/sudoers`**:
```yml
sshuser ALL=(ALL) NOPASSWD:ALL
```
> Позволяет запускать **sudo** без аутентификации 

<br/>

#### Создание пользователя `net_admin` на Ecorouter

Создаем самого пользователя:
```yml
username net_admin
```

<br/>

Задаем пароль:
```yml
password P@ssw0rd
```

<br/>

Присваиваем привилегии администратора:
```yml
role admin
```


</details>

<br/>

## Задание 4

### Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор

- Сервер HQ-SRV должен находиться в ID VLAN 100
- Клиент HQ-CLI в ID VLAN 200
- Создайте подсеть управления с ID VLAN 999
- Основные сведения о настройке коммутатора и выбора реализации разделения на VLAN занесите в отчёт

<br/>

<details>
<summary>Не решено</summary>
<br/>



</details>

<br/>

## Задание 5

### Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV

- Для подключения используйте порт 2024
- Разрешите подключения только пользователю sshuser
- Ограничьте количество попыток входа до двух
- Настройте баннер «Authorized access only»

<br/>

<details>
<summary>Решение</summary>
<br/>

Приводим указанные строки в файле **`/etc/openssh/sshd_config`** к следующим значениям:
```yml
Port 2024
MaxAuthTries 2
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
```
> В параметре **AllowUsers** вместо пробела используется **`Tab`**

<br/>

Создаем файл **`bannermotd`**:
```yml
----------------------
Authorized access only
----------------------
```

<br/>

Перезагружаем службу:
```yml
systemctl restart sshd
```

</details>

<br/>

## Задание 6

### Между офисами HQ и BR необходимо сконфигурировать IP-туннель

- Сведения о туннеле занесите в отчёт

- На выбор технологии GRE или IP in IP

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание туннеля на HQ-RTR

Создаем интерфейс **GRE**-туннеля на **HQ-RTR**:
```yml
int tunnel.0
```

<br/>

Назначаем **IP-адрес**:
```yml
ip add 172.16.0.1/30
```

<br/>

Выставляем параметр **MTU**:
```yml
ip mtu 1400
```
> В связи с добавлением служебного заголовка появляются новые требования к допустимому значению MTU при передаче пакета. Заголовок GRE имеет размерность 4 байта, 20 байт транспортный IP заголовок, заголовок IP пакета 20 байт, таким образом возникает необходимость задавать размер допустимого MTU на интерфейсах туннеля меньше стандартного значения.

<br/>

Задаем режим работы туннеля **GRE** и адреса **начала** и **конца** туннеля:
```yml
ip tunnel 172.16.4.2 172.16.5.2 mode gre
```

<br/>

#### GRE-туннель на BR-RTR настраивается аналогично примеру выше

</details>

<br/>

## Задание 7

### Обеспечьте динамическую маршрутизацию: ресурсы одного офиса должны быть доступны из другого офиса. Для обеспечения динамической маршрутизации используйте link state протокол на ваше усмотрение

- Разрешите выбранный протокол только на интерфейсах в ip туннеле

- Маршрутизаторы должны делиться маршрутами только друг с другом

- Обеспечьте защиту выбранного протокола посредством парольной защиты

- Сведения о настройке и защите протокола занесите в отчёт

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка OSPF на HQ-RTR

Создаем процесс **OSPF**, указываем **идентификатор маршрутизатора**, объявляем сети и указываем **пассивные** интерфейсы:
```yml
router ospf 1
  router-id 1.1.1.1
  network 172.16.0.0/30 area 0
  network 192.168.100.0/26 area 0
  network 192.168.200.0/28 area 0
  passive-interface default
  no passive-interface tunnel.0
```

<br/>

#### Маршрутизация OSPF на BR-RTR настраивается аналогично примеру выше

</details>

<br/>

## Задание 8

### Настройка динамической трансляции адресов

- Настройте динамическую трансляцию адресов для обоих офисов.

- Все устройства в офисах должны иметь доступ к сети Интернет

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка NAT на ISP

Добавляем правила **`iptables`** на ISP
```yml
iptables -t nat -A POSTROUTING -o ens224 -s 172.16.4.0/28 -j MASQUERADE
iptables -t nat -A POSTROUTING -o ens224 -s 172.16.5.0/28 -j MASQUERADE
```

<br/>

Сохраняем правила:
```yml
iptables-save > /etc/sysconfig/iptables
```

<br/>

Включаем и добавляем **`iptables`** в автозагрузку:
```yml
systemctl enable --now iptables
```

<br/>

#### Настройка NAT на HQ-RTR

Указываем **внутренние** и **внешние** интерфейсы:
```yml
int int1
  ip nat inside
!
int int2
  ip nat inside
!
int int0
  ip nat outside
```

<br/>

Создаем пул:
```yml
ip nat pool NAT_POOL 192.168.100.1-192.168.100.62,192.168.200.1-192.168.200.14
```

<br/>

Создаем **правило** трансляции адресов, указывая внешний интерфейс:
```yml
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
```

<br/>

#### Настройка NAT на BR-RTR

Конфигурация:
```yml
int int1
  ip nat inside
!
int int0
  ip nat outside
!
ip nat pool NAT_POOL 192.168.0.1-192.168.0.30
!
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
```

</details>

<br/>

## Задание 9

### Настройка протокола динамической конфигурации хостов

- Настройте нужную подсеть

- Для офиса HQ в качестве сервера DHCP выступает маршрутизатор HQ-RTR.

- Клиентом является машина HQ-CLI.

- Исключите из выдачи адрес маршрутизатора

- Адрес шлюза по умолчанию – адрес маршрутизатора HQ-RTR.

- Адрес DNS-сервера для машины HQ-CLI – адрес сервера HQ-SRV.

- DNS-суффикс для офисов HQ – au-team.irpo

- Сведения о настройке протокола занесите в отчёт

<br/>

<details>
<summary>Решение</summary>
<br/>

Создаем **пул** для **DHCP-сервера**:
```yml
ip pool hq-cli 192.168.200.14-192.168.200.14
```

<br/>

Настраиваем сам **DHCP-сервер**:
```yml
dhcp-server 1
  pool hq-cli 1
    mask 28
    gateway 192.168.200.1
    dns 192.168.100.62
    domain-name au-team.irpo
```
> **`pool hq-cli 1`** - привязка **пула**

> **`mask 28`** - указание **маски** для выдаваемых адресов из пула

> **`gateway 192.168.200.1`** - указание **шлюза по умолчанию** для клиентов

> **`dns 192.168.100.62`** - указание **DNS-сервера** для клиентов

> **`domain-name au-team.irpo`** - указание **DNS-суффикса** для офиса **HQ**

<br/>

Привязываем **DHCP-сервер** к интерфейсу (смотрящий в сторону **CLI**):
```yml
interface int2
  dhcp-server 1
```

</details>

<br/>

## Задание 10

### Настройка DNS для офисов HQ и BR

- Основной DNS-сервер реализован на HQ-SRV.

- Сервер должен обеспечивать разрешение имён в сетевые адреса устройств и обратно в соответствии с таблицей 2

- В качестве DNS сервера пересылки используйте любой общедоступный DNS сервер

<br/>

<table align="center">
  <tr>
    <td align="center">Устройство</td>
    <td align="center">Запись</td>
    <td align="center">Тип</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">hq-rtr.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">br-rtr.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-SRV</td>
    <td align="center">hq-srv.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">HQ-CLI</td>
    <td align="center">hq-cli.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-SRV</td>
    <td align="center">br-srv.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">moodle.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">wiki.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
</table>

<p align="center"><strong>Таблица 2</strong></p>

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка конфигурации bind

Устанавливаем необходимые пакеты:
```yml
apt-get install -y bind bind-utils
```

<br/>

Изменяем содержание перечисленных строк в **`/etc/bind/options.conf`** к следующему виду:
```yml
listen-on { 127.0.0.1; 192.168.100.62; };

forwarders { 77.88.8.8; };

allow-query { 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };

```
> **`listen-on`** - сетевые интерфейсы, которые будет прослушивать служба
>
> **`forwarders`** - DNS-сервер, на который будут перенаправляться запросы клиентов
>
> **`allow-query`** - IP-адреса и подсети от которых будут обрабатываться запросы

<br/>

Конфигурируем ключи **rndc**:
```yml
rndc-confgen > /etc/rndckey
```
> Делаем вывод в файл, чтобы скопировать оттуда

<br/>

Приводим файл **`/etc/bind/rndc.key`** к следующему виду:
```yml
//key "rndc-key" {
//  secret "@RNDC_KEY@";
//};

key "rndc-key" {
  algorithm hmac-sha256;
  secret "VTmhjyXFDo0QpaBl3UQWx1e0g9HElS2MiFDtNQzDylo=";
};
```
> Первые строки закомментировали
>
> Вставили ключ **rndc**

<br/>

Проверяем на ошибки:
```yml
named-checkconf
```

<br/>

Запускаем и добавляем в автозагрузку **`bind`**:
```yml
systemctl enable --now bind
```

<br/>

Изменяем **`resolv.conf`** интерфейса:
```yml
search au-team.irpo
nameserver 127.0.0.1
nameserver 192.168.100.62
nameserver 77.88.8.8
search yandex.ru
```

<br/>

#### Создание и настройка прямой зоны

Прописываем ее в **`/etc/bind/local.conf`**:
```yml
zone "au-team.irpo" {
  type master;
  file "au-team.irpo.db";
};
```

<br/>

Копируем шаблон прямой зоны:
```yml
cp /etc/bind/zone/localdomain /etc/bind/zone/au-team.irpo.db
```

<br/>

Задаем пользователя и права на файл:
```yml
chown named. /etc/bind/zone/au-team.irpo.db
chmod 600 /etc/bind/zone/au-team.irpo.db
```

<br/>

Приводим его к следующему виду:
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
        IN      A       192.168.100.62
hq-rtr  IN      A       192.168.100.1
br-rtr  IN      A       192.168.0.1
hq-srv  IN      A       192.168.100.62
hq-cli  IN      A       192.168.200.14
br-srv  IN      A       192.168.0.30
moodle  IN      CNAME   hq-rtr
wiki    IN      CNAME   hq-rtr
```

<br/>

Проверяем на ошибки:
```yml
named-checkconf -z
```

<br/>

#### Создание и настройка обратных зон

Прописываем их в **`/etc/bind/local.conf`**:
```yml
zone "100.168.192.in-addr.arpa" {
  type master;
  file "100.168.192.in-addr.arpa";
};

zone "200.168.192.in-addr.arpa" {
  type master;
  file "200.168.192.in-addr.arpa";
};

zone "0.168.192.in-addr.arpa" {
  type master;
  file "0.168.192.in-addr.arpa";
};
```

<br/>

Копируем шаблон обратной зоны:
```yml
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/100.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/200.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/0.168.192.in-addr.arpa
```

<br/>

Задаем пользователя и права на файл:
```yml
chown named. /etc/bind/zone/100.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/100.168.192.in-addr.arpa
chown named. /etc/bind/zone/200.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/200.168.192.in-addr.arpa
chown named. /etc/bind/zone/0.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/0.168.192.in-addr.arpa
```

<br/>

Приводим их к следующему виду:
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
1       IN      PTR     hq-rtr.au-team.irpo.
62      IN      PTR     hq-srv.au-team.irpo.
```
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
14      IN      PTR     hq-cli.au-team.irpo.
```
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
1      IN      PTR      br-rtr.au-team.irpo.
30     IN      PTR      br-srv.au-team.irpo.
```

<br/>

Проверяем на ошибки:
```yml
named-checkconf -z
```

<br/>

Перезапускаем **`bind`**:
```yml
systemctl restart bind
```

<br/>

Проверяем работоспособность:
```yml
nslookup **IP-адрес/DNS-имя**
```

</details>

<br/>

## Задание 11

### Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка часового пояса на Alt Linux

Меняем часовой пояс следующей командой:
```yml
timedatectl set-timezone Asia/Yekaterinburg
```

<br/>

Проверяем:
```yml
timedatectl status
```

<br/>

#### Настройка часового пояса на EcoRouter

Прописываем команду:
```yml
ntp timezone utc+5
```

<br/>

Проверяем:
```yml
show ntp timezone
```

</details>
