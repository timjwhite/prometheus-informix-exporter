# Informix Exporter for Prometheus

Prometheus exporter for various Informix metrics, written in Go.

### Prerequisites 📋

Docker and docker-compose are required.

### Installation 🔧

The installation will be carried out using Docker and a series of configuration files.

In the `./exporter/sqlhosts` file, add the Informix instances that you want to monitor in the same way as you would in the Informix `sqlhosts` file.

**File:** `./export/sqlhosts`
```plaintext
#Server         Protocol         Host           Port

prueba        onsoctcp    192.168.1.50    1527
prueba2       onsoctcp    192.168.1.50    1530


```
In the ./exporter/odbc.ini file, configure the ODBC.


```
[ODBC]
UNICODE=UCS-2
[prueba]
Driver=/opt/IDS12/lib/cli/libifcli.so
Server=prueba
Database=sysmaster
TRANSLATIONDLL=/opt/IDS12/lib/esql/igo4a304.so
LogonID=informix
pwd=informix
[prueba2]
Driver=/opt/IDS12/lib/cli/libifcli.so
Server=prueba2
Database=sysmaster
TRANSLATIONDLL=/opt/IDS12/lib/esql/igo4a304.so
LogonID=informix
pwd=informix

```

The ./exporter/config.yaml file will be used by the exporter to read the configuration data.
Example:

```
---
servers:
- name: pruebaids
  informixserver: prueba
  user: informix
  password: informix
- name: pruebaids2
  informixserver: prueba2
  user: informix
  password: informix
custom: 
- query: select tabid from systables where tabid=99 
  response: tabid


```

The Prometheus configuration is located in ./prometheus.

You can change the port where you want the exporter to listen.

```
- job_name: 'informix'

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
    - targets: ['ids_exporter:8080']
      #  - job_name: 'node'

```



## System Startup ⚙️

```
docker-compose up -d

```



## Authors ✒️



* **Antonio Martinez Sanchez-Escalonilla ** - [anmartsan](https://github.com/anmartsan)
    www.scmsi.es



