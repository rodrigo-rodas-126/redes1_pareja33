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
    enable
    configure terminal

    hostname Central

    !Configuracion interfaz serial
    interface s1/0
    ip address 10.0.0.1 255.255.255.252
    no shutdown

    !Configuracion primera interfaz
    interface e0/0
    ip address 133.168.1.2 255.255.255.248
    no shutdown

    !Configuracion segunda interfaz
    interface e0/1
    ip address 133.168.2.2 255.255.255.248
    no shutdown

    exit

    !Configuracion rutas estáticas

    ! Hacia 133.168.0.0
    ip route 133.168.0.0 255.255.255.0 133.168.1.1

    ! Hacia 133.178.1.0
    ip route 133.178.1.0 255.255.255.248 10.0.0.2

    ! Hacia 133.178.2.0
    ip route 133.178.2.0 255.255.255.248 10.0.0.2

    ! Hacia 133.178.0.0
    ip route 133.178.0.0 255.255.255.248 10.0.0.2

    do write

#

##### - R2

    ! Modo Configuracion
    enable
    configure terminal

    hostname R2

    !Configuracion interfaz enlace
    interface e0/0
    ip address 133.168.1.1 255.255.255.248
    no shutdown

    !Configuracion primera interfaz
    interface e0/1
    ip address 133.168.0.2 255.255.255.0
    no shutdown

    !Configuracion GLBP
    glbp 7 ip 133.168.0.1
    glbp 7 preempt
    glbp 7 priority 150
    glbp 7 load-balancing round-robin

    exit

    !Configuracion rutas estáticas

    ! Hacia 10.0.0.0
    ip route 10.0.0.0 255.255.255.252 133.168.1.2

    ! Hacia 133.168.2.0
    ip route 133.168.2.0 255.255.255.248 133.168.1.2

    ! Hacia 133.178.1.0
    ip route 133.178.1.0 255.255.255.248 133.168.1.2

    ! Hacia 133.178.2.0
    ip route 133.178.2.0 255.255.255.248 133.168.1.2

    ! Hacia 133.178.0.0
    ip route 133.178.0.0 255.255.255.0 133.168.1.2

    do write

#

##### - R5

    ! Modo Configuracion
    enable
    configure terminal

    hostname R5

    !Configuracion interfaz enlace
    interface e0/0
    ip address 133.178.1.1 255.255.255.248
    no shutdown

    !Configuracion primera interfaz
    interface e0/1
    ip address 133.178.0.2 255.255.255.0
    no shutdown

    !Configuracion HSRP
    standby version 2
    standby 21 ip 133.178.0.1
    standby 21 priority 109
    standby 21 preempt

    exit

    !Configuracion rutas estáticas

    ! Hacia 133.178.2.0
    ip route 133.178.2.0 255.255.255.248 133.178.1.2

    ! Hacia 10.0.0.0
    ip route 10.0.0.0 255.255.255.252 133.178.1.2

    ! Hacia 133.168.1.0
    ip route 133.168.1.0 255.255.255.248 133.178.1.2

    ! Hacia 133.168.2.0
    ip route 133.168.2.0 255.255.255.248 133.178.1.2

    ! Hacia 133.168.0.0
    ip route 133.168.0.0 255.255.255.0 133.178.1.2

    do write

#

##### - SW7

    ! Modo Configuracion
    enable
    configure terminal

    hostname SW7

    ! Creacion Etherchanel
    interface Port-channel 1

    ! Configuracion Interfaces
    interface range e0/0-1

    ! Configuracion Etherchanel LACP
    channel-group 1 mode active

    exit

    do write

#

##### - VPC11

    ip 133.168.0.4 255.255.255.0 133.168.0.1

#

#### 4 - Resumen de comandos usados
#

##### - Rutas Estaticas
Para la creacion de las rutas estaticas en cada router se utilizo el comando ip route con la diferentes redes de la topologia y los puetos de los routers para saltar entre redes.

    ip route <ID Red Destino> <Mascara de la Red Destino> <IP del primer salto>
#
##### - PortChannel con PAGP y LACP
Para la configuracion de portchannel se utilizaron los siguientes comandos con parametros diferentes, en las interfaces de los diferentes Switches.

    LACP
    channel-group <ID Grupo> mode <active|passive>

    PAGP
    channel-group <ID Grupo> mode <desirable|auto>
#
##### - IP virtual con HSRP y GLBP
Para la definicion de la IP Virtual entre Router se utilizo la primera direccion IP Disponible en las redes correspondientes, y se definieron Router Principales y de Respaldo con los comandos de cada uno de los protocolos.

    HSRP
    ! Router Principal
    standby version 2
    standby 21 ip <IP Virtual>
    standby 21 priority 109
    standby 21 preempt

    ! Router Respaldo
    standby version 2
    standby 21 ip <IP Virtual>

    GLBP
    ! Router Principal
    glbp 7 ip <IP Virtual>
    glbp 7 preempt
    glbp 7 priority 150
    glbp 7 load-balancing round-robin

    ! Router Respaldo
    glbp 7 ip <IP Virtual>
    glbp 7 load-balancing round-robin
#
##### - Configuración de VPC
###### Para la configuracion de las VPC's unicamente se utilizo el comando IP con su mascara y su gateway que es la IP virtual definidas en los routers correspondientes.
    
    ip <Direccion IP> <Mascara de Subred> <Gateway>


#
#### 5 - Comandos empleados para la verificación del correcto funcionamiento

Comando ping para la validacion de comunicacion entre redes y routers.

    ping <Direccion IP>

Comandos para la verificacion de la configuracion de los protocolos en los routers.

    show standby
    show standby brief

    show glbp
    show glbp brief

Comandos para la verificacion de la configuracion de portchannel en los switches.

    show etherchannel summary

    show lacp neighbor

    show pagp neighbor

Comando para la verificacion de direcciones estaticas.

    show ip route
    show running-config | section ip route

Comando para la consulta de la configuracion actual.

    show running-config