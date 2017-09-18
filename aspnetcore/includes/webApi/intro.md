## <a name="overview"></a>Обзор

Ниже приводится созданный вами API:

|API | Описание    | Текст запроса    | Текст ответа   |
|--- | ---- | ---- | ---- |
|GET/api/todo  | Получение всех элементов задач | Нет | Массив элементов задач|
|GET/api/todo/{id}  | Получение объекта по идентификатору | Нет | Элемент задачи|
|POST/api/todo | Добавление нового элемента | Элемент задачи  | Элемент задачи |
|PUT/api/todo/{id} | Обновление существующего элемента &nbsp;  | Элемент задачи |  Нет |
|DELETE/api/todo/{id}  &nbsp;  &nbsp; | Удаление элемента &nbsp; &nbsp;  | Нет  | Нет|

<br>

На следующем рисунке показана общая структура приложения.

![Клиент, представленный прямоугольником слева, отправляет запрос и получает ответ от приложения (прямоугольник справа). В прямоугольнике приложения также расположены три прямоугольника, представляющих контроллер, модель и уровень доступа к данным. Запрос поступает на контроллер приложения, который выполняет операции чтения и записи между контроллером и уровнем доступа к данным. Модель сериализуется и возвращается клиенту в ответе.](../../tutorials/first-web-api/_static/architecture.png)

* В качестве клиента может выступать любой компонент, использующий API (мобильное приложение, браузер и т. д.). В рамках этого руководства клиент не создается. Для тестирования приложения мы будем использовать [Postman](https://www.getpostman.com/) или [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html).

* *Модель* — это объект, представляющий данные в приложении. В этом случае единственной моделью является задача. Модели представлены классами C#, которые также известны как **P****O****C**# **O**.

* *Контроллер* — это объект, который обрабатывает HTTP-запросы и создает HTTP-ответ. В этом приложении используется один контроллер.

* Для удобства в этом руководстве приложение не использует постоянную базу данных. В этом примере приложение сохраняет элементы задач в базе данных в памяти.