# Домашнее задание к занятию «ELK» - `Бызгаев Александр`

### Задание 1. Elasticsearch 

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.

---

### Решение

![image](https://github.com/Byzgaev-I/ELK/blob/main/Elastic%20-1.png)

Скриншот с командой: 'curl -X GET 'localhost:9200/_cluster/health?pretty'

![image](https://github.com/Byzgaev-I/ELK/blob/main/Elastic-2.png)

![image](https://github.com/Byzgaev-I/ELK/blob/main/Elastic-3.png)

---

### Задание 2. Kibana

Установите и запустите Kibana.
*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.

---

### Решение

![image](https://github.com/Byzgaev-I/ELK/blob/main/Kibana-1.png)

**скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console**

![image](https://github.com/Byzgaev-I/ELK/blob/main/Kibana-2.png)

---  

### Задание 3. Logstash

Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.*

### Решение

Установил Nginx

![image](https://github.com/Byzgaev-I/ELK/blob/main/NGINX.png)

![image](https://github.com/Byzgaev-I/ELK/blob/main/NGINX-2.png)




