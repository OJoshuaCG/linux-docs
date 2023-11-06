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
| `OUTPUT`   | Paquetes de salida antes que salgan del sistema            |
| `FORDWARD` | Paquetes que pasan por el sistema, actuando como un router |


### nat

Se consulta cuando un paquete crea una nueva conexion, realiza la traduccion de direcciones de red, generalmente para el redireccionamiento de puertos (port fordwarding) o enmascaramientos de direcciones IP (SNAT - Source Network Address Translation).

| Cadena        | Descripcion                                                                                  |
| ------------- | -------------------------------------------------------------------------------------------- |
| `PREROUTING`  | Paquetes antes de ser enrutados, permitiendo el redireccionamiento de puertos                |
| `OUTPUT`      | Paquetes de salida antes que salgan del sistema                                              |
| `POSTROUTING` | Paquetes despues del enrutamiento, comunmente utilizado para el enmascaramiento de IP (SNAT) |


### mangle

Modifica las cabeceras de los paquetes. Utilizado para marcar paquetes para su posterior manipulacion por otras reglas o herramientas.

| Cadena        | Descripcion                                            |
| ------------- | ------------------------------------------------------ |
| `PREROUTING`  | Paquetes antes de ser enrutados                        |
| `INPUT`       | Paquetes de entrada antes de ser entregados localmente |
| `FORDWARD`    | Paquetes que solo pasan por el sistema                 |
| `OUTPUT`      | Paquetes de salida antes que salgan del sistema        |
| `POSTROUTING` | Paquetes despues del enrutamiento                      |


### raw

Configura exenciones del seguimiento de conexiones.

| Cadena       | Descripcion                                 |
| ------------ | ------------------------------------------- |
| `PREROUTING` | Modifica los paqutes antes de ser enrutados |
| `OUTPUT`     | Modifica los paquetes de salida             |


### security





## Fuentes

- [Hostgator - iptables](https://www.hostgator.mx/blog/guia-iptables/)
- [IONOS - iptables](https://www.ionos.mx/digitalguide/servidores/herramientas/iptables-conoce-las-reglas-para-crear-paquetes-de-datos/)