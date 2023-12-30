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
