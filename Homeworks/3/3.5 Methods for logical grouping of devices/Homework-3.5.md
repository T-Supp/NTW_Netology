## Домашнее задание к занятию "Методы логического объединения устройств"  

------

### Задание 1

Что такое технология MC-LAG в целом?  

### Ответ  

MC-LAG (Multi-Chassis Link Aggregation Group) – это технология агрегации нескольких линков Ethernet с резервированием коммутирующих устройств.  
Технология MC-LAG резервирует коммутаторы на аппаратном уровне и балансирует нагрузку между ними.  
А так же решает проблемы «единой точки отказа», «петель», неэффективного использования пропускной способности портов коммутаторов.  

------

### Задание 2

Какие есть различия между VSS и vPC?

### Ответ  

Технология VSS присуща коммутаторам серий Catalyst, vPC - коммутаторам Nexus, предназначенных для ЦОД.  
Основное отличие vPC от VSS состоит в том, что в vPC каждый коммутатор имеет независимый Control Plane и Management Plane, это дает гарантию того, что при отказе какого-либо компонента, сеть продолжит функционировать.  
В vPC синхронизация происходит через выделенный канал peer link, позволяя объединить два коммутатора, но при этом подключить еще "дочерние"(FEX).   
В VSS используется Port-Channel и позволяет объединить два коммутатора.    

------

### Задание 3

Какие преимущества дает технология StackWise?

### Ответ  

StackWise позволяет объединить до 9 коммутаторов, имея при этом один Control Plane.  
Так же позволяет экономить на uplink-портах и увеличить количество access-портов.  
Используя StackWise, можно подключать или отключать коммутаторы в «горячем» режиме, стек при этом продолжит функционировать. 
Повышенная отказоустойчивость стеков достигается не только технологиями горячей замены, но и избыточным электропитанием.  

------

### Задание 4

Если вам нужно построить распределенный Дата Центр, разнесенный по разным городам, какую технологию вы предпочтете: VSS или vPC?  
Обоснуйте свой ответ.

### Ответ  

vPC.  
По причине независимости Control\Data Plane, возможности расширения, а так же из-за расстояния, которое может быть между коммутаторами.  

------

### Вопрос 5

Вы хотите увеличить отказоустойчивость сетевой инфраструктуры в пределах одного Дата Центра, а именно зарезервировать коммутаторы уровня ядра.  
Какую технологию целесообразнее использовать StackWise или VSS/vPC?

### Ответ  

Если использовать коммутаторы Catalyst, то VSS. А если коммутаторы Nexus, тогда vPC.  
Предпочтительнее все-таки Nexus и vPC, ввиду бОльшей производительности, возможности расширения и отказоустойчивости.   
StackWise целесообразнее использовать на access уровне.  

------