# <p align="center">Hotels.com Python Telegram Bot

Telegram бот для поиска подходящих отелей с сайта [Hotels.com](https://www.hotels.com/).



## Как запустить бота:

- Скачать скрипт:
```commandline
git clone https://gitlab.skillbox.ru/iurii_ilin_1/PA_Python_DPO_bot
```
- Установить необходимые библиотеки, прописанные в файле __`requirements.txt`__:
```commandline
pip install pyTelegramBotAPI
```
```commandline
pip install python-dotenv
```
```commandline
pip install peewee
```
```commandline
pip install loguru
```
```commandline
python -m pip install requests
```
- Создать Telegram бота у [BotFather](https://t.me/BotFather) и получить токен.
- Получить ключ от [RapidAPI](https://rapidapi.com/hub/):
    - Зарегистрироваться на сайте. 
    - Перейти в API Marketplace → категория Travel → Hotels (либо просто перейти по прямой ссылке на документацию [Hotels API Documentation](https://rapidapi.com/apidojo/api/hotels4/)).
    - Нажать кнопку __Subscribe to Test__.
    - Выбрать бесплатный пакет __Basic__.
    - Забрать KEY.
- Создать файл __.env__ и прописать там BOT_TOKEN и RAPID_API_KEY так, как прописано в файле .env.template
- Запустить бота в своей IDE или в командной строке:
```commandline
python main.py
```

## Возможности бота:

__Бот реагирует на команды:__
- __/start__ - Перезапустить бота.
- __/help__ - Помощь.
- __/lowprice__ - Топ самых дешёвых отелей в городе.
- __/highprice__ - Топ самых дорогих отелей в городе.
- __/bestdeal__ - Топ отелей, наиболее подходящих по цене и расположению от центра.
- __/history__ - История поиска отелей.
- __/delete_history__ - Очистить историю поиска.

## Принцип работы:

После ввода команд __/lowprice__, __/highprice__ и __/bestdeal__ у пользователя запрашивается:
- Город, где будет проводиться поиск.
- Количество отелей (максимум 15).
- Необходимость загрузки и вывода фотографий для каждого отеля (“Да/Нет”). При положительном ответе у пользователя запрашивается количество фотографий (максимум 10).
- Дата заезда и дата выезда.

При вводе команды __/bestdeal__ дополнительно запрашивается:
- Диапазон цен в $ за одну ночь.
- Максимальное расстояние до центра города.

Все запросы и их результаты сохраняются в базу данных.

После ввода команды __/history__ пользователю выводится история поиска отелей. Сама история содержит:
- Команду, которую вводил пользователь.
- Дату и время ввода команды.
- Параметры запроса.
- Отели, которые были найдены.

После ввода команды __/delete_history__ вся история поиска будет удалена из базы данных.