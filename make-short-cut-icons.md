```
cd /usr/share/applications/
```

```
sudo touch my-program-name.desktop
```

```
sudo nano my-program-name.desktop
```

insert text:
------------
[Desktop Entry]
Name=Idea Ultimate                                        //название ярлыка
Comment=
GenericName=
Keywords=idea                                            //ключевые слова, по которым будет находиться в поиске приложений
Exec=/bin/bash -i -c "/home/user/idea-IU-232.10203.10/bin/idea.sh" %f       //исполняемая команда (чтобы было видно переменные окружения в Idea)
Terminal=false
Type=Application
Icon=/home/user/idea-IU-232.10203.10/bin/idea.png        //путь к иконке приложения
Path=
Categories=Development                                   //категория в которой будет отображаться ярлык
NoDisplay=false

example
-------
```
[Desktop Entry]
Name=Idea Ultimate
Comment=
GenericName=
Keywords=idea
Exec=/bin/bash -i -c "/home/user/idea-IU-232.10203.10/bin/idea.sh" %f
Terminal=false
Type=Application
Icon=/home/user/idea-IU-232.10203.10/bin/idea.png
Path=
Categories=Development
NoDisplay=false
```
