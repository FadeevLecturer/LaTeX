# Настройка проверки русской грамматики в TeXstudio

По умолчанию TeXstudio проверяет грамматику только для английского языка. 
Если начать набирать русский текст, то редактор будет подсвечивать каждое слово крассным цветом, даже если этот текст абсолютно корректен с точки зрения правил русского языка.
Чтобы "подружить" TeXstudio с русским языком, необходимо установить русский словарь. Ниже прилагается инструкция.

1. Скачайте файлы [russian_english.aff](./russian_english.aff) и [russian_english.dic](./russian_english.dic). 
2. Найдите папку с установленным TeXstudion (у меня это "C:\Program Files (x86)\texstudio") и положить скачанные файлы в папку dictionaries.
3. Далее в TeXstudio в меню "Options" выбираем "Configure TeXstudio". В открывшемся окне выбираем пункт "Language checking".
4. Необходимо убедиться, что напротив пункта "Spelling Dictionary Directories" стоит та директория, куда вы положили скачанные файлы (у меня это "C:\Program Files (x86)\texstudio\dictionaries").
5. Напротив пункта "Default language" необходимо выставить "russian_english". 
