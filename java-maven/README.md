Maven Java application
----------------------

This project demonstrates the usage of Bazel to retrieve dependencies from
Maven repositories.

To build this example, you will need to
[install Bazel](http://bazel.io/docs/install.html).

The Java application makes use of a library in [Guava](https://github.com/google/guava), which is downloaded from a remote repository using Maven.

This application demonstrates the usage of rules `maven_jar` and `maven_server` to configure dependencies. The dependencies are configured in the `WORKSPACE` file.

Build the application by running:

```
$ bazel build :java-maven
```

Test the application by running:

```
$ bazel test :tests
```

To reproducing missing guava in the output .jdeps:

    $ bazel --bazelrc jdk10.bazelrc build //...
    
    $ cat bazel-out/darwin-fastbuild/bin/libjava-maven-lib.jdeps|strings
    //:java-maven-lib
    com.example.myproject

With jdeps:

    $ bazel build //...
    
    $ cat bazel-out/darwin-fastbuild/bin/libjava-maven-lib.jdeps|strings
    bazel-out/darwin-fastbuild/genfiles/external/com_google_guava_guava/jar/_ijar/jar/external/com_google_guava_guava/jar/com_google_guava_guava-ijar.jar
    //:java-maven-lib
    com.example.myproject

Using `-s` shows `-Xbootclasspath/p` when `--host_javabase` is java 8:

    $ bazel build -s //...
    $ bazel --bazelrc jdk10.bazelrc build -s //...
