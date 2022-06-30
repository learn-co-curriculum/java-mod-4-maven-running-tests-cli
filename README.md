# Running Tests

## Learning Goals

- Add the Surefire plugin.
- Run tests using Maven.

## Introduction

Maven can’t run the tests by itself. It requires the `maven-surefire-plugin` to
run tests. In this lesson, we will install the plugin and look at how we can run
our tests.

## Add the Surefire Plugin

Add the following lines in the `<plugins>` section of your `pom.xml` file:

```xml
<plugin>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>3.0.0-M7</version>
</plugin>
```

Your POM file should look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>example-app</artifactId>
  <version>1.0-SNAPSHOT</version>

  <name>example-app</name>
  <url>http://www.example.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <version>5.8.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.10.1</version>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.2.2</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>org.example.App</mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.0.0-M7</version>
      </plugin>
    </plugins>
  </build>
</project>
```

## Run the Tests

We can now use the `mvn test` command to run tests. Here’s the output of the
command:

```bash
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.example:example-app >-----------------------
[INFO] Building example-app 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ example-app ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 0 resource
[INFO]
[INFO] --- maven-compiler-plugin:3.10.1:compile (default-compile) @ example-app ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ example-app ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 0 resource
[INFO]
[INFO] --- maven-compiler-plugin:3.10.1:testCompile (default-testCompile) @ example-app ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M7:test (default-test) @ example-app ---
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running org.example.AppTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.017 s - in org.example.AppTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.641 s
[INFO] Finished at: 2022-06-29T14:19:42-04:00
[INFO] ------------------------------------------------------------------------
```

The `mvn test` command automatically compiles the program before running the
tests. By default, it runs all the test classes it can find in the project.

We can run specific tests by using the `-Dtest` flag with the `mvn` command. You
can learn more about it in
[the documentation](https://maven.apache.org/surefire/maven-surefire-plugin/examples/single-test.html).

## Conclusion

Running tests is an integral part of the development process. Maven makes it
convenient for developers to add the necessary testing libraries and run tests
as part of the build process.
