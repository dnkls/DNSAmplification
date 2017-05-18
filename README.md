# DNSAmplification
Набор утилит для DNS Amplification stresstesting
## Системные требования
* Python 2.x.;
* Scapy;
* Linux;
* для утилиты dnsamplification.py - внешний IP адрес без фильтраци и NAT.
## Структура проекта

| Файл/директория | Описание |
| ---------------| -------- |
|dnsamplcheck.py | утилита правоерки DNS серверов на возможность DNS Amplification |
|dnsamplification.py | утилита для многопоточной отправки DNS запросов с возможностью спуфинга |
|dnsamplscan.py | утилита сканирования сети для поиска уязвимых DNS серверов |
|servers.txt | пример списка серверов и запросов |
| README.md | этот файл |
| LICENSE | лицензия |

## Начало работы
### dnsamplcheck.py
Параметры:
```
-input - входной файл со списком DNS серверов для проверки (требуется);  
-timeout - время ожидания ответа от DNS сервера (По умолчанию 2 сек.);  
-output - выходной файл со списком проверенных серверов (требуется).  
```
Пример:
```
python dnsamplcheck.py -input servers.txt -output good-servers.txt
```
### dnsamplification.py
Параметры:
```
-target - IP адрес тестируемого сервера (требуется);
-servers - файл со списком DNS серверов для усиления (требуется);
-timeout - время тестирования (в секундах) (По умолчанию: 10 сек.);
-threads - количество потоков для отправки DNS запросов (По умолчанию: 10).
```
Пример:
```
python dnsamplification.py -target 192.168.1.2 -servers servers.txt -timeout 100 -threads 20
```
### dnsamplscan.py
Параметры:
```
-ip - диапазон IP адресов для поиска DNS серверов;
-query - DNS запрос (По умолчанию: .);
-querytype - тип DNS запроса (A,MX,PTR и т.д.) (По умолчанию: A);
-timeout - время ожидания ответа от DNS сервера (По умолчанию: 10 сек.);
-aratio - требуемый коэффицент усиления (По умолчанию: 0);
-output - файл со списком найденных серверов.
```
Пример:
```
python dnsamplscan.py -192.168.0.0/24 -query . -querytype A -timeout 5 -aratio 10 -output servers.txt
```
### формат файла серверов
Список DNS серверов, передаваемый в файле имеет следующий формат:
```
<адрес сервера> <DNS запрос> <Тип DNS запроса> <коэффициент усиления>
```
Все параметры разделяются пробелами.  
Пример:
```
8.8.8.8 . A 2
```
## Что дальше

Посетите наш сайт, посвященный информационной безопасности.

Команда сайта BlackDiver.Net

[https://BlackDiver.Net](https://blackdiver.net)
