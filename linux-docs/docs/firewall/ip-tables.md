IP tables nos permite configurar las tablas proporcionadas por el cortafuegos de Linux y las cadenas y reglas que almacena.

## Accion

| Accion (target) | Descripcion                                                                                                                            |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `ACCEPT`        | Aceptar el paquete                                                                                                                     |
| `DROP`          | Rechazar el paquete                                                                                                                    |
| `QUEUE`         | Mueve el paquete a los procesos de usuario y requiere un intermediario (queue handler) que reenvie todos los paquetes a una aplicacion |
| `RETURN`        | El paquete se reenvia de nuevo a la cadena anterior en caso de que haya sido definida por el usuario                                   |


---

## Tablas

Existen cuatro tablas principales, cada una con sus cadenas (chains) y proposito especifico.

### filter

Permite filtrar el trafico de paquetes basandose en reglas definidas

| Cadena     | Descripcion                                                |
| ---------- | ---------------------------------------------------------- |
| `INPUT`    | Paquetes de entrada                                        |
| `OUTPUT`   | Paquetes de salida, antes que salgan del sistema           |
| `FORDWARD` | Paquetes que pasan por el sistema, actuando como un router |


### nat

Se consulta cuando un paquete crea una nueva conexion, realiza la traduccion de direcciones de red, generalmente para el redireccionamiento de puertos (port fordwarding) o enmascaramientos de direcciones IP (SNAT - Source Network Address Translation).

| Cadena        | Descripcion                                                                                  |
| ------------- | -------------------------------------------------------------------------------------------- |
| `PREROUTING`  | Paquetes antes de ser enrutados, permitiendo el redireccionamiento de puertos                |
| `OUTPUT`      | Paquetes de salida, antes que salgan del sistema                                             |
| `POSTROUTING` | Paquetes despues del enrutamiento, comunmente utilizado para el enmascaramiento de IP (SNAT) |


### mangle

Modifica las cabeceras de los paquetes. Utilizado para marcar paquetes para su posterior manipulacion por otras reglas o herramientas.

| Cadena        | Descripcion                                            |
| ------------- | ------------------------------------------------------ |
| `PREROUTING`  | Paquetes antes de ser enrutados                        |
| `INPUT`       | Paquetes de entrada antes de ser entregados localmente |
| `FORDWARD`    | Paquetes que solo pasan por el sistema                 |
| `OUTPUT`      | Paquetes de salida, antes que salgan del sistema       |
| `POSTROUTING` | Paquetes despues del enrutamiento                      |


### raw

Configura exenciones del seguimiento de conexiones.

| Cadena       | Descripcion                                      |
| ------------ | ------------------------------------------------ |
| `PREROUTING` | Paqutes antes de ser enrutados                   |
| `OUTPUT`     | Paquetes de salida, antes que salgan del sistema |


### security

Esta tabla es usada para las reglas de red por MAC.

| Cadena    | Descripcion                                      |
| --------- | ------------------------------------------------ |
| `INPUT`   | Paquetes de entrada                              |
| `OUTPUT`  | Paquetes de salida, antes que salgan del sistema |
| `FORWARD` | Paquetes que solo pasan por el sistema           |


## Opciones

Opciones que son reconocidas por iptables y pueden ser divididas en distintos grupos

### Comandos

Estas opciones especifican la acción deseada a realizar.

| Comando                | Accion                                                                             |
| ---------------------- | ---------------------------------------------------------------------------------- |
| `-A`, `--append`       | Agrega regla(s) al final de la cadena seleecionada                                 |
| `-C`, `--check`        | Verifica si una regla existe en la cadena                                          |
| `-D`, `--delete`       | Elimina regla(s) en la cadena, coincidiendo con el numero o la regla               |
| `-I`, `--insert`       | Inserta regla(s) en la cadena ingresando un numero de regla                        |
| `-R`, `--replace`      | Reemplaza una regla de la cadena seleccionada                                      |
| `-L`, `--list`         | Lista todas las reglas de la cadena seleccionada                                   |
| `-S`, `--list-rules`   | Imprime odas las reglas de la cadena seleccionada                                  |
| `-F`, `--flush`        | Elimina la cadena seleccionada (todas las cadenas de la tabla si no se especifica) |
| `-Z`, `--zero`         | Establece en 0 los contadores de paquetes y bytes en todas o una cadena            |
| `-N`, `--new-chain`    | Crea una nueva cadena de acuerdo al nombre dado                                    |
| `-X`, `--delete-chain` | Elimina una cadena especifica, no debe tener referencias                           |


### Parametros

| Parametro               | Accion                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `-p`, `--protocol`      | Protocolo del paquete, **tcp**, **udp**, **udplite**, **icmp**, **icmpv6**, **esp**, **ah**, **sctp**, **mh**, **all**                     |
| `-s`, `--source`        | Fuente del paquete, colocando la IP, nombre de red o hostname                                                                              |
| `-d`, `--destination`   | Destino del paquete, colocando la IP, nombre de red o hostname                                                                             |
| `-m`, `--match`         | Indica la coincidencia a utilizar.                                                                                                         |
| `-j`, `--jump`          | Indica el objetivo de la regla en caso de coincidir, el objetivo puede ser una cadena, otro objetivo o una extension                       |
| `-g`, `--goto`          | Indica que el procesamiento debe continuar en una cadena especifica                                                                        |
| `-i`, `--in-interface`  | Nombre de la interfaz donde se recibe el paquete (solo cadenas **INPUT**, **FORWARD** y **PREROUTING**)                                    |
| `-o`, `--out-interface` | Nombre de la interfaz a donde se dirigira el paquete (solo cadenas **FORWARD**, **OUTPUT**, **POSTROUTING**)                               |
| `-c`, ``--set-counters` | Permite al administrador inicializar los contadores de paquetes y bytes de una regla (en operaciones **INSERT**, **APPEND**, **REPLACE**). |


## Fuentes

- [Hostgator - iptables](https://www.hostgator.mx/blog/guia-iptables/)
- [IONOS - iptables](https://www.ionos.mx/digitalguide/servidores/herramientas/iptables-conoce-las-reglas-para-crear-paquetes-de-datos/)