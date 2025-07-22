# Gradle practical tasks

## 1. Install required software locally (latest version of Gradle, Java).

Done.

## 2. ​​Go to https://github.com/spring-projects/spring-petclinic, fork it, and clone the forked repo.

Done.

## 3. Check what tasks are available for the project.

**Command:**

```bash
./gradlew tasks
```

**Result:**

<p align="center"> <img src="img/img1.png" alt="Img" width="80%"> </p>

## 4. Run all available project tests.

**Command:**

```bash
./gradlew test
```

**Result (got an error - it seems Gradle can't find Java 17 on the machine):**

<p align="center"> <img src="img/img2.png" alt="Img" width="80%"> </p>

On the macine I have installed Java 21, so I just replaced version in the build.gradle from 17 to 21 instead and it works fine:

```java
java {
  toolchain {
    languageVersion = JavaLanguageVersion.of(21)
  }
}
```

<p align="center"> <img src="img/img3.png" alt="Img" width="80%"> </p>

## 5. Build the project and run it, and verify it’s available on the localhost in the browser.

**Command:**

```bash
./gradlew build
```

**Result:**

<p align="center"> <img src="img/img4.png" alt="Img" width="80%"> </p>

To run project we can use two commands: `run` or `bootRun`. The difference is that `bootRun` is a Gradle task provided by the Spring Boot Gradle plugin (includes all dependencies and Spring Boot features, loads Spring Boot’s embedded server), however `run` task does not include Spring Boot-specific setup and will not start the embedded Tomcat server properly.

**Command:**

```bash
./gradlew bootRun
```
**Result:**

<p align="center"> <img src="img/img5.png" alt="Img" width="80%"> </p>


## 6. Perform the cleanup.

**Command:**

```bash
./gradlew clean
```
**Result:**

After the command execution, web-site stopped be available.


## 7. Explore gradle-related files. Identify which gradle file defines the project name and change it. Build the project again and verify the new project name is being used (you need to find .jar files).

Name of the project is located in the `settings.gradle` file.

```
rootProject.name = 'spring-petclinic'
```

After changing the value of the `rootProject.name` variable and project rebuilding, Gradle generated ".jar" file with the new name:

<p align="center"> <img src="img/img6.png" alt="Img" width="80%"> </p>


## 8. Create an additional custom task, which depends on the build task (so by calling this task the build and test tasks will also be executed). It should open the browser with generated test results.

In the `build.gradle` paste this task definition:

```
task testReport(dependsOn: build) {
  doLast {
    def testReportUrl = "file://${project.buildDir}/reports/tests/test/index.html"
    exec { commandLine "open", testReportUrl }
  }
}
```

* `doLast` -  the action to perform after the build finishes 
* `file://` — this scheme tells that it’s a local file, not an HTTP/HTTPS URL

**Result:**

<p align="center"> <img src="img/img7.png" alt="Img" width="80%"> </p>


## 9. Add the dynamic versioning to your project using the commonly used axion-release-plugin (GitHub - allegro/axion-release-plugin: Gradle release & version management plugin.). Check the Version your project (Gradle best practice tip #5) to find the tutorial on how to do this.


## 10. Check the new available commands after the plugin addition. Using these new commands, check the current project version. Then add and commit some changes to the project and make the project release. Check the current version one more time and git tags available. Note the difference between SNAPSHOT and release versions.


## 11. Perform the cleanup.


Hint: you may need the following documentation while working on the practice task:

Authoring Tasks
The Java Plugin
Version your project (Gradle best practice tip #5)
Gradle task to open a url in the default browser - Stack Overflow
