## Ingresar

Para ingresar a un servidor vía `ssh` podemos ejecutar el siguiente comando

```sh
ssh user@host

# Example
ssh admin@192.168.122.122
```

Por defecto, se intentara ingresar a traves del puerto `22`, si se desea especificar otro, debe usarse el flag `-p`

```sh
ssh user@host -p 23
```

Si se tiene un archivo `.pem` se debera hacer uso del flag `-i`

```sh
ssh -i /path/pem_file user@host
```


---

## Clave publica

Dentro de nuestro equipo donde deseamos ingresar al servidor, vamos a crear una clave a traves del siguiente comando

```sh
ssh-keygen -t rsa
```

Esto nos generara una clave en `~/.ssh/` con el nombre `id_rsa.pub` el cual podremos copiar en nuestro servidor donde deseamos ingresar

```sh
ssh-copy-id user@host
```


---

## Ejecutar comandos

Podemos ejecutar comandos en un servidor vía ssh de manera sencilla.

```sh
ssh user@host "comando"

# Ejemplo
ssh user@host hostname
```

Tambien es posible ejecutar multiples comandos

```sh
ssh user@host comando1; comando2; comando3

# Ejemplo
ssh user@host hostname; date
```

Otro ejemplo para ingresar comandos es con ayuda del comando `EOF`

```sh
ssh user@host << EOF
comando1
comando2
EOF

# Ejemplo
ssh user@host << EOF
hostname
date
echo "Hola mundo!" > /tmp/archivo.txt
EOF
```


---

## Flags

`-1`, `-2`, especifica la version del protocolo ssh

```sh
ssh -1 user@host
ssh -2 user@host
```


`-4`, `-6`, conectarnos a un host por IPv4 o IPv6

```sh
ssh -4 user@host
ssh -6 user@host
```


`-C`, comprime toda la informacion obtenida de ssh, esto es funcional en conexiones lentas

```sh
ssh -C user@host
```


`-f`, ejecuta en segundo plano los comandos ingresados

```sh
ssh -f user@host hostname
```

`-F`, especificar un archivo de configuracion, por defecto se considera `~/ssh/config`

```sh
ssh -F /path/filename user@host
```


`-g`, permite al host remoto conectarse a puertos locales

```sh
ssh -g -L local_port:localhost:host_port user@host
```


`-J`, permite conectarnos a otro host remoto desde el host en que nos conectemos

```sh
ssh -J user@jump_host user@host_destination

ssh -J user@jump_host1,user@jump_host1:port user@host_destination
```


`-v`, muestra un debug de la conexion ssh

```sh
ssh -v user@host
```


`-E`, guarda el debug de la conexion ssh en un archivo especifico

```sh
ssh -v -E /path/filename user@host
```


---

## Fuentes

- [https://www.golinuxcloud.com/ssh-command-in-linux/](https://www.golinuxcloud.com/ssh-command-in-linux/)
- [https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples/](https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples)
- [https://linuxcommand.org/lc3_man_pages/ssh1.html](https://linuxcommand.org/lc3_man_pages/ssh1.html)