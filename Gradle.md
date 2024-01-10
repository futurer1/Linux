Install gradle package:
```
sudo apt update
sudo apt install gradle
```
 
Uninstall / Remove gradle package:

```
sudo apt remove gradle
sudo apt autoclean && sudo apt autoremove
```

Commands:
```
gradle tasks
```
```
gradle build
```

Создать необходимый wrapper
```
task wrapper1(type: Wrapper) {
    gradleVersion = '7.4.2'
}

выполнить task: gradle wrapper1
```

Сборка через wrapper
```
./gradlew clean build
```


fat jar task for build.gradle (with module):
```java
plugins {
    id 'application'
    id 'com.example.java-application-conventions'

}

dependencies {
    implementation 'org.apache.commons:commons-text'
    implementation project(':utilities')
}

application {
    mainClass = 'com.example.app.App'
}


jar {
    archiveBaseName.set('gradleHelloWorld')
    archiveVersion.set('0.1')
    archiveClassifier.set('')
    manifest {
        attributes 'Main-Class': 'com.example.app.App'
    }

    duplicatesStrategy = DuplicatesStrategy.EXCLUDE

    from {
        configurations.runtimeClasspath.collect {
            it.isDirectory() ? it : zipTree(it)
        }
    }
}
```
