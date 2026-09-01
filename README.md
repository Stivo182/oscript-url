# url

`url` — библиотека OneScript для строгого разбора, преобразования и изменения URI и URL по
[RFC 3986](https://www.rfc-editor.org/rfc/rfc3986.html). Кодирование параметров формы соответствует алгоритму
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

## Разбор и разрешение URI

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

Адрес = Новый URL("https://example.com/users?page=1");

Адрес.ПараметрыЗапроса()
    .Установить("page", "2")
    .Добавить("include", "orders");

Сообщить(Адрес.ВСтроку());
```

Результат:

```text
https://example.com/users?page=2&include=orders
```

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
