Установка Idea.
----------------

0. Установить java (`sudo apt install openjdk-17-jdk`)
просмотр других установленных версий java: `sudo update-alternatives --config java`
  
2. Скачать архив
3. Распаковать в home directory.
4. `cd ~/idea-IU-233.14808.21/bin`
5. `.\idea.sh`
6. Создать shortcut icon в окне с выбором проектов.

Чтобы всё было красиво:
```
rm -rf .java/.userPrefs
```


Для работы с Lombok в Idea добавить в 
Setting:
    Build, Execution, Deployment -> Compiler -> Shared build process VM options
опцию
-Djps.track.ap.dependencies=false

