#### MANUAL TECNICO - PROYECTO1 1

#### 1 - Tabla Direcciones IP

| Dispositivo | Interfaz | IP | Mascara SubRed (CIDR) |
|---|---|---|---|
|Central|S1/0|10.0.0.1|/30|
|--|e0/0|133.168.1.2|/29|
|--|e0/1|133.168.2.2|/29|
|R2|e0/0|133.168.1.1|/29|
|--|e0/1|133.168.0.2|/24|
|R3|e0/0|133.168.2.1|/29|
|--|e0/1|133.168.0.3|/24|
|R2-R3|Virtual|133.168.0.1|/24|
|VPC11|eth0|133.168.0.4|/24|
|Villa_Nueva|S1/0|10.0.0.2|/30|
|--|e0/0|133.178.1.2|/29|
|--|e0/1|133.178.2.2|/29|
|R5|e0/0|133.178.1.1|/29|
|--|e0/1|133.178.0.2|/24|
|R6|e0/0|133.178.2.1|/29|
|--|e0/1|133.178.0.3|/24|
|R5-R6|Virtual|133.178.0.1|/24|
|VPC12|eth0|133.178.0.4|/24|

#

#### 2 - Tabla de Rangos IP's

| ID de Red | Direcciones IP Disponibles | Mascara de SubRed | Primera IP Disponible | Ultima IP Disponible | Direccion de Broadcast |
|---|---|---|---|---|---|
|10.0.0.0|2|255.255.255.252|10.0.0.1|10.0.0.2|10.0.0.3|
|133.168.0.0|254|255.255.255.0|133.168.0.1|133.168.0.254|133.168.0.255|
|133.168.1.0|6|255.255.255.248|133.168.1.1|133.168.1.6|133.168.1.7|
|133.168.2.0|6|255.255.255.248|133.168.2.1|133.168.2.6|133.168.2.7|
|133.178.0.0|254|255.255.255.0|133.178.0.1|133.178.0.254|133.178.0.255|
|133.178.1.0|6|255.255.255.248|133.178.1.1|133.178.1.6|133.178.1.7|
|133.178.2.0|6|255.255.255.248|133.178.2.1|133.178.2.6|133.178.2.7|


#

#### 3 - Detalle Comandos Utilizados
#

##### - Central

    ! Modo Configuracion
    configure terminal

    !Configuracion interfaz serial
    interface s1/0
    ip address 10.0.0.1 255.255.255.252
    no shutdown

    !Configuracion primera interfaz
    interface e0/0
    ip address 133.168.1.2 255.255.255.248
    no shutdown

    !Configuracion segunda interfaz
    interface e0/0
    ip address 133.168.2.2 255.255.255.248
    no shutdown

#

##### - R2

    ! Modo Configuracion

#

##### - R5

    ! Modo Configuracion

#

##### - SW7

    ! Modo Configuracion

#

##### - VPC11

    ip 133.168.0.4 255.255.255.0 133.168.0.1

#