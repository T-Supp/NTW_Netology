## Домашнее задание к занятию "Методы логического объединения интерфейсов. Балансировка нагрузки, протоколы"  

---  

### Задание 1
Компания ОАО «XXX – век» планирует увеличить пропускную способность канала связи. К вам поступила заявка: настроить статическую агрегацию для сети.
Необходимо настроить и проверить доступность компьютеров, проверить настройки через пространство команд show.

![hbc](https://user-images.githubusercontent.com/73060384/150137949-45bfd56c-a35c-4042-9377-5764cb09594d.png)

Пришлите pkt с полученным проектом.  

### Ответ  

[.pkt файл](https://disk.yandex.ru/d/xqcnazGdlxyCPA) и скрин проверки  
![3.3-1](scr/3.3-1.png)  

---  

### Задание 2

Компания ОАО «XXX – век» после модернизации и расширения сети задумалась над резервированием существующего агрегированного канала.    
К вам поступила заявка: настроить динамическую агрегацию каналов для сети, так как есть риск разрыва соединения на основных интерфейсах.   


Необходимо: 
- настроить сетевое оборудование и проверить доступность компьютеров,
- проверить настройки через пространство команд show, 
- проверить работу после отключения основных интерфейсов.

<img width="600" alt="152157053-a276776b-efb9-41e6-9d32-7bbd326373df" src="https://user-images.githubusercontent.com/85602495/152174571-f344c6ec-ec34-4683-8f8b-51dbe57d6b45.png">

*Пришлите pkt с полученным проектом*  

### Ответ  

[.pkt файл](https://disk.yandex.ru/d/6cs3x0pBSWuAKA) и скрины проверки    
![1](scr/1.png)  
![2](scr/2.png)  

---  

### Задание 3

Компания ОАО «XXX – век» разместила в своей сети сетевые сервисы. Для увеличения полосы пропускания, повышения надежности и реализации высокой доступности серверов и расположенных на них сервисах Вам поставили задачу доработать топологию сети с учетом возможностей оборудования и настроить балансировку на основе ip адресов источника и получателя.
 
Необходимо: 
- настроить и проверить доступность компьютеров, 
- проверить настройки через пространство команд show.    

**Важно!** В эмуляторе Cisco Packet Tracer есть особенность: часть настроек сетевого оборудования в этой лабораторной работе не сохраняется, когда вы сохраняете ее в .pkt файл.  
**Решение**: На всех сетевых устройствах после окончания настройки нужно выполнить команду "write" или "copy running-config startap-config".
 

<img width="650" alt="image" src="https://user-images.githubusercontent.com/73060384/152157089-dc2af0c6-1968-4a18-abfe-647488afa52b.png">

*Пришлите pkt с полученным проектом*  

### Ответ  

[Ссылка на .pkt файл](https://disk.yandex.ru/d/GtgtASVakutqPA)  
![3.3-3](scr/3.3-3.png)
