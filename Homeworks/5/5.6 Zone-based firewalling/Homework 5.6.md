## Домашнее задание к занятию "Межсетевое экранирование на основе зон, stateful/stateless packet inspection"

---

### Лабораторная работа  

Лабораторная работа заключается в настройке МСЭ компании. ЛВС логически разделена на пользовательскую подсеть, подсеть принтеров и подсеть с сервером DMZ. Для каждой из этих зон расписаны правила доступа в соседние.
Схема сети 
![image](https://user-images.githubusercontent.com/5977962/168447439-471d693b-2748-40a5-82c8-97f502243f19.png)


Настройки оборудования:

![image](https://user-images.githubusercontent.com/5977962/168447553-09a16892-4961-4f9f-ba0a-364fce364c5d.png)

Перенесите топологию в PT, настройте оборудование по предложенным данным. 

-----

### Задание 

От службы безопасности были переданы требования для ограничения сетевого доступа между различными подсетями:

1) Разрешить прохождение только ICMP трафика из INSIDE в OUTSIDE, в обратную сторону разрешить ответный трафик
2) Разрешить прохождение только HTTP-трафика из INSIDE в DMZ, в обратную сторону разрешить ответный трафик
3) Разрешить прохождение только ICMP-трафика из INSIDE в PRINTER, в обратную сторону разрешить ответный трафик
4) Из OUTSIDE разрешить инициировать сессии в DMZ по 80 TCP порту, в INSIDE и PRINTER разрешить только ответные пакеты
5) Из PRINTER запретить инициировать трафик во все остальные зоны
6) Из DMZ разрешить инициировать трафик в OUTSIDE по ICMP, в INSIDE и PRINTER разрешить только ответные пакеты

Необходимо, используя полученные знания о межсетевом экранировании на основе зон, stateful и stateless инспекции, сконфигурировать эти правила на МСЭ и выполнить проверку средствами Packet tracer.

### Ответ  

<details>  
<summary>Конфигурация МСЭ</summary>  

ciscoasa(config)#sh run

ASA Version 9.6(1)  
!  
hostname ciscoasa  
domain-name reboot  
names  
!  
interface GigabitEthernet1/1  
 nameif INSIDE  
 security-level 100  
 ip address 192.168.1.1 255.255.255.0  
!  
interface GigabitEthernet1/2  
 nameif OUTSIDE  
 security-level 0  
 ip address 10.10.10.1 255.255.255.0  
!  
interface GigabitEthernet1/3  
 nameif PRINTER  
 security-level 75  
 ip address 192.168.2.1 255.255.255.0  
!  
interface GigabitEthernet1/4  
 nameif DMZ  
 security-level 50  
 ip address 192.168.3.1 255.255.255.0  
!  
interface GigabitEthernet1/5  
 no nameif  
 no security-level  
 no ip address  
 shutdown  
!  
interface GigabitEthernet1/6  
 no nameif  
 no security-level  
 no ip address  
 shutdown  
!  
interface GigabitEthernet1/7  
 no nameif  
 no security-level  
 no ip address  
 shutdown  
!  
interface GigabitEthernet1/8  
 no nameif  
 no security-level  
 no ip address  
 shutdown  
!    
interface Management1/1  
 management-only  
 no nameif  
 no security-level  
 no ip address  
 shutdown  
!  
!  
!  
access-list HTTP_TO_DMZ extended permit tcp any host 192.168.3.2 eq www  
access-list HTTP_TO_DMZ extended permit icmp host 192.168.3.2 host 10.10.10.2  
access-list OUTSIDE extended permit tcp host 10.10.10.2 host 192.168.3.2 eq www  
access-list OUTSIDE extended permit icmp host 10.10.10.2 host 192.168.3.2  
access-list PRINTER extended deny ip any any  
!  
!  
access-group HTTP_TO_DMZ in interface DMZ  
access-group PRINTER in interface PRINTER  
access-group OUTSIDE in interface OUTSIDE  
!  
!  
class-map inspection_default  
 match default-inspection-traffic  
!  
policy-map type inspect dns preset_dns_map  
 parameters  
  message-length maximum 512  
policy-map global_policy  
 class inspection_default  
  inspect http   
  inspect icmp  
!  
service-policy global_policy global  
!  
telnet timeout 5  
ssh timeout 5  

</details>

### Доработка ДЗ  



<details>  
<summary>Корректировка ACL МСЭ</summary>  

!   
access-list OUTSIDE extended permit icmp 10.10.10.0 255.255.255.0 192.168.0.0 255.255.0.0  
access-list OUTSIDE extended permit tcp 10.10.10.0 255.255.255.0 192.168.3.0 255.255.255.0 eq www   
access-list PRINTER extended deny ip any any  
access-list HTTP_TO_DMZ extended permit icmp 192.168.3.0 255.255.255.0 10.10.10.0 255.255.255.0   
access-list INSIDE extended permit icmp 192.168.1.0 255.255.255.0 10.10.10.0 255.255.255.0  
access-list INSIDE extended permit icmp 192.168.1.0 255.255.255.0 192.168.2.0 255.255.255.0  
access-list INSIDE extended deny icmp 10.10.10.0 255.255.255.0 192.168.1.0 255.255.255.0
!  
!  
access-group PRINTER in interface PRINTER  
access-group OUTSIDE in interface OUTSIDE  
access-group HTTP_TO_DMZ in interface DMZ  
access-group INSIDE in interface INSIDE  
!  

</details>