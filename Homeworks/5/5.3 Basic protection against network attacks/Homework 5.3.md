## Домашнее задание к занятию "Основные средства защиты от сетевых атак на коммутаторах."  

---

### Задание 1. 

На картинке изображена схема офисной сети:
![image](https://user-images.githubusercontent.com/51816695/160147812-5bd15814-762e-4cec-b27e-e8a601f461da.png)

Каким образом необходимо настроить все 4 свитча, чтобы в сети корректно работал только один DHCP сервер - маршрутизатор R1.
Очень важна корректная конфигурация портов на всех свитчах.

*Перечислите список свитчей и список команд, которые необходимо выполнить.*

### Ответ.  

На всех свитчах дать команду `ip dhcp snooping` для глобального включения опции.  
А так же отключаем опцию 82 `no ip dhcp snooping information option`.  
Далее на портах каждого коммутатора, "смотрящих" в сторону DHCP:  
SW1
```
interface g1/1  
ip dhcp snooping trust
```
SW2
```
interface g0/0  
ip dhcp snooping trust
```
SW3
```
interface g0/2  
ip dhcp snooping trust
```
SW4
```
interface g0/1  
ip dhcp snooping trust
```
---  

### Задание 2. 

По топологии из задания 1 необходимо на SW2 настроить ARP Inspection и IP Source guard для Client9 и Client10, подключенных к SW2.
Client9 получает адрес по DHCP, Client10 ip адрес задан статически. DHCP Snooping уже настроен по первому заданию.

*Перечислите список команд, которые необходимо применить на SW2*

### Ответ.  

Включить DAI на vlan `ip arp inspection vlan <..>`, а также на интерфейсах g0/0, g0/2, g0/1 коммутатора SW2 дать команду `ip arp inspection trust`.   
В глобальной конфигурации SW2 можно включить опцию проверки mac-адреса, например источника `ip arp inspection validate src-mac`.  
Для клиентов со статическими настройками сети создаем ACL:  
````
arp access-list DAI
permit ip host <client ip> mac host <client mac>
````
Или настроить Source Guard:  
```
ip source binding <client mac> <client vlan> <client ip> interface Gi1/0
```

