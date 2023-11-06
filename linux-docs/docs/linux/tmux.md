`tmux` es un multiplexor de terminal, en español, nos permite ejecutar aplicaciones/comandos/scripts sobre sesiones de terminales, siendo en forma de paneles o ventanas.

## Sesiones (sessions)

Crear sesiones

```sh
tmux
tmux new
tmux new -s <NAME>
```

Ingresar a una sesion

```sh
# Ingresar al a ultima sesion creada
tmux a
tmux att

tmux a -t <NAME>
```

Eliminar una sesion

```sh
# Elimina la ultima sesion creada
tmux kill-ses

tmux kill-session -t <NAME>
```

Ver sesiones activas

```sh
tmux ls
```


| Atajo                | Accion                        |
| -------------------- | ----------------------------- |
| ++ctrl+b++   ++"$"++ | Renombrar sesion              |
| ++ctrl+b++   ++d++   | Salir de una sesion (dettach) |
| ++ctrl+b++   ++")"++ | Ir a la siguiente sesion      |
| ++ctrl+b++   ++"("++ | Ir a la sesion anterior       |
| ++ctrl+b++   ++s++   | Listar sesiones activas       |


---
## Ventanas (windows)

Las ventanas son como pestañas en un navegador, ocupan el espacio de la pantalla.

| Atajo                         | Accion                               |
| ----------------------------- | ------------------------------------ |
| ++ctrl+b++   ++c++            | Crear una nueva ventana              |
| ++ctrl+b++   ++n++            | Ir a la siguiente ventana            |
| ++ctrl+b++   ++p++            | Ir a la ventana anterior             |
| ++ctrl+b++   ++l++            | Ir a la ventana reciente             |
| ++ctrl+b++   ++0++ ... ++9++  | Seleccionar un numero de ventana     |
| ++ctrl+b++   ++single-quote++ | Seleccionar la ventana por su nombre |
| ++ctrl+b++   ++period++       | Cambiar el numero de la ventana      |
| ++ctrl+b++   ++comma++        | Renombrar la ventana                 |
| ++ctrl+b++   ++w++            | Listar ventanas                      |
| ++ctrl+b++   ++f++            | Buscar una ventana                   |
| ++ctrl+b++   ++"&"++          | Cerrar/eliminar ventana              |


---
## Paneles (panes)

Los paneles son secciones de las ventanas que dividen la pantalla.

| Atajo                              | Accion                                    |
| ---------------------------------- | ----------------------------------------- |
| ++ctrl+b++   ++"%"++               | Dividir en vertical                       |
| ++ctrl+b++   ++double-quote++      | Dividir en horizontal                     |
| ++ctrl+b++   ++o++                 | Ir al siguiente panel                     |
| ++ctrl+b++   ++semicolon++         | Ir al ultimo panel activo                 |
| ++ctrl+b++   ++close-brace++       | Ir al panel de la derecha                 |
| ++ctrl+b++   ++open-brace++        | Ir al panel de la izquierda               |
| ++ctrl+b++   ++q++                 | Mostrar numero del panel                  |
| ++ctrl+b++   ++q++ ++0++ ... ++9++ | Mostrar numero del panel y seleccionarlo  |
| ++ctrl+b++   ++z++                 | Panel en pantalla completa de la terminal |
| ++ctrl+b++   ++exclam++            | Convertir panel en ventana                |
| ++ctrl+b++   ++'<ARROW>'++         | Mover panel hacia un lado                 |
| ++ctrl+b++   ++space++             | Cambiar vista de los paneles              |
| ++ctrl+b+'<ARROW>'++               | Cambiar tamaño del panel                  |
| ++ctrl+b++   ++x++                 | Cerrar/eliminar panel                     |


++ctrl+b++ ++question++ para ver la lista de comandos.

<!--
https://facelessuser.github.io/pymdown-extensions/extensions/keys/
-->

## Fuentes

- https://tmuxcheatsheet.com/
- https://www.pluralsight.com/resources/blog/cloud/tmux-cheat-sheet