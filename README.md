# url

`url` — библиотека OneScript для строгого разбора, преобразования и изменения URI и URL с символами Unicode по
стандартам
[RFC 3986](https://www.rfc-editor.org/rfc/rfc3986.html) и
[RFC 3987](https://www.rfc-editor.org/rfc/rfc3987.html). Кодирование параметров формы соответствует алгоритму
[`application/x-www-form-urlencoded`](https://url.spec.whatwg.org/#application-x-www-form-urlencoded) из стандарта
WHATWG URL. Библиотека не выполняет DNS-запросов и других сетевых операций.

## Требования

- OneScript 2.0.0 или новее;
- OPM для установки зависимостей и сборки пакета.

## Установка

```powershell
opm install url
```

Подключение библиотеки:

```bsl
#Использовать url
```

Для проекта с `packagedef`:

```bsl
Описание.ЗависитОт("url");
```

## Разрешение URI

```bsl
#Использовать url

Ссылка = Новый URI("../users?page=2");
База = Новый URI("https://example.com/api/v1/");

Абсолютный = База.Разрешить(Ссылка);
Сообщить(Абсолютный.ВСтроку());
```

Результат:

```text
https://example.com/api/users?page=2
```

## Изменение URL

```bsl
#Использовать url

Адрес = Новый URL("https://example.com/users");

Адрес.ДобавитьСегментПути("team/a");
Адрес.ПараметрыЗапроса()
    .Установить("q", "hello world")
    .Добавить("include", "orders")
    .Добавить("include", "contacts");

Сообщить(Адрес.ВСтроку());
```

Результат:

```text
https://example.com/users/team%2Fa?q=hello+world&include=orders&include=contacts
```

## Адреса с символами Unicode

```bsl
#Использовать url

Адрес = Новый URL("https://пример.рф/путь?q=я");

Сообщить(Адрес.ВСтроку());
Сообщить(Адрес.КодированноеПредставление());
```

Результат:

```text
https://пример.рф/путь?q=я
https://%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80.%D1%80%D1%84/%D0%BF%D1%83%D1%82%D1%8C?q=%D1%8F
```

`ВСтроку()` возвращает адрес с сохранением символов Unicode. `КодированноеПредставление()` возвращает
ASCII-представление URI: символы Unicode преобразуются в UTF-8, после чего каждый полученный байт записывается
как `%HH`.

## Документация

- [Справочник API](docs/README.md)
- [URI](docs/URI.md)
- [URL](docs/URL.md)
- [ПараметрыURL](docs/ПараметрыURL.md)
- [КодированиеURL](docs/КодированиеURL.md)
- [КодыОшибокURL](docs/КодыОшибокURL.md)

## Разработка

Установить зависимости:

```powershell
opm install -l --dev
```

Запустить тесты:

```powershell
oneunit execute --recursive
```

Собрать пакет:

```powershell
opm build .
```
