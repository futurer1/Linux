Как установить
--------------

С сайта https://jmeter.apache.org/ скачать бинарную версию https://dlcdn.apache.org//jmeter/binaries/

распаковать архив
```
unzip apache-jmeter-5.6.zip
```

переименовать папку
```
mv apache-jmeter-5.6 jmeter
```

перенести папку с содержимым в /opt
```
sudo mv jmeter /opt
```

добавить переменную окружения
```
echo 'export PATH="$PATH:/opt/jmeter/bin"' >> ~/.bashrc
```
применить новую конфигурацию
```
source ~/.bashrc
```

зайти и запустить
```
cd /opt/jmeter/bin
./jmeter.sh
```
