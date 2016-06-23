

## mikrotik RouterOS

![Mikrotik Cloud Core Router](https://i.ytimg.com/vi/EL6IxslKiHs/maxresdefault.jpg)

###### from latvia with love

---

## Что такое Mikrotik
Маленькая латвийская фирма производящая сетевое оборудование для небольших интернет провайдеров. До недавнего времени специализировались на Wi-Fi оборудовании. 

Их устройства популярны в малом и среднем бизнесе из-за очень хорошего соотношения цены  к предоставляемым возможностям. Все устройства работают под управлением Mikrotik RouterOS либо Mikrotik SwitchOS (модификация RouterOS).

[http://www.mikrotik.com](http://www.mikrotik.com/)
---
## RouterOS
  * Основана на ядре Linux 3.3+
  * Устанавливается на все роутеры Mikrotik, может быть установлена на x86 компьютере или сервере. Распространяется также образ для применения в качестве виртуального роутера внутри виртуальной машины. [Прошивки и образы](http://www.mikrotik.com/download)
  * RouterOS 7 - это как Half-Life 3

В целом это довольно своеобразная, но удобная надстройка над Linux и userspace утилитами для управления сетью.

---
## [Веб интерфейс](http://wiki.mikrotik.com/wiki/Manual:Webfig "Фиговый лист")

  * Поддерживает нескучные скины
  * Позволяет сделать почти все путем тыканья мышкой
  * Наглядно показывает структуру всех меню

<img src="http://www.servethehome.com/wp-content/uploads/2015/02/MikroTik-CRS226-WebFig-600x514.jpg" alt="Drawing" style="width: 100%;">

---
## CLI

Все настройки представлены в виде иерархических меню. С уровнями иерархии или конечными объектами можно выполнять действия, например, показать все маршруты в таблице маршрутизации:
```bash
johnny@cr1.b08.warp.local] > ip route print
Flags: X - disabled, A - active, D - dynamic, 
C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme, 
B - blackhole, U - unreachable, P - prohibit 
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0 A S  0.0.0.0/0                          10.100.100.106            1
 1 ADb  1.0.4.0/24                         194.226.195.1            20
 2  Db  1.0.4.0/24                         194.226.194.1            20
 3 ADb  1.0.5.0/24                         194.226.195.1            20
 4  Db  1.0.5.0/24                         194.226.194.1            20
 5 ADb  1.0.6.0/24                         194.226.195.1            20
 6  Db  1.0.6.0/24                         194.226.194.1            20
 7 ADb  1.0.7.0/24                         194.226.195.1            20
```
___
## CLI
#####(Примеры)
Выключить BGP соседа:
```bash
routing bgp peer disable CCR-b06
```
Показать логи в кратком виде
```bash
[johnny@cr1.b08.warp.local] > log print terse 
...
16:54:25 dhcp,debug,packet     ciaddr = 10.10.80.81 
16:54:25 dhcp,debug,packet     yiaddr = 10.10.80.81 
16:54:25 dhcp,debug,packet     siaddr = 10.1.53.101 
16:54:25 dhcp,debug,packet     chaddr = 94:DE:80:8A:9E:50 
16:54:25 dhcp,debug,packet     file = "boot\x86\wdsnbp.com" 
16:54:25 dhcp,debug,packet     Msg-Type = ack 
16:54:25 dhcp,debug,packet     Server-Id = 10.10.80.1 
```

___
## CLI
##### (Примеры)

Удалить файрвольные правила с 7 по 70:
```bash
ip firewall filter remove 7,8,9,10,11,12,13,14,15,16,17,18,19,
20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,
41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,
62,63,64,65,66,67,68,69,70
```

Пропищать отрывок имперского марша:
```bash
:beep frequency=500 length=500ms;
:delay 500ms;
:beep frequency=500 length=500ms;
:delay 500ms;
:beep frequency=500 length=500ms;
:delay 500ms;
:beep frequency=400 length=500ms;
:delay 400ms;
:beep frequency=600 length=200ms;
:delay 100ms;
:beep frequency=500 length=500ms;
:delay 500ms;
:beep frequency=400 length=500ms;
:delay 400ms;
:beep frequency=600 length=200ms;
:delay 100ms;
:beep frequency=500 length=500ms;
:delay 1000ms;
:beep frequency=750 length=500ms;
:delay 500ms;
:beep frequency=750 length=500ms;
:delay 500ms;
:beep frequency=750 length=500ms;
:delay 500ms;
:beep frequency=810 length=500ms;
:delay 400ms;
:beep frequency=600 length=200ms;
:delay 100ms;
:beep frequency=470 length=500ms;
:delay 500ms;
:beep frequency=400 length=500ms;
:delay 400ms;
:beep frequency=600 length=200ms;
:delay 100ms;
:beep frequency=500 length=500ms;
:delay 1000ms;
```

---
## CLI
##### пояснение структуры команд
Выполнение команды определенного уровня иерархии без указания действия переводит консоль в указанный уровень, аналогично тому как работает команда cd:
```bash
[johnny@cr1.b08.warp.local] > routing bgp 
[johnny@cr1.b08.warp.local] /routing bgp> 

```

Дальнейшие команды выполняются относительно текущего уровня иерархии:
```bash
[johnny@cr1.b08.warp.local] /routing bgp> peer print 
Flags: X - disabled, E - established 
 #   INSTANCE        REMOTE-ADDRESS                                 REMOTE-AS  
 0 E RUNNet          194.226.194.1                                  3267       
 1 E RUNNet          194.226.195.1                                  3267       
 2 E RUNNet          10.100.100.106                                 60928     
```

___
## CLI
##### пояснение структуры команд
Возврат на уровень выше:
```bash
[johnny@cr1.b08.warp.local] /routing bgp> ..
[johnny@cr1.b08.warp.local] /routing> 
```

Для большинства элементов иерархии доступен вот такой набор команд:
```bash
[johnny@cr1.b08.warp.local] > ip address 
add  comment  disable  edit  enable  export  find  print  remove  set

```

___
## CLI
##### пояснение структуры команд
  * **`add`** добавление объекта иерархии (адреса, файрвольного правила и т.п.)
  * **`set`** изменение или установка неопределенного значения атрибута объекта. Например, переброс файрвольного правила из одной цепочки в другую
  * **`enable/disable`** включение или выключение объекта, например, ip адреса
  * **`export`** экспорт объекта в виде команд которые нужно ввести чтобы привести его к текущему состоянию

---
## CLI
##### основные принципы работы CLI RouterOS
  * Работают дополнения команд по **tab** и вывод подсказок по знаку **?**
  * Все изменения применяются **сразу же**. Есть безопасный режим и возможность сокращения команд как в Cisco (см. вертикальный слайд ниже)
  * Print работает одновременно и как функция нумерации выводимых объектов (см. второй вложенный вертикальный слайд)
  * Нет, *^ядь, диапазонов. При необходимости менять много элементов их нужно перечислять через запятую.

___
## CLI
##### режимы Safe и HotLock

* **Режим Safe.** Поскольку команды применяются сразу же, чтобы избежать ошибок сделающих роутер недоступным существует безопасный режим. Он включается по нажатию **ctrl+X**. Если ssh/telnet сессия рвется, введенные команды отменяются. Отменить введенные в этом режиме команды можно также вручную нажав **ctrl+F**
* **Режим HotLock.** Позволяет писать команды не полностью, а в произвольно-сокращенном виде, RouterOS сама дописывает слова.

___
## CLI
##### print
  * Print выводит список объектов в данном уровне иерархии. Например:
```bash
[johnny@cr1.b08.warp.local] > ip route print
...
27  Db  1.0.160.0/19                       194.226.194.1            20
28 ADb  1.0.160.0/21                       46.29.76.153            200
29 ADb  1.0.168.0/21                       46.29.76.153            200
30 ADb  1.0.176.0/20                       46.29.76.153            200
```

___
## CLI
##### PRINT

  * Вывод можно фильтровать используя ключевое слово where:
```bash
[johnny@cr1.b08.warp.local] > ip route print where gateway=46.29.76.153
Flags: X - disabled, A - active, D - dynamic, 
C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme, 
B - blackhole, U - unreachable, P - prohibit 
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0 ADb  1.0.144.0/20                       46.29.76.153            200
 1 ADb  1.0.160.0/21                       46.29.76.153            200
 2 ADb  1.0.168.0/21                       46.29.76.153            200
 3 ADb  1.0.176.0/20                       46.29.76.153            200
```

___
##CLI
#####PRINT
* Выводимые номера объектов относительные. Выборка нумеруется каждый раз начиная с нуля. Например, один и тот же маршрут в двух print выводится под разными номерами: 
```bash
29 ADb  1.0.168.0/21                       46.29.76.153            200
 2 ADb  1.0.168.0/21                       46.29.76.153            200
```

* То есть, **print** нумерует элементы которые выводит в консоль и после этого к элементам можно обращаться по этим номерам. Важно помнить какой номер имел объект в последний раз.

---

## CLI
##### Команды add и set
* **Add** добавляет новый объект. При создании можно сразу указать все нужные атрибуты объекта.

```bash
[johnny@cr1.b08.warp.local] > ip address add  
address=192.168.1.107/24  interface=eth8 comment="Nyan ^_^"  

[johnny@cr1.b08.warp.local] > routing ospf instance add 
router-id=192.168.1.107 name="slowpoke-ospf"

[johnny@cr1.b08.warp.local] > routing ospf network add 
area=backbone network=192.168.1.0/24
```

___
## CLI
##### Команды add и set
  * Set работает аналогично команде add. Указывать можно номер объекта, либо его имя. Здесь указан номер **1**:

```bash
[johnny@cr1.b08.warp.local] > routing ospf instance set 
comment="My comment" 1
```

---
## Пример.
##### Простой OSPF роутер
[DHT ссылка на торрент с OVA файлом виртуальной машины](magnet:?xt=urn:btih:41a615507cba4f7ce7a8920bae1f08b979d6a912&dn=mikrotik.ova&tr=udp%3A%2F%2F192.168.1.1%3A6969)

   * Задаем имя роутера:						 

```bash 
[admin@MikroTik] > system identity set name=johnny-slowpoke
[admin@johnny-slowpoke] > 
```

   * Добавляем себе пользователя и отключаем стандартного admin:                                          

```bash 
[admin@johnny-slowpoke] > user add name=johnny group=full 
password="vjqk.,bvsqhf xjr"  
[johnny@johnny-slowpoke] > user disable admin
```

___

## Пример.
##### Простой OSPF роутер

* Включаем ssh, смотрим свой адрес и заходим на роутер с хостовой системы:                                          
```bash 
[johnny@johnny-slowpoke] > ip service enable ssh
[johnny@johnny-slowpoke] > ip address print      
Flags: X - disabled, I - invalid, D - dynamic 
 #   ADDRESS            NETWORK         INTERFACE                              
 0 D 192.168.1.246/24   192.168.1.0     ether1  
```

* Создаем пустой bridge интерфейс с выдуманным адресом, он будет имитировать сеть доступную только через вас:

```bash
[johnny@johnny-slowpoke] > interface bridge add name=slow-bridge disabled=no
[johnny@johnny-slowpoke] > ip address add address=172.29.100.5/24 
interface=slow-bridge
```

___
## Пример.
##### Простой OSPF роутер

*  Создаем OSPF процесс:

```bash
[johnny@johnny-slowpoke] > routing ospf instance add 
name=slow-ospf router-id=192.168.1.246 
redistribute-connected=as-type-1 disabled=no
```

* Создаем  новую OSPF зону:
```bash
```
