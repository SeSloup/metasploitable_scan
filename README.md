# Домашнее задание к занятию «Уязвимости и атаки на информационные системы»


------

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

[настройка](https://github.com/SeSloup/metasploitable_scan/blob/main/safety_inf.txt)
![настройка](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/test_ping.png)

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?

![nmap -sV](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/nmap_scan.png)

- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

FTPD, Mysql 5.0.5*, smtp, apache
[vsftpd 2.3.4](https://www.exploit-db.com/exploits/49757)
[MySQL 5.0.x](https://www.exploit-db.com/exploits/29724)
[MySQL 5.0.x - IF Query](https://www.exploit-db.com/exploits/30020)
[apache](Apache 1.3)

![auxilairy scan](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/01.png)
![auxilairy scan](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/02_mysql_smtp.png)

 

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
лучше всего различия описываются в документации [nmap](https://nmap.org/man/ru/man-port-scanning-techniques.html)


```
-sS : Он работает с любым TCP стеком, не завися от каки-либо особенностей специфичной платформы, как это происходит при сканированиях типа FIN/NULL/Xmas, Maimon и idle сканировании. 
```

```
-sU : UDP сканирование работает путем посылки пустого (без данных) UDP заголовка на каждый целевой порт. Если в ответ приходит ICMP ошибка о недостижимости порта (тип 3, код 3), значит порт закрыт. (остальные - фильтруется)
```

```
-sX, -sF : Эти типы сканирования используют (другие типы сканирования доступны с использованием опции --scanflags описанной в другой секции) незаметную лазейку в TCP RFC, чтобы разделять порты на открытые и закрытые.
Когда сканируется система отвечающая требованиям RFC, любой пакет, не содержащий установленного бита SYN, RST или ACK, повлечет за собой отправку RST в ответ в случае, если порт закрыт, или не повлечет никакого ответа, если порт открыт. 
```

- Как отвечает сервер?
WIRESHARK scan

![sS](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/syn.png)
![sF](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/fin.png)
![sX](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/xmas.png)
![sU](https://github.com/SeSloup/metasploitable_scan/blob/main/screens/udp.png)

