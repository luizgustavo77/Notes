# GRAFANA

***Grafana install***  
[Youtube](https://www.youtube.com/watch?v=92g7b_KxEzk)

***Prometheus install***  
``` bash
sudo mkdir /home/monit
sudo cd /home/monit
sudo wget https://github.com/prometheus/prometheus/releases/download/v2.9.2/prometheus-2.9.2.linux-amd64.tar.gz
sudo tar -zxvf prometheus-2.9.2.linux-amd64.tar.gz
sudo mv prometheus-2.9.2.linux-amd64 prometheus
sudo rm -r prometheus-2.9.2.linux-amd64.tar.gz
sudo vim ~/.bashrc

#ADD COMAND
-------------------------------------------------------------------------
alias prometheus='/home/monit/prometheus/./prometheus --config.file=/home/monit/prometheus/prometheus.yml &'
-------------------------------------------------------------------------

source ~/.bashrc
```

***Node_export install***
``` bash
sudo cd /home/monit/
sudo wget https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz
sudo tar xvfz node_exporter-0.18.1.linux-amd64.tar.gz
sudo rm node_exporter-0.18.1.linux-amd64.tar.gz
sudo mv node_exporter-0.18.1.linux-amd64 node_exporter
sudo vim ~/.bashrc

#ADD COMAND
-------------------------------------------------------------------------
alias node_exporter='/home/monit/node_exporter/./node_exporter &'
-------------------------------------------------------------------------
source ~/.bashrc
vim /home/monit/prometheus/prometheus.yml

#ADD TO LISTEM
-------------------------------------------------------------------------
– targets:[‘localhost:9100’]
```


> Lembre-se de adicionar a porta 9100 no prometheus para expor os dados por ele   


***REDIS_EXPORT***
```
https://github.com/oliver006/redis_exporter
go get github.com/oliver006/redis_exporter
cd $GOPATH/src/github.com/oliver006/redis_exporter - aqui o caminho se instala como root fica /root/go/src/...
go build
./redis_exporte -redis.password	SENHA - para subir o redis_exporte com senha de Redis
/root/go/src/github.com/oliver006/redis_exporter/./redis_exporter -redis.password SENHA &
```
> Lembre-se de adicionar a porta 9121 no prometheus para expor os dados por ele

***Loki***
``` docker
version: "3"

services:
  loki:
    image: grafana/loki:latest
    ports:
      - "3100:3100"
    command: -config.file=/etc/loki/local-config.yaml

  promtail:
    image: grafana/promtail:latest
    volumes:
      - /var/log:/var/log
    command: -config.file=/etc/promtail/docker-config.yaml
```
> Lembre-se de adicionar a porta 3100 no prometheus para expor os dados por ele

***MySQL_Export***  
``` docker
docker run -d \
  -p 9104:9104 \
  -e DATA_SOURCE_NAME="exporter:SENHA" \
  prom/mysqld-exporter
```
``` bash
wget https://github.com/prometheus/mysqld_exporter/releases/download/0.7.1/mysqld_exporter-0.7.1.linux-amd64.tar.gz
tar xz < mysqld_exporter-0.7.1.linux-amd64.tar.gz  
```
- Criando user MySQL
``` sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'SENHA' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'localhost';
-- ALTER USER 'exporter'@'localhost' IDENTIFIED WITH mysql_native_password BY 'SENHA';
flush privileges;
```
vim .my.cnf  
``` css
[client]
user=USER
password=SENHA
```
- PROMETHEUS 
``` bash
- targets: ['localhost:9104']`  
./mysqld_exporter -config.my-cnf=".my.cnf"  
```

***BLACKBOX***
``` bash
cd /home/monit/
sudo curl -LO https://github.com/prometheus/blackbox_exporter/releases/download/v0.12.0/blackbox_exporter-0.12.0.linux-amd64.tar.gz
sha256sum blackbox_exporter-0.12.0.linux-amd64.tar.gz
sudo tar xvf blackbox_exporter-0.12.0.linux-amd64.tar.gz
sudo rm -r blackbox_exporter-0.12.0.linux-amd64.tar.gz
sudo mv blackbox_exporter-0.12.0.linux-amd64 blackbox_exporter
sudo vim blackbox_exporter/blackbox.yml

#ADD HTTP
-------------------------------------------------------------------------
modules:
  http_2xx:
    prober: http
    timeout: 5s
    http:      
      valid_status_codes: []
      method: GET
-------------------------------------------------------------------------
sudo vim ~/.bashrc

#ADD COMAND
-------------------------------------------------------------------------
alias blackbox_exporter='/home/monit/blackbox_exporter/./blackbox_exporter --config.file /home/monit/blackbox_exporter/blackbox.yml &'
-------------------------------------------------------------------------

source ~/.bashrc

#ADD TO LISTEM
-------------------------------------------------------------------------
- job_name: 'blackbox'
    metrics_path: /probe
    params:
      module: [http_2xx]
    static_configs:
      - targets:
        - http://localhost:8080
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: localhost:9115
```
---
---
***Dash metrica***  
```
Timeout - node_netstat_Tcp_CurrEstab
Swap - node_memory_SwapTotal_bytes 
SWAP USADO - node_memory_SwapCached_bytes
WEEK - node_time_seconds - node_boot_time_seconds
UPTIME - node_time_seconds - node_boot_time_seconds
CPU - (rate(node_cpu_seconds_total{mode!="idle"}[1m]))*100
DISK TOTAL - node_filesystem_size_bytes 
DISCK USADO - (node_filesystem_size_bytes- node_filesystem_avail_bytes)
RAM TOTAL - node_memory_MemTotal_bytes 
RAM USADO - node_memory_MemTotal_bytes - node_memory_MemFree_bytes - node_memory_Cached_bytes - node_memory_Buffers_bytes - node_memory_Slab_bytes
```

***Adiciona prometheus para inicar apos reboot***
``` shell
sudo crontab -e
@reboot prometheus
@reboot node_exporter

**Reload no prometheus
#!/bin/dash
 ps -e | grep -q "prometheus"
 if [ $? -eq 0 ] ;
 then
	 echo "prometheus ok"
 else
         prometheus
 fi

 ps -e | grep -q "node_exporter"
 if [ $? -eq 0 ] ;
 then
         echo "node_exporter ok"
 else
         node_exporter
 fi
 ```
***Adiciona no CRONTAB***  
``` bash
#write out current crontab
crontab -l > mycron
#echo new cron into cron file
*/1 * * * * ./inicia_prometheus.sh
#install new cron file
crontab mycron
rm mycron
``` 
***Email alert***  
```#################################### SMTP / Emailing ##########################
[smtp]
enabled = true
host = smtp.gmail.com:587
user = NOME@gmail.com
# If the password contains # or ; you have to wrap it with trippel quotes. Ex """#password;"""
password = """SENHA"""
;cert_file =
;key_file =
skip_verify = true
from_address = NOME@gmail.com
from_name = Grafana
# EHLO identity in SMTP dialog (defaults to instance_name)
;ehlo_identity = dashboard.example.com

[emails]
;welcome_email_on_sign_up = false
```
***Exemplo de mensagens***
```
Servidor DOWN [dd_eg_32_001 - ymi_database]
Uso de CPU acima de 95% [dd_eg_32_001 - ymi_database]
Servidor sem espaço de disco [dd_eg_32_001 - ymi_database]
Uso de memória RAM acima de 90% [dd_eg_32_001 - ymi_database]
Consumo de banda acima de 100mb [dd_eg_32_001 - ymi_database]
```
