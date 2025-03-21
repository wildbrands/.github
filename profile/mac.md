# MAC

Esto applica solo si estas trabajando en un equipo con MACOS.

## Base

2 de las herramientas que te simplificaran la obtencion de herramientas y nuevas versiones son: Homebrew y Pyenv.

### Homebrew

Te permite instalar paquetes y otras herramientas creadas por la comunidad, esto te da muchas mas flexibilidades para encontrar y usar nuevas funcionalidades que puedes que no encuentres en la AppStore.

Para instalar homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Una vez instalado arrojara unas instrucciones que tienes que seguir para asegurar que quede reguistrado en tu terminal.

Link a [Homebrew](<https://brew.sh/>]

### Pyenv

Vital para instalar python, si puedes isntalarlo directamente, pero es muy probable que se te rompa la instalaccion por culpa de algun paquete (me ha pasado muuuultiples veces) y Pyenv te permite instalar multiples versiones en paralelo, manejar ambientes virtuales. Arreglar conflictos de librerias, etc.

Instalacion:

1. Instalacion base

    ```bash
    brew update
    brew install pyenv
    ```

2. Configurar terminal

    ```bash
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
    echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
    ```

3. Reinicia terminal

    ```bash
    exec "$SHELL"
    ```

## Herramientas trabajo

### VSCODE

Instalcion:

Extensiones:

### GCP

### DBT

Instalacion:

Extensiones:
