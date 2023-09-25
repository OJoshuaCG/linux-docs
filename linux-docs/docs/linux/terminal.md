## [Kitty](https://sw.kovidgoyal.net/kitty/)

### Instalar

En arch linux, utilizamos pacman para instalar Kitty

```sh
sudo pacman -S kitty
```

### Configurar

El archivo de configuracion, lo podemos encontrar dentro de la carpeta `$HOME/.config/kitty/kitty.conf`, en caso de no existir, debemos crearlo

```sh
mkdir $HOME/.config/kitty
touch $HOME/.config/kitty/kitty.conf
```

!!! tip
    Puedes descargar el siguiente [enlace](https://github.com/OJoshuaCG/dotfiles/blob/main/config/kitty/kitty.conf) o sobreescribir tu archivo `kitty.conf`

    ```sh
    cp $HOME/.config/kitty/kitty.conf $HOME/.config/kitty/kitty.conf.backup
    wget -P $HOME/.config/kitty/kitty.conf https://raw.githubusercontent.com/OJoshuaCG/dotfiles/main/config/kitty/kitty.conf
    ```


### Tema

Para cambiar el tema, podemos descargar uno de los que se encuentra en el siguiente [repositorio](https://github.com/dexpota/kitty-themes) o buscar por nuestra cuenta un tema, simplemente debemos incluirlo en nuestro archivo de configuracion

```sh
nano $HOME/.config/kitty/kitty.conf

# ~/.config/kitty/kitty.conf
include $HOME/.config/kitty/<THEME_NAME>.conf
```


---
## [Alacritty](https://alacritty.org/)

### Instalar

Primeramente, instalaremos [`rustup`](https://rustup.rs/), el cual es un compilador para programas hechos en `Rust`

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

rustup override set stable
rustup update stable
```

Procedemos a instalar las dependencias y despues alacritty

```sh
pacman -S cmake freetype2 fontconfig pkg-config make libxcb libxkbcommon python
sudo pacman -S alacritty
```

### Configurar

El archivo de configuracion, lo encontramos en la carpeta `$HOME/.config/alacritty/alacritty.yml`, en caso de no existir podemos crearlo o copiar el archivo de referencia que nos brinda Alacritty a esa ubicacion

```sh
mkdir $HOME/.config/alacritty
touch $HOME/.config/alacritty/alacritty.yml

cp /usr/share/doc/alacritty/example/alacritty.yml $HOME/.config/alacritty/alacritty.yml
```

!!! tip
    Puedes descargar el siguiente [enlace](https://github.com/OJoshuaCG/dotfiles/blob/main/config/alacritty/alacritty.yml) o sobreescribir tu archivo `alacritty.yml`

    ```sh
    cp $HOME/.config/alacritty/alacritty.yml $HOME/.config/alacritty/alacritty.yml.backup
    wget -P $HOME/.config/alacritty/alacritty.yml https://raw.githubusercontent.com/OJoshuaCG/dotfiles/main/config/alacritty/alacritty.yml
    ```


### Temas

Para elegir un tema, debemos descargar un archivo del siguiene [repositorio](https://github.com/alacritty/alacritty-theme), lo colocaremos en la carpeta `$HOME/.config/alacritty/` para utilizarlo editaremos nuestro archivo de configuracion e importaremos el tema

```sh
nano $HOME/.config/alacritty/alacritty.yml

# ~/.config/alacritty/alacritty.yml
import:
    - $HOME/.config/alacritty/<THEME_NAME>.yml
```


<!-- ---
## Terminator

## Konsole

## xfce terminal

## gnome terminal -->

