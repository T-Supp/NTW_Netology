## Домашнее задание к занятию "Преобразование сетевых адресов (NAT)"

---

### Лабораторная работа "Настройка статического NAT и PAT overload"

Схема сети 
![image](https://user-images.githubusercontent.com/5977962/163477371-1c6c0142-91c6-4133-890d-06125107db9d.png)

Настройки оборудования:

- 1841 telnet server  
loopback0	10.10.10.10/32  
Fastethernet0/0	192.168.1.10/24  
ip route 0.0.0.0 0.0.0.0 192.168.1.1
- PC  
Fastethernet0	192.168.1.11/24  
ip route 0.0.0.0 0.0.0.0 192.168.1.1

- NAT-Router  
Fastethernet0/0	192.168.1.1/24  
Fastethernet0/1	8.8.8.1/24  

- Internet-router  
Fastethernet0/0	8.8.8.8/24  


Перенесите топологию в PT, настройте оборудование по предложенным данным. 
#### Важно!  
На маршрутизаторе Internet-router для нужной работы сети роутинг настраивать не нужно.  

-----

### Задание 1. 

Настроить PAT overload для всех внутренних хостов LAN через внешний интерфейс маршрутизатора NAT-Router. С хостов должен пинговаться 8.8.8.8.

*В качестве ответа приложите вывод команды "sh run" с маршрутизатора NAT-Router.*

------

### Задание 2. 

Обеспечьте доступ с Internet-router к telnet-server(10.10.10.10) по протоколу telnet, не настраивая маршрутизацию на Internet-router. Доступ из LAN к 8.8.8.8 должен сохраниться.

*В качестве ответа приложите вывод команды "sh run" с маршрутизатора NAT-Router.*

### Ответ на задания 1 и 2.  


<details>  
<summary>Вывод конфигурации</summary>  

sh run  
Building configuration...  

Current configuration : 940 bytes  
!  
version 12.4  
no service timestamps log datetime msec  
no service timestamps debug datetime msec  
no service password-encryption  
!  
hostname 1841_NAT-Router  
!  
!  
!  
!  
!  
!  
!  
!  
ip cef  
no ipv6 cef  
!  
!  
!  
!  
!  
!  
!  
!  
!  
!  
!  
!  
spanning-tree mode pvst  
!    
!  
!  
!  
!  
!  
int erface FastEthernet0/0  
 ip address 192.168.1.1 255.255.255.0  
 ip nat inside  
 duplex auto  
 speed auto  
!  
interface FastEthernet0/1  
 ip address 8.8.8.1 255.255.255.0  
 ip nat outside  
 duplex auto  
 speed auto  
!  
interface Vlan1  
 no ip address  
 shutdown  
!  
ip nat inside source list NAT-TO-ISP interface FastEthernet0/1 overload  
ip nat inside source static tcp 10.10.10.10 23 8.8.8.1 23   
ip classless    
ip route 10.10.10.0 255.255.255.0 FastEthernet0/0 2  
ip route 0.0.0.0 0.0.0.0 8.8.8.8   
!  
ip flow-export version 9  
!  
!  
ip access-list extended NAT-TO-ISP  
 permit ip 192.168.1.0 0.0.0.255 any  
 permit ip 10.10.10.0 0.0.0.255 any  
!  
!  
!  
!  
!  
!  
line con 0  
!  
line aux 0  
!  
line vty 0 4  
 login  
!  
!  
!  
end  

<details>  
