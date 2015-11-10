# Iris user documentation

This repository contains the Iris user documentation. The user docs
are based on [Iris v2.1](https://cxc.cfa.harvard.edu/iris/v2.1).

The documentation must be built with [Maven](http://maven.apache.org)
and the main Iris source code repository (at https://github.com/ChandraCXC/iris).

## To build

1. Clone the main Iris repository.

    ```
    git clone --recursive https://github.com/ChandraCXC/iris.git
    ```

2. `cd` into `iris` and run `mvn site:site -DskipTests`. This builds
   Iris locally on your machine. The built site can be accessed from
   `${basedir}/iris/target/site/index.html`.

    ```
    cd iris
    mvn site:site -DskipTests     # to skip running the tests
    open target/site/index.html   # to view the site in your browser
    ```
