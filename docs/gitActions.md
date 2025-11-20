# GitActions
---

Este documento relata que hay que hacer para crear una página web con **MKDocs** y como lo he hecho yo.

---

Para realizar esta tarea hay que utilizar dos ficheros principales **mkdocks.yml** que está en la raíz del proyecto y **CreacionDocumentacion.yml** el cual está en `.github/workflows/` y en este documento vamos a ver para que sirven cada uno de ellos.

## CreacionDocumentacion.yml
Este archivo tiene como tarea automatizar Github Actions y mediante su sintaxis podemos ver de forma clara cuales son sus directivas.

![creacionDocumentacion]()
`yml` :  
```
name: Deploy MkDocs

on:
  push:
    branches:
      - main

permissions:
  contents: write
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repo
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: pip install mkdocs

    - name: Deploy docs
      run: mkdocs gh-deploy --force
      env:
        GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Este es un archivo bastante largo así que iré explicandolo poco a poco.

- name
    + Sirve para darle nombre a la tarea en la página de *Actions* en Github.
- on:push:branches:
    + Este bloque dicta cuando deberá empezar la ejecución , en este caso cuando se haga una modificación en *main* .
- permissions
    + El nombre es autodescriptivo aquí se definen los permisos que necesitará el archivo para ejecutar la tarea.
- jobs
    + Hemos llegado a lo más importante, los jobs son como se me ocurre a mi llamarlos el centro de este documento , basicamente tienen lo que se va a ejecutar y la tarea principal de este fichero , podemos apreciar que tiene subapartados dentro, estos son los **pasos** que tiene que seguir el documento para funcionar, aquí podemos ver que primero hace un checkout del repositorio, luego descarga phyton (ya que mkdocks funciona en python) para proseguir descargando MKDocs y termina ejecutando un comando que despliega la página web y que  fuerza con --force.

## mkdocks.yml

Proseguimos con mkdocks.yml , este es el que controla la página web y los archivos markdown.

![mkdocks]()

`yml` :  
```
site_name: Práctica Unidad 0 PPS - HectorBG
nav:
  - Indice: index.md
  - Git: git.md
  - GitActions: gitActions.md
  - Docker: docker.md
  - Conclusiones personales: conclusiones.md
docs_dir: docs
```
Este archivo es bastante más sencillo e intuitivo para cualquier ojo comparado al anterior.

- site_name
    +Es el nombre que aparecerá arriba del todo, en mi caso será ***Práctica Unidad 0 PPS - HectorBG*** 
- nav
    + Este apartado especifica lo que va a salir en la barra de navegación de arriba y a que documentos están enlazados.
- docs_dir
    + Referencia al directorio que contiene todos los documentos que utiliza la página.

