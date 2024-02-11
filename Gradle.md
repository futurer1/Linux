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

[Youtube](https://www.youtube.com/watch?v=pSKY3-K9_qc)

Использование зависимостей из подключенной библиотеки (API scope) внутри модуля, к которому подключили библиотеку
(передача зависимостей):
```java

// плагин позволяет работать с библиотеками в зависимостях из подключенного модуля
plugins {
    id 'java-library'
}

dependencies {
    api "org.projectlombok:lombok:1.18.24"
}

// разрешение использовать модуль как библитеку (например, common)
jar.enabled = true

//В основном модуле подключаем этот common:
dependencies {
    implementation project(":common")
}
```

Подключение библиотек через импорт внешнего файла с HashMap содержащей зависимости:
```java
allprojects {
    apply plugin: 'java'
    apply from: "$rootProject.projectDir/dependencies.gradle"

    group = 'com.mikhail.telegram'
    version = '0.0.1'
    java.sourceCompatibility = JavaVersion.VERSION_17
    java.targetCompatibility = JavaVersion.VERSION_17

    configurations {
        compileOnly.extendsFrom annotationProcessor
        testCompileOnly.extendsFrom annotationProcessor
        testAnnotationProcessor.extendsFrom annotationProcessor
    }

    repositories {
        mavenCentral()
    }

    dependencies {
        testImplementation platform(libsTest.junitBom)
        testImplementation(libsTest.jupiter)

        compileOnly libs.lombok
        annotationProcessor libs.lombok
    }

    test {
        useJUnitPlatform()
    }
}
```

Содержимое файла dependencies.gradle:
```java
    ext.libs = [
            "lombok" : "org.projectlombok:lombok:1.18.24",
    ]

    ext.libsTest = [
            'jupiter' : 'org.junit.jupiter:junit-jupiter',
            'junitBom' : 'org.junit:junit-bom:5.9.1',
    ]
```
