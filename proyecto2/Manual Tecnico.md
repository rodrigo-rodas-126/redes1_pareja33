#### MANUAL TECNICO - PROYECTO 2

#### 1 - Tabla Direcciones IP

| Dispositivo | Interfaz | IP | Mascara SubRed (CIDR) | Gateway |
|---|---|---|---|---|
|Academico|eth0|172.133.2.2|/27|
|Investigacion|eth0|172.133.2.33|/28|
|Administracion|eth0|172.133.2.49|/28|
|Seguridad|eth0|172.133.2.65|/29|
|R|e0/0.13|172.133.2.3|/27|
|R|e0/0.23|172.133.2.34|/28|
|R|e0/0.33|172.133.2.50|/28|
|R|e0/0.43|172.133.2.66|/29|

#

#### 2 - Tabla de Redes

| ID de Red | Direcciones IP Disponibles | Mascara de SubRed | Primera IP Disponible | Ultima IP Disponible | Direccion de Broadcast |
|---|---|---|---|---|---|
|Red Base|---|---|---|---|---|
|172.133.2.0|254|255.255.255.0|172.133.2.1|172.133.2.254|172.133.2.255|
|SubRedes|---|---|---|---|---|
|172.133.2.0|30|255.255.255.224|172.133.2.1|172.133.2.30|172.133.2.31
|172.133.2.32|14|255.255.255.240|172.133.2.33|172.133.2.46|172.133.2.47
|172.133.2.48|14|255.255.255.240|172.133.2.49|172.133.2.62|172.133.2.63
|172.133.2.64|6|255.255.255.248|172.133.2.65|172.133.2.70|172.133.2.71

#

#### 3 - 

#

#### 4 - Capturas Topologia