# Discord Whitelist Bot
1. [Настройка бота](#setting)
2. [Установка и запуск бота](#install-and-launch)
3. [Как получить токен от аккаунта](#token)
4. [Как записать сообщения](#messages)
5. [Как настроить телеграм бот](#telegram)
6. [Прочие настройки](#config)

<a name="setting"></a>
## Настройка бота
Вместе с ботом в архиве лежит папка config. Ее нужно распаковать в ту же папку что и бота
В папке находятся 5 файлов:

Обязательно нужно настроить:
- accounts.txt - здесь необходимо сохранить токены ваших аккаунтов (один токен - одна строчка)
- messages.txt - здесь нужно сохранить сообщения, которые бот будет отправлять. Мы предоставляем пример такого файла для 3ех аккаунтов. Если вы хотите сделать собственный файл, смотрите ниже, как правильно записать эти сообщения

Дополнительно можно настроить:
- config.yaml - основной файл конфигурации, здесь можно поменять различные настройки бота
- proxy.txt - файл для прокси, в нем должно быть столько же строчек сколько и аккаунтов. Одна строчка - один аккаунт, который и будет отправлять сообщения с этого прокси (аккаунт стоящий на 1ой строчке в accounts.txt будет использовать прокси стоящий на 1ой строчке в proxy.txt, 2ой аккаунт - 2ой прокси, и тд)
- telegram_settings.yaml - здесь указываются настройки телеграм бота, куда будут отправляться сообщения из бота. Смотрите ниже, как правильно его настроить.

<a name="install-and-launch"></a>
## Установка и запуск бота

1. Распакуйте zip архив в удобную вам папку. Зайдите в папку bot
2. Проверьте что в папке config присутствуют все файлы указанные ниже (proxy.txt только если вы используете прокси, telegram_settings.txt только если вы используете телеграм бота) 
3. Поместите токены аккаунтов в accounts.txt через строчку
3. Запустите файл bot (bot.exe на Windows)

<a name="token"></a>
## Как получить токен для аккаунта

1. Зайдите в любой чат в дискорде.
2. Откройте консоль разработчика. Для этого либо нажмите F12, либо нажмите правой кнопкой мыши по странице и выберете 'Посмотреть код' ('Inspect' на английском).
3. Перейдите во вкладку 'Сеть' ('Network')
4. Напишите и отправьте любое сообщение в чат дискорд
5. Нажмите на 'messages' в левой колонке
6. В правой колонке пролистайте до секции "Заголовки запросов". Найдите строчку начинающуюся с 'authorization: '
7. Скопируйте страшную последовательность символов после 'authorization: ' и вставьте в accounts.txt. 

Сделайте эту последовательность шагов для каждого аккаунта, который вы хотите использовать. Записывайте токены через строчку.

<a name="messages"></a>
## Как записать сообщения (messages.txt)
Бот может посылать сообщения с неограниченного количества аккаунтов. 
- Если вы используете только один аккаунт, просто запшите сообщения по строчкам. Одно сообщение - одна строчка.
- Если вы используете два или больше аккаунтов, необходимо писать в начале строчки какой аккаунт пишет сообщение. Пример:

Первый аккаунт (из accounts.txt) пишет сообщение:
1:Привет
Второй аккаунт пишет сообщение:
2:Как дела?

Одно сообщение - одна строчка

- Аккаунт может ответить на последнее сообщение другого (сделать реплай). Для этого после указания аккаунта, который пишет сейчас, нужно указать кому он отвечает. Пример:

Первый аккаунт пишет сообщение:
1:Всем привет
Второй аккаунт отвечает:
2:1:Привет! Как дела?

! Аккаунт отвечает только на ПОСЛЕДНЕЕ сообщение упомянутого аккаунта. Если упомянутый акккаунт еще ничего не писал, упомянут он быть не может.
! Упоминания через @ в данный момент не работают и будут выглядеть как обычный текст

<a name="telegram"></a>
## Как настроить телеграм бот (telegram_settings.yaml)

Если вы знаете как создать бота в телеграме, можете создать его и пропустить шаги 1 и 2
1. Для начала нужно создать телеграм бот. Для этого зайдите в телеграм и через поиск найдите бота @BotFather и начните диалог.
2. Напишите /newbot. Придумайте название и отправьте его боту. После этого придумайте юзернейм на английском, он должен состоять из одного слова и заканчиваться на 'bot'
3. Бот отправит вам ссылку на бота и токен похожий на `1234567890:Abcde_fghq00e-aBCD2EFGD2EFGHkQ23a3h`. Скопируйте его в файл telegram_settings.yaml в строку `telegram_token` (`telegram_token: 1234567890:Abcde_fghq00e-aBCD2EFGD2EFGHkQ23a3`)
4. Зайдите обратно в @BotFather и перейдите на своего бота через ссылку. Начните диалог
5. Через поиск найдите бота @RawDataBot. Начните с ним диалог
6. Он пришлет страшное сообщение с кучей данных. Нас интересует то что стоит рядом с "id". Там будет какое то (скорее всего восьмизначное, как и количество нулей на вашем аккаунте после продажи вл) число. Скопируйте его и вставьте в telegram_settings.yaml в строку chat_id (`chat_id:12345678`)
7. В config.yaml найдите строчку `log_tg: False` и поменяйте False на True

Все готово! Теперь бот будет пересылать вам все, что выводит в консоли. Кстати в config.yaml можно настроить, что именно бот будет выводить.

<a name="config"></a>
## Прочие настройки (config.yaml)

В config.yaml можно также поменять различные другие настройки. Тут можно настроить задержки при отправке, скорость печати сообщений и др. Все настройки прокоменнтированы, можете смело заглянуть и поменять что вам надо