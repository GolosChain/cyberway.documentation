# 3 Создание контейнера
Процесс построения сервисов представляет собой построение томов `Docker volume`.  

**3.1 Создание тома Docker**  
Создать тома Docker для хранения базы данных состояния системы и данных цепочки, исполнив:
```
sudo docker volume create cyberway-mongodb-data
sudo docker volume create cyberway-nodeos-data
```
**3.2 Проверка создания томов**  
Для проверки создания томов необходимо исполнить:
```
docker volume ls
```
Создание томов считается успешным, если в выдаче команды содержится информация о созданных томах:
```
local cyberway-mongodb-data
local cyberway-nodeos-data
```
**3.3 Запуск сервисов**  
 Для запуска узла требуется запуск двух сервисов — `nodeosd` и `mongo`. Для упрощения процесса запуска используется утилита `docker-compose`.  
Войти в директорию `~/testnet` (в которой находится docker-compose.yml), и исполнить команду загрузки сервисов:
```
sudo docker-compose up -d
``` 
где:  
`-d` —  запускает контейнер в фоновом режиме.  

**3.4 Проверка запуска контейнеров**  
Для проверки успешного запуска контейнеров необходимо исполнить следующую команду:
```
sudo docker ps
```
Создание контейнеров считается успешным, если в тексте лог-файлов будут отсутствовать сообщения об ошибках и появятся сообщения о создании контейнеров с именами `nodeosd` и `mongo`. Для анализа текста лог-файлов можно использовать команды вида:
```
sudo docker logs --tail 100 -f nodeosd
sudo docker logs --tail 100 -f mongo
```
где:  
`--tail`  —  задает количество последних строк текста;  
`-f`  —  указывает, что необходимо следить за обновлением лог-файла.  

Текст лог-файла `nodeosd` должен также содержать информацию о сгенерированных блоках, а также о блоках, принимаемых из Testnet. Информация в лог-файле о сгенерированном блоке должна иметь следующий вид:
```
info  2019-03-07T06:57:09.024 thread-0  producer_plugin.cpp:1491      produce_block        ] Produced block 00000c992d36ab56... #3225 @ 2019-03-07T06:57:09.000 signed by producera [trxs: 0, lib: 2564, confirmed: 0]
```
Информация в лог-файле о получаемых по сети блоках должна иметь следующий вид:
```
info  2019-03-07T06:57:00.096 thread-0  producer_plugin.cpp:344       on_incoming_block    ] Received block 6d6ac52bfe754174... #3222 @ 2019-03-07T06:57:00.000 signed by cyber [trxs: 0, lib: 2562, conf: 0, latency: 96 ms]
```
При успешном старте тестнета в лог-файл периодически сохраняется информация о полученных по сети блоках.  

**3.5 Рекомендация**  
> В случае появления ошибок во время запуска контейнера рекомендуется остановить функционирование сервисов, удалить `Docker volume` и создать его заново.  

Для останова функционирования сервисов исполнить:
```
sudo docker-compose down
```
Для удаления `Docker volume` необходимо испольнить следующую команду:
```
sudo docker volume rm cyberway-mongodb-data cyberway-nodeos-data
```
Для повторного создания `Docker volume` необходимо заново выполнить указания, начиная с п. 3.1. В случае наличия ошибок при повторном создании `Docker volume` следует сообщить об этом команде разработчиков CyberWay. 