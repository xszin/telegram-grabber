# Telegram Grabber v2.4 2024
# Телеграм Граббер v2.4 2024
Бот позволяет пересылать весь контент с любого telegram канала на ваш канал без упоминания автора канала. Также есть возможность заменить ссылки и упоминания в постах на ваши

# RoadMap
- [x] 02.01.24 Добавил инлайн-меню, режим модерации, перезагрузку бота из онлайн меню, добавление каналов без команд (по нажатию на инлайн-меню), обновил инструкцию

- [x] 10.01.24 Добавил возможность добавлять каналы по @username; Задал версию клиента при авторизации для решения возможной проблемы с вылетом на всех устройствах

- [x] 11.01.24 Фикс отображения встроенных ссылок при замене; Теперь все переменные, которые нужно менять, **заполняются в файле config.py**

- [x] 11.01.24 Внедрение Chat GPT - в режиме модерации добавил кнопку "Рерайтинг текста" (Работает только с одиночными сообщениями, если отправляется альбом, то кнопки не будет). Текст по нажатию на кнопку должен будет переписать Chat GPT для создания уникальной публикации.

- [x] 12.01.24 Добавил запрет на все команды(/) для пользователей, чьи id не совпадают с my_id из config.py

- [x] 21.01.24 Исправил проблему при которой не пересылались сообщения, в которых есть превью; Починил соответствия; Добавил кнопку "Показать соответствия" в инлайн-меню; Исправил баг с частью нерабочих кнопок инлайн-меню, **поменял файл config.py**


# Используемые библиотеки

_Всё тестировалось на Python 3.11_

Для работы бота необходимо установить библиотеки.

Библиотека aiogram:

    pip install aiogram==2.25.1
_(Если в будущем предложит обновить библиотеку aiogram, то не нужно. Всё работает только на версии 2.25.1)_

Библиотека telethon:   
 
    pip install telethon
_В данный момент всё стабильно работает на последней версии библиотеки telethon (1.33)_


Библиотека httpx: (proxy для работы Chat GPT)

    pip install httpx


# Как запустить

1. Создать телеграм-бота. Для этого нужно написать боту [BotFather](https://telegram.me/botfather) и следовать инструкциям. После этого сохраните токен бота.
2. Получить api_id, api_hash. Сделать это можно на сайте [my.telegram.org](https://my.telegram.org/auth). Инструкция: https://www.youtube.com/watch?v=JBDnmEhvgac
3. Задать переменные api_id, api_hash, bot_token и my_id в файле config.py. Также заполните id технического канала (Смотреть 6 пункт)

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/e06a14e4-e2cc-4873-9f84-1b0ee28f654e)


my_id брать в [Get My ID](https://t.me/getmyid_bot) отсюда (отправить в бот любое сообщение, он выдаст ваш id):

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/10a83730-3708-47d7-a134-f700ef037c4d)



Запустить бота командой:

    python main.py

**При первом запуске нужно ввести НОМЕР ТЕЛЕФОНА (НЕ ТОКЕН) и код, который придёт в telegram**

# Пример использования:
1. Переходим в telegram бот, который создали в начале. Вводим команду "/start", нажимаем "Добавить канал" и вводим id канала, с которого нужно брать контент. 
id нужного канала можно узнать переслав любое сообщение с канала в бот (пример id для каналов: -1001009232144) [Get My ID](https://t.me/getmyid_bot)
![image](https://user-images.githubusercontent.com/91873172/236866756-06b5a78f-0b58-45f2-a238-ce6e40550b8a.png)

Можно вводить и username через "@", но через id стабильнее работает. **Если через id не получается вводим @username**

2. Добавляем канал, на который должны будут приходить сообщения. Для этого жмём "Добавить канал-получатель". Бот, в котором мы всё это вводим, обязательно должен быть администратором этого канала.
3. **Обязательно** указываем соответсвие между каналами (это пригодится когда добавите несколько каналов-источников и несколько каналов-получателей, при этом хотите чтобы публикации из определённых каналов приходили на конкретные каналы) написав id канала-источника и id канала-получателя через пробел командой /set_channel_mapping (Пример: /set_channel_mapping -100123132890 -1000932314321).
4. После этого перезагружаем код либо вручную закрыв и открыв компилятор кода (стабильнее всего), в котором работаем, либо по кнопке "Перезагрузить бота" (не стабильно). **Теперь все новые сообщения будут приходить на ваш канал.**
5. Также вам доступна команда

    /last_messages ко-во сообщений или all, если все
    
Она отправляет последние сообщения на ваш канал. Если добавили несколько каналов-источников, а последние сообщения нужны только с одного канала, то напишите

    /last_messages id канала источника ко-во сообщений

6. Режим модерации. При активации режима модерации все сообщения будут приходить сначала на ваш технический канал, в котором вы можете их редактировать, удалять и публиковать:

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/cbdf1fb7-e5b0-4870-b01a-59a514785abd)


![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/d6cf2ccf-f474-4bf0-b371-d3ad3cf0c77e)


Для его работы создаём новый пустой канал и вводим id этого канала в technical_channel_id в файле config.py. (получить id можно по аналогии как с остальными каналами). Не забываем назначить бота администратором технического канала.


Если вы отредактировали сообщение, то нажимайте на "Отредактировано" чтобы оно обновилось в хранилище. Возможный баг: когда в техническом канале скапливается большое количество сообщений, то при нажатии на "Отправить" может зависать. Чтобы всё заработало нажимаем на "Отредактировано", а потом "Отправить".

**Также есть возможность заменять все ссылки и упоминания, которые публикуются на каналах на ваши**. В файле config.py замените на нужные вам

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/f563501d-7f12-4316-877e-4f99918f9ce9)


**Рерайт текста с Chat GPT**. В режиме модерации есть кнопка "Рерайт текста". Для её работы заполняем proxy_url и openai_api_key в файле config.py. proxy_url должны быть формата HTTP или HTTPS. Если у вас прокси с логином и паролем, то в настройках прокси ставьте авторизацию по вашему ip. 
Даже если прокси HTTPS, то тут всё равно должно быть http:
![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/36bdced9-73ef-4d94-8fe5-655c02fe69a6)

openai_api_key берётся на сайте openai https://platform.openai.com/api-keys при наличии бюджета в https://platform.openai.com/usage . При отсутствии прокси и openai_api_key, то оставьте эти данные пустыми, либо за покупкой можно обратиться ко мне.

Подписывайтесь на наш телеграм канал: https://t.me/my_grab

# Список доступных команд:
* /start - Начало работы с ботом
* /help - Получить список доступных команд
* /add_channel - Добавить канал для работы
* /remove_channel - Удалить канал из списка
* /list_channels - Показать список добавленных каналов
* /add_destination_channel - Добавить канал-получатель
* /remove_destination_channel - Удалить канал-получатель из списка
* /list_destination_channels - Показать список каналов-получателей
* /set_channel_mapping - Установить соответствие между каналами
* /last_messages (ко-во сообщений или all, если все) - Отправить последние сообщения с каналов


# Если хотите поддержать проект

ЮMoney: 410011379451106

Карта МИР: 2204120200078646


Буду очень благодарен!
