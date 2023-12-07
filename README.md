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

Чуть помучился с Logstash


![image](https://github.com/Byzgaev-I/ELK/blob/main/NGINX-3.png)

Прописал конфиг.  
Настройки для логстэша хранятся в каталоге /etc/logstash/conf.d в файлах формата JSON. Для конфигурации используются следующие секции:   
1) input (входные данные).   
2) filter (фильтры).   
3) output (выходные данные).
   
*input.conf* с содержимым

``` bash
input {
  file {
    path => "/var/log/nginx/access.log"
    start_position => "beginning"
  }
}
```


*filter.conf*

``` bash
filter {
    grok {
      match => { "message" => "%{IPORHOST:remote_ip} - %{DATA:user_name}
      \[%{HTTPDATE:access_time}\] \"%{WORD:http_method} %{DATA:url}
      HTTP/%{NUMBER:http_version}\" %{NUMBER:response_code} %{NUMBER:body_sent_bytes}
      \"%{DATA:referrer}\" \"%{DATA:agent}\"" }
    }
    mutate {
        remove_field => [ "host" ]
    }
}
```

*output.conf*

``` bash
output {
    elasticsearch {
      hosts => "http://localhost:9200"
      data_stream => "true"
    }
}

```
смотрим логи

![image](https://github.com/Byzgaev-I/ELK/blob/main/NGINX-5.png)

---

### Задание 4. Filebeat. 

Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.*

### Решение

cоздал дашборды 
**filebeat setup --dashboards** 

![image](https://github.com/Byzgaev-I/ELK/blob/main/filebeat-1.png)

включил нужные модули
**filebeat modules enable system nginx**

![image](https://github.com/Byzgaev-I/ELK/blob/main/filebeat-2.png)

поменял конфиг Logstash "input"
**nano /etc/logstash/conf.d/input.conf**

![image](https://github.com/Byzgaev-I/ELK/blob/main/filebeat-3.png)

также поменял конфигурацию в /etc/filebeat/filebeat.yml
Скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.

![image](https://github.com/Byzgaev-I/ELK/blob/main/filebeat-4.png)




