# Телеграм бот Star-Wars-Bot


## Окна и диалоги

Бот построен на окнах и диалогах
у каждого окна есть своё состояние и кнопки

При нажатии кнопок бот вызывает getter для сохранения данных о кнопе или выдаче текста

При использовании кнопок бот переходит в следующее окно в зависимости от его состояния

## Маршрутизатор

файл router.py является маршрутизатором для диалогов

в этом же файле запускается базовый диалог при команде /start


## Модель

Модель User описана в виде:

- id - id пользователя
- tg_id - телеграм id пользователя

Модель Log описана в виде:

- id - id лога
- user_id - id юзера закреплённого за этим логом
- url - url запролса к API
- filter_name - названия фильтра
- param - объект по которому можно фильтровать
- arg_param - название поля объекта
- value - значение которое ввёл пользователь
- count_value - кол-во запросов которе ввёл пользоваетль
- date_of_log - дата записи лога
- status_request - статус запроса 200 - ОК 400 c запросом что то пошло не так
- count_obj - кол-во объектов которые вернулись к пользователю по фильтру

## DataClass, формат текста

DataClass используется для удобного форматирования текста

Текст делится на формат | JSON | Читабельный текст |

DataClass основан на схемах API
- https://swapi.dev/documentation

## Class API

Класс API иеет поиск по фильтру или по имени

Филтры:
- low - фильтрация типа |значение поля| <= |введёного значения|

- height - фильтрация типа |значение поля| >= |введёного значения|

- custom -  фильтрация типа |введёного значения 1|  >= |значение поля| >= |введёного значения 2|

Примечание: custom работает как в диапазоне (от - до) так и в диапазоне (до - от)


Валидация типов происходит по типу float если поле объекта не проходит валидацию то оно не учитывается в результате
        У каждого объекта есть своё поле фильтрации
        Так же бот принимает кол-во запрашиваемых объектов

        Примечание: Бот не выдаёт те API объекты в которых фильтруемое поле является None

        Каждое поле кроме поля name принимает в себя только цифры, при необхости найти объект по
        его имени используйте фильтрацию по полю name.

        Поле name ищет объект по его имени
        Пример: Sand Crawler найдёт объект чьё поле name: Sand Crawler

        Если ваше введённое значение или даипазон не совпадает по фильтрации со значением поля
        лбого объекта, то Бот вернёт 0 кол-во объектов

        Если вы введёте кол-во запрашиваемых объектов изначально привышающее кол-во объектов API
        То бот выдаст все объекты удовлетворяющие фильтрации

        Если кол - во удовлетворяющих фильтрации объектов меньше чем вы задали то бот вернёт так же
        все объекты удовлетворяющие фильтрации

        Иначе бот вернёт то кол-во объектов которе вы запросили

Для поиска по имени валидация не происходит

Объекты по которым можно фильтровать:

        people - Люди (персонажи)
        starships - Звездолеты
        vehicles - Техника
        species - Разновидности (рассы)
        planets - Планеты
        
У каждого объекта есть свои наборы полей по которым можно фильтровать


## История
В окне история отображается не больше 10 логов
Каждый последующий лог после 10 удаляет первый лог данного пользоватеял

## Помощь
В окне помощь есть подробное описание как пользоваться ботом

## Результат
Окно результата выдаёт объекты удовлетворяющие фильтру и значениям по которым данные запроса фильтруются.

Можно посмотреть любой объект в виде формате JSON


##

- Документация API https://swapi.dev/documentation
- Оригинальный сайт API https://swapi.dev/