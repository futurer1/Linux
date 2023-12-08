Как установить
--------------

С сайта https://jmeter.apache.org/ скачать бинарную версию https://dlcdn.apache.org//jmeter/binaries/

Распаковать архив
```
unzip apache-jmeter-5.6.zip
```

Переименовать папку
```
mv apache-jmeter-5.6 jmeter
```

Перенести папку с содержимым в /opt
```
sudo mv jmeter /opt
```

Добавить переменную окружения
```
echo 'export PATH="$PATH:/opt/jmeter/bin"' >> ~/.bashrc
```
Применить новую конфигурацию
```
source ~/.bashrc
```

Зайти и запустить
```
cd /opt/jmeter/bin
./jmeter.sh
```

Можно создать ярлык
```
cd /usr/share/applications/
sudo touch jmeter.desktop
sudo nano jmeter.desktop
```

Вставить в файл конфигурации ярлыка
```
[Desktop Entry]
Name=Apache Jmeter
Comment=
GenericName=
Keywords=jmeter
Exec=/opt/jmeter/bin/./jmeter.sh
Terminal=false
Type=Application
Icon=/opt/jmeter/docs/images/jmeter_square.png
Path=
Categories=Development
NoDisplay=false
```
