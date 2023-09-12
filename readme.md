## Documentacion de Linux

Esta es una pequeña documentacion, guia, blog; el cual, permite conocer y explorar sobre Linux, enfocado para ser utilizado en tu uso personal y tambien en el area de servidores.

Aprenderas los primeros pasos en los SO de Linux, como:

- Arch Linux
- Debian
- Open Suse
- Rocky Linux

Tambien conoceras la diferencia entre "Shell" y "Terminal".

Por ultimo, veremos como personalizar entornos de escritorio (Desktop Environments), firewalls y Qemu, un software para virtualizar.

Puedes ingresar al siguiente enlace para visualizar la documentacion:

[https://ojoshuacg.github.io/linux-docs/](https://ojoshuacg.github.io/linux-docs/)


---
## Clonar repositorio

Puedes clonar el repositorio, crear su entorno virtual e instalar sus dependencias:

``` 
git clone https://github.com/OJoshuaCG/linux-docs.git
cd linux-docs
python -m venv venv
source ./venv/bin/activate
pip install -r requirements.txt
```

Modifica los archivos de la carpeta linux-docs, puedes renombrarla si gustas. Para visualizar tu avance puedes ejecutar lo siguiente:

```
cd linux-docs
mkdocs serve
```


### Descripcion del proyecto

Este proyecto esta creado con el paquete [mkdocs](https://www.mkdocs.org/) de [python](https://www.python.org/). Permite desarrollar tu documentacion con ayuda de archivo markdown (.md).

```
pip install mkdocs
```

Además de utilizar el tema [material](https://squidfunk.github.io/mkdocs-material/), el cual tiene muchas caracteristicas para crear una documentacion atractiva y personalizable.

```
pip install material
```

---
## Empezar desde 0

Si deseas empezar desde cero tu proyecto con mkdocs, sigue los siguientes pasos:

```
pip install mkdocs material
mkdocs new <project-name>
cd <project-name>
mkdocs serve
```

