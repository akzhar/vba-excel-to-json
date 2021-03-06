# vba-excel-to-json - конвертер данных из Excel в JSON

Данные, хранящиеся в виде таблиц в Excel, преобразуются VBA макросом в формат JSON.

## Как пользоваться конвертером

- Данные должны храниться в соотвествиями с правилами (см. ниже + описаны на странице `Инструкция` в файле `EXCEL to JSON.xlsm`)
- На странице `Инструкция` указываем:
    - имя файла, например `data.json`
    - путь к файлу, например `C:\data\`
- Нажимаем кнопку `EXCEL → JSON` → получаем файл `C:\data\data.json`

<img src="https://raw.githubusercontent.com/akzhar/vba-excel-to-json/main/demo.gif" alt="demo" title="demo" width="100%"/>

## Правила хранения данных в Excel

- Корневым JSON объектом / массивом объектов является страница ROOT

На каждой из страниц файла Excel данные хранятся в виде объекта / массива объектов:

- 1 вкладка = 1 поле корневого объекта / массива объектов с именем = имени вкладки
- 1 вкладка = 1 объект / массив объектов
- Первая строка хранит имена полей объекта
- На остальных строках хранятся значения полей объекта
- 1 колонка = 1 поле объекта
- 1 строка = 1 объект

Значением свойства объекта может быть:

- Простое значение (формат JSON хранит все значения в виде строк)
- Массив простых значений:
    - обозначается квадратными скобками `[ ... ]`
    - внутри скобок через запятую указываются эл-ты массива `[ элемент1 , элемент2 , элемент3 ]`
    - не допускается вкладывать массив простых значений в массив простых значений → `[ элемент1 , [ ... ] , элемент3 ]`
- Другой объект / массив объектов:
    - обозначается фигурными скобками `{ ... }`
    - внутри скобок должно быть указано имя вкладки, строки которой будут преобразованы в объекты
    - если строк на вкладке > 2, будет возвращен массив объектов, иначе один объект
    - допускается вкладывать объект / массив объектов в массив простых значений → `[ { ... } ]`
