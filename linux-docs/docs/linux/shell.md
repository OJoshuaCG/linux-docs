## Cambiar entre terminales

```sh
# Visualizar terminales instaladas
cat /etc/shells
# or
chsh -l

chsh -s $(which zsh)        # Cambiar a zsh
chsh -s $(which /bin/bash)  # Cambiar a bash
```

---
## bash

### Instalar [Oh My Bash](https://github.com/ohmybash/oh-my-bash)

```sh
# Via curl
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"

# Via wget
bash -c "$(wget https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh -O -)"
```

Para cambiar el tema de Oh My Bash, editar el archivo `~/.bashrc`, editar la siguiente linea eligiendo el nombre de algun tema del [siguiente enlace](https://github.com/ohmybash/oh-my-bash/wiki/Themes)
```sh
# ~/.bashrc

# Change
OSH_THEME="powerline"

# For
OSH_THEME="rr" # or "axin", "bake", "cooperkid", "duru", "pure", "purity", "rana"
```

Con esto ya tendremos configurado la shell para nuestro usuario y no el root, para ello entraremos en el entorno `root` y luego enlazar el archivo `.bashrc` de root al del usuario.
```bash
sudo su
ln -s -f /home/<USER>/.bashrc /root/.bashrc

# Si existe...
rm /root/.bashrc
```


---
## zsh

### Instalar plugins (sin Oh my zsh)

Instalar [sudo plugin](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/sudo/sudo.plugin.zsh):

```sh
sudo su
cd /usr/share
mkdir zsh-sudo
chown <USER>:<USER> zsh-sudo/
exit
cd /usr/share/zsh-sudo
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/plugins/sudo/sudo.plugin.zsh
```

Los siguientes plugins a instalar seran [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) y [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

```sh
sudo pacman -S zsh-autosuggestions zsh-syntax-highlighting locate
```

Localizaremos los archivos de los plugins con los siguientes comando

```sh
sudo updatedb
locate zsh-syntax-highlighting.zsh
locate zsh-autosuggestions.zsh
```

Ahora modificaremos el archivo `~/.zshrc` para agregar los plugins con sus respectivas localizaciones del resultado de `locate`

```sh
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-sudo/sudo.plugin.zsh
```

---
### Instalar [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Los plugins a instalar seran [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) y [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) dentro de la carpeta `.oh-my-zsh`

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Agregar las siguientes lineas en el archivo `~/.zshrc`

```sh
plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)
```

---
### Powerlevel10k

Instalaremos [powerlevel10k](https://github.com/romkatv/powerlevel10k)

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

En el siguiente reinicio de terminal, comenzara un proceso para customizar la terminal con `powerlevel10k`, caso contrario, podemos ejecutar el comando `p10k configure` para iniciarlo manualmente.

Verificar dentro de nuestro archivo `.zshrc` que este seleccionado el tema de Powerlevel10k

```sh
nano ~/.zshrc

  # Agregar/modificar la siguiente linea en el archivo .zshrc
  ZSH_THEME="powerlevel10k/powerlevel10k"
```


## root

Para el usuario root, no contara con toda esta configuracion. para ello, vamos a ejecutar los siguiente comandos
```sh
sudo su
chsh -s $(which zsh)
exec zsh

ln -s /home/<USER>/.zshrc /root/.zshrc

# Si existe...
rm /root/.zshrc

exit
sudo su

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k

# Si existe...
rm -r /root/powerlevel10k

exit
sudo su
```
