# Iris user documentation

This repository contains the Iris user documentation.

The documentation must be built with [Maven](http://maven.apache.org)
and the main Iris source code repository (at https://github.com/ChandraCXC/iris).

## To build

1. Clone the main Iris repository.

    ```
    git clone --recursive https://github.com/ChandraCXC/iris.git
    ```

2. `cd` into `iris` and run `mvn site:site -DskipTests`. This builds
   Iris locally on your machine. The built site can be accessed from
   `${basedir}/iris/target/site/index.html`. The goal `mvn site:run`
   will start a local webserver that can be viewed at `localhost:8080`.

    ```
    cd iris
    mvn site:site  # to skip running the tests
    mvn site:run   # to view the site in your browser
    ```

`site:run` also allows to show changes as the source code is edited.

Note that the submodules sites will not be reachable with the above instructions.

In order to test the full actual site, including submodules, you can use
the `site:stage` goal:

````
mvn site:site site:stage
````
