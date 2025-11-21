# MAC

Esto applica solo si estas trabajando en un equipo con MACOS.

## Base

3 de las herramientas que te simplificaran la obtencion de herramientas y nuevas versiones son: Homebrew y Pyenv. También recomendamos VSC como editor, aunque puede usar el que quiera.

### Visual Studio Code

Link instalcion: [VS Code](https://code.visualstudio.com/download)
Escoger si es Intel o Apple (chips M algo) y seguir las instrucciones.

### Homebrew

Te permite instalar paquetes y otras herramientas creadas por la comunidad, esto te da muchas mas flexibilidades para encontrar y usar nuevas funcionalidades que puedes que no encuentres en la AppStore.

Para instalar homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Una vez instalado arrojara unas instrucciones que tienes que seguir para asegurar que quede reguistrado en tu terminal.

Link a [Homebrew](<https://brew.sh/>)

### Pyenv

Vital para instalar python, si puedes isntalarlo directamente, pero es muy probable que se te rompa la instalaccion por culpa de algun paquete (me ha pasado muuuultiples veces) y Pyenv te permite instalar multiples versiones en paralelo, manejar ambientes virtuales. Arreglar conflictos de librerias, etc.

Instalacion:

1. Instalacion base

    ```bash
    brew update
    brew install pyenv
    brew install pyenv-virtualenv
    ```

2. Configurar terminal

    ```bash
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
    echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
    echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
    ```

3. Reinicia terminal

    ```bash
    exec "$SHELL"
    ```

Ahora puedes usarlo con normalidad para instalar python:

```bash
pyenv install 3.11
pyenv global 3.11
```

## Herramientas trabajo

Herramientas varias que sirven directamente a como estamos trabajando en WILD (independiente si LAMA o FOODS), junto con algunas mejoras en calidad de vida.

### GCP

Basicamente toda nuestra operacion en la nube esta apalancada en GCP y la idea de instalar el Cliente de GCP de forma local es poder simplificar la conexion a esta.

En general el step by step se puede encontrar en: [Cloud SDK](https://cloud.google.com/sdk/docs/install). Pero indicare de todas maneras los principales pasos y unas configuraciones que realizar:

1. Descargar el archivo de [Cloud SDK](https://cloud.google.com/sdk/docs/install) correspondiente a tu OS/procesador y dejar en alguna carpeta que no vayas a borrar, ejemplo Documentos > Google Client
2. Descomprimir en la carpeta
3. Abrir un terminal en esa carpeta e instalar:

    ```bash
    ./google-cloud-sdk/install.sh
    ```

   1. Recomiendo seguir todos los pasos que indique y si aparece algun mensaje de si quiere incluir algo a PATH hacerlo o poner que si
4. Reiniciar el termial

    ```bash
    exec "$SHELL"
    ```

5. Inicial el cliente

    ```bash
    ./google-cloud-sdk/bin/gcloud init
    ```

    1. Deberia abrir un buscardor con una pagina de login, ingresar su correo institucional.
    2. Cuando pregunte projecto por defecto, ingresar el correspondiente a su empresa
       1. WFCL: prj-wfcl-p-data-share
       2. WLMX: prj-wfmx-p-data-share
       3. WL: prj-wlcl-p-data-share
    3. Cuando pregunte una region/zona por defecto, solo apretar enter y seguir.
6. Finalmente autorizar el cliente en GCP y Drive:
    1. Este paso es importante para que te deje acceder bien al contenido de la nube y a lo que quieras de Google Drive.

    ```bash
    gcloud auth application-default login \
        --scopes="https://www.googleapis.com/auth/drive","https://www.googleapis.com/auth/cloud-platform"
    ```

### DBT

La instalaccion de DBT es bien directa, ya que se apalanca de Python para su funcionamiento:

```bash
pip install dbt-core dbt-bigquery
```

Una vez instalados ya se puede usar de forma regular, recomiento mirar la extension [Power User for dbt](<https://marketplace.visualstudio.com/items?itemName=innoverio.vscode-dbt-power-user>) para simplificar su uso.

Recomiendo mirar tambien el quickstart de DBT, puede tener algunas explicaciones extra: [DBT](https://docs.getdbt.com/docs/get-started-dbt)

## Extra: Extensiones VC Code

En caso de que escojas usar VS Code para trabajar, aqui te dejo un listado de extensiones que te podrian servir:

- Extension de GCP: [Google Cloud Code](<https://marketplace.visualstudio.com/items?itemName=googlecloudtools.cloudcode>)
- Herramientas de calidad de vida para DBT: [Power User for dbt](<https://marketplace.visualstudio.com/items?itemName=innoverio.vscode-dbt-power-user>)
- Formateo de codigo Pyhton: [Black Formatter](<https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter>)
- Mejor notificacion de errores: [Error Lens](<https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens>)
- Mejor visualizacion de cambios en git: [Git Lens](<https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens>)
- Mayor visibilidad de indentacion: [indent-rainbow](<https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow>)
- Notebooks de python: [Jupyter Notebooks](<https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter>)
- Ultimas versiones de los paquetes en archivos requirements.txt: [Python PyPI Assistant](<https://marketplace.visualstudio.com/items?itemName=twixes.pypi-assistant>)
- Identificacion de columnas en CSV: [Rainbow CSV](<https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv>)
- Formateo al guardar: [Run on Save](<https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave>)

Le voy a dar un doble click a este ultimo, este lo utilizo en especifico para formatear los archivos .sql cuando guardo, y para que quede funcionando hay que hacer lo siguiente:

1. Instalar sqlfmt:

   ```bash
   pip install "shandy-sqlfmt[jinjafmt]"
   ````

2. Editar settings.json:
   1. command + P en mac o en la barra superior al centro, donde esta la lupita:
   2. \>Preferences: Open User Settings (JSON)
   3. agregar al final del JSON:

    ```json
    "emeraldwalk.runonsave": {
        "commands": [
        {
            "match": ".*\\.sql(\\.jinja)?",
            "isAsync": false,
            "cmd": "sqlfmt ${file}"
        }
        ]
    }
    ```

Y listo, ahora cuando guardes un archivo SQL se realizara el formateo automatico.
