---
sidebar_position: 4
title: 4. Primera acción con Flutter
---

# Primera acción con Flutter

@Eugenio Tesio

Nuestra intensión con el curso, más allá de aprender, es que le quede código al estudiante que pueda reutilizar en sus proyectos, es por esto que nuestra __primera acción__ específica para Flutter será correr un par de __checkeos__ de código cada vez que se realize un `push` en el código.

## Creando el proyecto ejemplo

Utilizaremos el tipico ejemplo que viene con Flutter, para ello nos ubicamos en el root del proyecto de cicd que venimos utilizando y ejecutamos:

```bash
flutter create ./
```

Luego corremos el test para verificar si está todo ok.

```bash
flutter analyze
flutter test
```

## Agregando los checks con la acción push

Agregaremos un nuevo archivo en la carpeta de Workflows al cual llamaremos `all-branches-push-checks.yml` y copiaremos el siguiente código:

```yml
name: PR checks

on:
  push:

jobs:
  checks:
    runs-on: ubuntu-latest

    steps:
   
    - uses: actions/checkout@v2  # Acción externa que clona el directorio root del proyecto en la máquina virtual.
      
    - uses: subosito/flutter-action@v2 
      with:
        channel: stable # Acción externa que instala Flutter stable en la máquina virtual
    
    - run: flutter --version # Información útil
    
    - run: flutter pub get # Instalación de dependencias
  
    - run: flutter format --line-length=80 --set-exit-if-changed . # formateo del código

    # En caso de necesiten correr el generador de código, descomentar la línea de código de abajo.
    # - run: flutter pub run build_runner build
    
    - run: flutter analyze # Verificar problemas a través el análisis estático

    - run: flutter test # Correr los test
```

Los comandos ejectuados en el Workflow son los que nuestro equipo considera indispensables en el momento de subir código a nuestro repositorio. El comando `flutter pub run build_runner build` que se encuentra comentado muchas veces no es necesario, ya que muchos desarrolladores toman por convensión incluir los archivos generados `*.g.dart` en el repositorio, por lo cual no sería necesario ejecutarlo en el `push`.
