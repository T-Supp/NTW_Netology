## Домашнее задание к занятию "Методы контроля и управления доступом к сети"

---

### Задание 1. 

На картинке изображена схема подключения хаба к свитчу. К хабу одновременно может подключаться не более 3 трех устройств. Если будет обнаружено, что подключено более 3 устройств, то необходимо запретить трафик с дополнительных устройств и отправить уведомление о нарушении. 


![image](https://user-images.githubusercontent.com/51816695/155541965-c60aa0fe-ebdb-465f-adcd-9d6bcecd759c.png)

Как необходимо настроить порт Fa0/5 на свитче?

*Отправьте список команд.*

### Ответ.  

Команды на порт f0/5:  
````
Switch(config)#interface fa0/5
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security maximum 3
Switch(config-if)#switchport port-security mac-address sticky
Switch(config-if)#switchport port-security violation restrict
````

### Задание 2. 

Для отдела мониторинга необходимо настроить view monitoring, в котором можно будет делать следующие операции:
- Смотреть логи устройства
- Смотреть таблицу MAC адресов
- Смотреть таблицу arp
- Смотреть полную конфигурацию свитча

*Отправьте конфигурацию parser view monitoring.*

### Ответ.  

Настройки следующие:  
```
Switch(config)#aaa new-model
Switch(config)#parser view monitoring
Switch(config-view)#secret password123
Switch(config-view)#commands exec include show logging
Switch(config-view)#commands exec include show mac address-table
Switch(config-view)#commands exec include show arp
Switch(config-view)#commands exec include show running-config
```
