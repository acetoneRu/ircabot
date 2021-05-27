# IRCaBot

ИркаБот - это непрожорливый логгер для IRC-чата: записывает историю, бережно сортируя сообщения по дате. Поддерживает функцию быстрого поиска слова или фразы, выводит статистику по каждой найденной дате. При поисковом запросе с датой отдает весь лог в ЛС запросившему пользователю.

Бот уважает права участников и дает возможность скрыть сообщения через специальную пометку. Точка в начале сообщения скрывает основной текст, но никнейм попадает в лог. Если в начале сообщения две точки, оно полностью игнорируется ботом и не появляется в логе.

Все запросы бот принимает только через общий чат, чтобы все могли видеть кто и что ищет. Обращения пользователей и свои ответы бот не записывает в историю, чтобы не захламлять лог.

## Конфигурация

Бот принимает путь до конфигурационного файла через передаваемый параметр: `ircabot /path/to/config.json`.

```json
{
    "socket":
    {
        "address":  "127.0.0.1", <-- адрес сервера
        "port":     "6667",      <-- порт сервера
        "channel":  "#ircabot",  <-- канал для подключения
        "nickname": "ircabot",   <-- никнейм бота
        "password": ""           <-- пароль от никнейма (для NickServ). Может быть пустым.
    },

	"handler":
	{
    	"help":     "'search' and 'test'.",  <-- ответ бота по умолчанию

        "logpath":  "/var/www/irc-log",      <-- директория хранения логов (должна существовать)
    	"admin":    "acetone",               <-- никнейм админа для сообщения об ошибках в ЛС
    	"success":  "success :)",            <-- сообщение об успехе
    	"error":    "error :(",              <-- сообщение об ошибке
    	"trylater": "try later.",            <-- сигнал о загруженности, "попробуйте позже"

    	"find":     "search",                <-- команда поиска, для русскоговорящих можеть быть "поиск"
    	"notfound": "not found.",            <-- сообщение о том, что поиск не дал результата
    	"findzero": "blahblah",              <-- инструкция по поиску при вызове команды без параметров
    	"links":    "http://si.te/log/",     <-- сообщение, выводимое после выдачи лога (веб-ссылка на лог)

    	"test":     "it's work!"
	}
}
```
Не копируйте конфиг отсюда, так как комментарии ломают файл. Практические примеры находятся в корне репозитория.

На месте `"test": "it's work!"` может быть неограниченное количество триггеров в формате ключ-значение. При получении сообщения, например: `ircabot, test` бот ответит `username, it's work!`. Подобная функция может использоваться для размещения объявлений, кошелька для доната и прочее, например, `"donate": "btc: xxxxxxxxxxxxxxxxxxxxxxx"`. Чтобы пользователи могли узнать о возможных функциях вызова, целесообразно упомянуть каждую в графе `help`.

Бот поддерживает изменение конфигурационного файла без перезапуска. Для применения изменений необходимо, чтобы пользователь, чей никнейм вписан в поле `admin`, написал в чате `ircabot, reload` (указывается актуальный никнейм бота).

Будьте внимательны: запятая в конце строки ключ-значение отсутствует только тогда, когда строка является последней. Если вы добавите некоторую кастомную строку, необходимо добавить запятую к предпоследней строке, а у последней строки запятой быть не должно.



Протестировать бота можно в [ILITA IRC, канал #acetonevideo](https://notabug.org/acetone/video/wiki/contacts#irc).



