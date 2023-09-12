## [Kitty](https://sw.kovidgoyal.net/kitty/)

Descargar un tema de [Kitty themes en Github](https://github.com/dexpota/kitty-themes)
```bash
THEME=https://raw.githubusercontent.com/dexpota/kitty-themes/master/themes/3024_Day.conf
# or
THEME=https://raw.githubusercontent.com/rxyhn/bspdots/main/config/kitty/color.ini
# or
THEME=https://raw.githubusercontent.com/catppuccin/kitty/main/themes/mocha.conf
wget "$THEME" -P ~/.config/kitty/kitty-themes/themes
```

Crear un enlace simbolico de `theme.conf` al tema descargado:

_**No olvides cambiar en el segundo comando el nombre del archivo por el que descargaste**_

```bash
cd ~/.config/kitty
ln -s ./kitty-themes/themes/3024_Day.conf ~/.config/kitty/theme.conf
```

Por ultimo abriremos el archivo `kitty.conf` para agregar la siguiente linea:
```bash
nano ~/.config/kitty/kitty.conf

# ~/.config/kitty/kitty.conf
include ./theme.conf
```

Tambien es posible configurar algunos comandos, puedes descargar el siguiente [archivo](https://gist.github.com/OJoshuaCG/72a7aa6d0caca80e802cf751446fa8b3), el cual debera ir en la siguiente direccion `~/.config/kitty/kitty.conf`.

---
## [Alacritty](https://alacritty.org/)

Descargar un tema

---
## Terminator


---
## Konsole

