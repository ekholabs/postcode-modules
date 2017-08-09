# Postcode Checker Demo Application

The Postcode application is a project used to demonstrate the use of the coolest add-on to the JDK 9: Project Jigsaw.

### Requirements

  - [JDK 9](http://jdk.java.net/9/)

### One-liner Builder

It's important to go over the commands below and try to understand them. However, if you want to quickly build
and run the application, do the following:

  - ```./build.sh```

### Build Modules

  - ```javac --module-path nl.ekholabs.address.checker -d nl.ekholabs.postcode.validator $(find src/nl.ekholabs.postcode.validator -name "*.java")```
  - ```javac -p . -d nl.ekholabs.address.checker $(find src/nl.ekholabs.address.checker -name "*.java")```

#### Multi-module compilation

  - ```javac -d . --module-source-path src $(find src -name "*.java")```

### Run Application

  - ```java -p . -m nl.ekholabs.address.checker/nl.ekholabs.address.checker.api.Application 3252RG nl```

### Create a modular JAR (make sure 'bin' exists)

  - ```jar --create --file bin/postcodevalidator.jar --module-version=1.0 -C nl.ekholabs.postcode.validator .```

### Specify MainClass

  - ```jar --create --file bin/addresschecker.jar --module-version=1.0 --main-class=nl.ekholabs.address.checker.api.Application -C nl.ekholabs.address.checker .```

### Run module

  - ```java -p bin -m nl.ekholabs.address.checker 3452RG nl```

### Create a runtime image

  - ```jlink --module-path $JAVA_HOME/jmods:bin --add-modules nl.ekholabs.address.checker --output linkedmod```

### List modules from the image

  - ```linkedmod/bin/java --list-modules```

### Run application from the image

  - ```linkedmod/bin/java -m nl.ekholabs.address.checker 3452RG nl```

### Reducing image size

  - ```rm -rf linkedmod```
  - ```jlink --module-path $JAVA_HOME/jmods:bin --add-modules nl.ekholabs.address.checker --output linkedmod --compress=2```
