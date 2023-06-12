---
sidebar_position: 4
title: 4. First action with Flutter
---

# First action with Flutter

@Eugenio Tesio

Our intention with the course, beyond learning, is that the student is left with code that can be reused in their projects, that is why our __first action__ specific to Flutter will be to run a couple of __checks__ of code each time a `push` is performed on the code.

## Creating the example project

We will use the typical example that comes with Flutter, for this we go to the root of the cicd project that we have been using and run:

```bash
flutter create ./
```

Then we run the test to ensure that everything is OK.

```bash
flutter analyze
flutter test
```

## Adding checks with the push action

We will add a new file in the Workflows folder which we will call `all-branches-push-checks.yml` and copy the following code:

```yml
name: PR checks

on:
  push:

jobs:
  checks:
    runs-on: ubuntu-latest

    steps:
  
    - uses: actions/checkout@v2   # External action that clones the root directory of the project in the virtual machine.
        
    - uses: subosito/flutter-action@v2 
      with:
        channel: stable # External action that installs Flutter stable in the virtual machine
   
    - run: flutter --version # Useful information
    
    - run: flutter pub get # Dependencies installation
    
    - run: flutter format --line-length=80 --set-exit-if-changed . # code formatting

 # In case you need to run the code generator, uncomment the line of code below.
    # - run: flutter pub run build_runner build

    - run: flutter analyze # Verify problems through static analysis

    - run: flutter test # Running the tests
```

The commands executed in the Workflow are the ones that our team considers indispensable when uploading code to our repository. The `flutter pub run build_runner build` command that is commented is often not necessary, since many developers take by convention to include the generated `*.g.dart` files in the repository, so it would not be necessary to execute it in the `push`.
