# Telegram Grabber
Бот позволяет пересылать весь контент с любого telegram канала (если админ канала не запретил копирование контента) на ваш канал без упоминания автора канала. Также есть возможнос заменить все ссылки и упоминания в постах на ваши


# Используемые библиотеки

Для работы бота необходимо установить библиотеки.

Python:
   
    sudo apt-get update
    sudo apt-get install python3

Библиотека aiogram:

    pip install aiogram

Библиотека telethon:   
 
    pip install telethon

Библиотека pickle:

    pip install pickle

Библиотека re:

    pip install re

# Как запустить

1. Создать телеграм-бота. Для этого нужно написать боту [BotFather](https://telegram.me/botfather) и следовать инструкциям. После этого сохраните токен бота.
2. Получить api_id, api_hash. Сделать это можно на сайте [my.telegram.org](https://my.telegram.org/auth).
3. Задать переменные api_id, api_hash и bot_token в файле main.py.

![image](https://user-images.githubusercontent.com/91873172/236864151-bc15d37b-d1dc-4abf-bdf7-71c8268d4d3f.png)

Запустить бота 
мандой:

    python main.py

**При первом запуске нужно ввести номер телефона и код, который придёт в telegram**

# Пример использования:
1. Переходим в telegram бот, который создали в начале и добавляем id каналов, с которых нужно брать контент командой /add_channel (/add_channel -2312312312). 
id нужного канала можно узнать переслав любое сообщение с канала в бот [Get My ID](https://t.me/getmyid_bot)
![image](https://user-images.githubusercontent.com/91873172/236866756-06b5a78f-0b58-45f2-a238-ce6e40550b8a.png)

2. Добавить канал, на который должны будут приходить сообщения командой /add_destination_channel (/add_destination_channel -321312311). Бот, который вы создали в начале обязательно должен быть администратором этого канала.
3. Указать соответсвие между каналами написав id канала-источника и id канала-получателя через пробел командой /set_channel_mapping (/set_channel_mapping -100123132890 -1000932314321). **Теперь все новые сообщения, которые будут публиковать будут приходить на ваш канал.**
4. Также вам доступна команда

    /last_messages ко-во сообщений или all, если все
    
Она отправляет последние сообщения на ваш канал. Если добавили несколько каналов-источников, а последние сообщения нужны только с одного канала, то напишите

    /last_messages id канала источника ко-во сообщений
    
**Также есть возможность заменять все ссылки и упоминания, которые публикуются на каналах на ваши**. В поиске редактора кода найдите все упоминания "test" и вставь нужное вам:
![image](https://user-images.githubusercontent.com/91873172/236871594-5904f387-637a-4df4-894e-b54c3a6ab9a6.png)
Тоже самое со ссылкой:
![image](https://user-images.githubusercontent.com/91873172/236871955-47e04ae3-5db4-4f55-b2f6-f95f28b1c6e0.png)


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



Сообщения в исходном канале могут быть как текстовыми, так и содержать медиа-файлы (фото, документы).

Когда бот обнаруживает новое сообщение в исходном канале, он заменяет все упоминания пользователей на новое значение, заданное в переменной new_link, и пересылает его во все заданные каналы.
Вставьте нужное вам упоминание сюда

Также бот умеет обрабатывать альбомы (группы сообщений, содержащих медиа-файлы) и пересылать их в заданный канал в виде одного сообщения с общим описанием и медиа-файлами.

Списки идентификаторов каналов хранятся в файле *.pickle для сохранения настроек после перезапуска бота.
