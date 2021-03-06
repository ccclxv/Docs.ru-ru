---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: Кэширование данных с помощью ObjectDataSource (VB) | Документы Microsoft
author: rick-anderson
description: Кэширование может означать разницу между медленных и быстрый веб-приложения. Этот учебник является первым четырем, просмотрите подробные кэширование в ASP.NET...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: a79ed980e28e2c20a73fa4193f8c0970c9dbdef8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2018
---
<a name="caching-data-with-the-objectdatasource-vb"></a>Кэширование данных с помощью ObjectDataSource (Visual Basic)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Загрузить пример приложения](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe) или [скачать PDF](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> Кэширование может означать разницу между медленных и быстрый веб-приложения. Этот учебник является первым четырем, просмотрите подробные кэширования в ASP.NET. Сведения и основные понятия кэширования кэшировать уровень представления через элемент управления ObjectDataSource.


## <a name="introduction"></a>Вступление

В вычислительной технике *кэширование* — это процесс получения или данные затратна получить и сохранить его копию в расположении, проще и быстрее доступа. Для приложений, управляемых данными больших и сложных запросов обычно потребляют большую часть времени выполнения приложения s. Часто такие s производительность приложения, затем можно повысить путем сохранения результатов запросов дорогих базы данных в памяти приложения s.

ASP.NET 2.0 предлагает широкий набор параметров кэширования. Всю веб-страницу или пользовательский элемент управления отображался разметки могут кэшироваться через *кэширование вывода*. Элементы управления ObjectDataSource и SqlDataSource предоставляют возможности кэширования также, тем самым позволяя данных кэшируются на уровне элемента управления. И ASP.NET s *кэш данных* предоставляет широкие возможности API кэширования, который позволяет разработчикам программным образом объектов кэша. В этот учебник и трех последующих, мы изучим, с помощью ObjectDataSource s кэширования функций, а также в кэш данных. Также мы изучим, как кэшировать данные уровня приложения во время запуска, а также для хранения кэшированных данных в новую при помощи зависимости кэша SQL. Эти учебники не исследовать кэширование вывода. Подробное рассмотрение кэширование вывода в разделе [кэширование вывода в ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx).

Кэширование могут применяться в любом месте в архитектуре, от уровня доступа к данным вверх через уровень представления данных. В этом учебнике мы рассмотрим применение кэширования на уровень представления через элемент управления ObjectDataSource. В следующем уроке, который будет рассматриваться кэширование данных на уровне бизнес-логики.

## <a name="key-caching-concepts"></a>Основные понятия кэширование ключей

Кэширование s приложения может значительно повысить общую производительность и масштабируемость, получение данных затратна, для создания и хранения его копию в расположении, которое может осуществляться более эффективно. Так как кэш-память содержит копию фактического базовых данных, он может устареть, или *устаревших*при изменении базовых данных. Для решения этой разработчик страницы можно указать критерии, по которым будут элемента кэша *вытеснение* из кэша, используя:

- **Временном критерии** элемента могут быть добавлены в кэш абсолютный или скользящий длительности. Например разработчик может указывать длительность, скажем, 60 секунд. Абсолютный длительностью 60 секунд, после его добавления в кэш, независимо от того, насколько часто осуществлялся вытеснение кэшированного элемента. Скользящий длительностью 60 секунд после последнего доступа вытеснение кэшированного элемента.
- **Критерии зависимостей** зависимости могут быть связаны с элементом при добавлении в кэше. При изменении элемента s зависимости он удаляется из кэша. Зависимость может быть файл, сочетание двух или другого элемента кэша. ASP.NET 2.0 также поддерживает зависимости кэша SQL, которые позволяют разработчикам добавить элемент в кэш и их удаления при изменении основной базы данных. Изучим зависимости кэша SQL в следующем подразделе [с помощью кэш-зависимости SQL](using-sql-cache-dependencies-vb.md) учебника.

Независимо от того, заданным критериям вытеснения элемента в кэше может быть *очистки для* перед выполнены условия на основе времени или на основе зависимостей. Если кэш достигнут максимальный объем, необходимо удалить существующие элементы, перед добавлением новых. Следовательно при программно работа с кэшированными данными s важных всегда предполагается, кэшированных данных может отсутствовать. Мы рассмотрим шаблон, используемый при доступе к данным из кэша программными средствами в далее в этом руководстве *кэширование данных в архитектуре*.

Кэширование предоставляет экономичный способ для сжатие дополнительные производительности из приложения. Как [Smith Стивен](http://aspadvice.com/blogs/ssmith/) articulates в его статье [кэширование ASP.NET: методики и рекомендации](https://msdn.microsoft.com/library/aa478965.aspx):

Кэширование может быть хороший способ получения хорошей производительности достаточно не требует много времени и анализа. Требует больших затрат памяти, поэтому, если вы можете получить производительности, путем кэширования выходных данных для 30 секунд, вместо того чтобы тратить дня или недели, пытаясь оптимизировать свой код или базы данных, выполните решение для кэширования (при условии, что 30 - старых секунду данных — ОК) и перейти. Со временем плохое проектирование будут, вероятно, догонит, разумеется, следует попытаться правильно проектировать свои приложения. Но если необходимо получить хорошее достаточно производительности сегодня, кэширование может быть отличным [подход] покупки время рефакторинг впоследствии при наличии времени для этого приложения.

Кэширование может обеспечить повышение производительности достаточное, она не применимо во всех ситуациях, например с приложениями, которые используют в режиме реального времени, часто обновлять данные или когда неприемлема даже вскоре жили устаревшие данные. Однако для большинства приложений, следует использовать кэширование. Дополнительные сведения о кэшировании в ASP.NET 2.0 см. в разделе [кэширования для повышения производительности](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) раздел [ASP.NET 2.0 статьи краткого руководства](https://quickstarts.asp.net/QuickStartv20/aspnet/).

## <a name="step-1-creating-the-caching-web-pages"></a>Шаг 1: Создание кэширования веб-страницы

Прежде чем начать наши исследования функции кэширования s ObjectDataSource, позволяют сначала занять некоторое время для создания страниц ASP.NET в данном проекте веб-сайта, он понадобится для этого учебника и трех последующих s. Начните с добавления в новую папку с именем `Caching`. Добавьте следующие страницы ASP.NET в этой папке, убедитесь, что связать каждую страницу с `Site.master` главной страницы:

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`


![Добавление страниц ASP.NET для учебников, связанные с кэшированием](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**Рис. 1**: Добавление страницы ASP.NET для учебников, связанные с кэшированием


Как и в других папках, `Default.aspx` в `Caching` папки будут перечислены учебники в своем разделе. Помните, что `SectionLevelTutorialListing.ascx` пользовательский элемент управления предоставляет следующие функциональные возможности. Таким образом, добавьте этот пользовательский элемент управления для `Default.aspx` , перетащив его из обозревателя решений на странице s представление конструктора.


[![Рисунок 2: Добавьте Default.aspx SectionLevelTutorialListing.ascx пользовательского элемента управления](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**На рисунке 2**: рис. 2: добавление `SectionLevelTutorialListing.ascx` пользовательского элемента управления на `Default.aspx` ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image4.png))


И, наконец, добавьте эти страницы как операции для `Web.sitemap` файла. В частности, добавьте следующую разметку после работы с двоичными данными `<siteMapNode>`:


[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

После обновления `Web.sitemap`, занять некоторое время для просмотра учебников веб-сайт с помощью браузера. В левом меню теперь включает элементы для кэширования учебники.


![Карта сайта теперь содержит записи для кэширования учебники](caching-data-with-the-objectdatasource-vb/_static/image5.png)

**Рис. 3**: карта сайта теперь содержит записи для кэширования учебники


## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>Шаг 2: Отображение списка продуктов в веб-страницы

Этот учебник посвящена тому, как использовать элемент управления ObjectDataSource управления s встроенных функций кэширования. Прежде чем можно рассмотреть эти функции, однако необходимо сначала страницы для работы с. S позволяют создать веб-страницы, использующий GridView для просмотра сведений о продукции извлекаемые ObjectDataSource из `ProductsBLL` класса.

Сначала откройте `ObjectDataSource.aspx` страницы в `Caching` папки. Перетащите элемент управления GridView с панели элементов в конструктор, задайте его `ID` свойства `Products`и в его смарт-тег, выберите, чтобы привязать его к новый элемент управления ObjectDataSource `ProductsDataSource`. Настройка ObjectDataSource для работы с `ProductsBLL` класса.


[![Настройка ObjectDataSource с помощью класса ProductsBLL](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**Рис. 4**: Настройка ObjectDataSource для использования `ProductsBLL` класса ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image8.png))


Для этой страницы позволяют создавать изменяемого элемента управления GridView, чтобы мы можно проверить, что происходит при изменении данных, кэшированных в ObjectDataSource через интерфейс s GridView s. Оставьте раскрывающегося списка на вкладке ВЫБЕРИТЕ значение по умолчанию `GetProducts()`, но изменить элемент, выбранный на вкладке «обновление» для `UpdateProduct` перегрузку, которая принимает `productName`, `unitPrice`, и `productID` качестве входных параметров.


[![Установить обновления вкладку s раскрывающемся список перегрузке соответствующего UpdateProduct](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**Рис. 5**: присвоено s вкладку обновление раскрывающегося списка приемлемым `UpdateProduct` перегрузки ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image11.png))


Наконец раскрывающиеся списки на вкладках INSERT и DELETE (нет) и нажмите кнопку Готово. После завершения работы мастера настройки источника данных, Visual Studio устанавливает ObjectDataSource s `OldValuesParameterFormatString` свойства `original_{0}`. Как было сказано в [Обзор Вставка, обновление и удаление данных](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) учебник, это свойство должно быть удалены из декларативного синтаксиса или снова установить значение по умолчанию `{0}`, в порядке для наших рабочего процесса обновления Продолжить без ошибок.

Кроме того после завершения работы мастера Visual Studio добавляет поле к GridView для каждого из полей данных продукта. Удалите все, кроме `ProductName`, `CategoryName`, и `UnitPrice` стояли. Затем обновите `HeaderText` свойства каждой из этих стояли с продуктом, категории и цену, соответственно. Поскольку `ProductName` поле является обязательным, преобразовать в TemplateField BoundField и добавить RequiredFieldValidator для `EditItemTemplate`. Аналогичным образом преобразовать `UnitPrice` BoundField в TemplateField и добавьте CompareValidator для убедитесь, что введенное пользователем значение валюты допустимое значение s больше или равно нулю. Помимо этих изменений вы можете выполнить все изменения внешнего вида, например правым `UnitPrice` значения или указание форматирования для `UnitPrice` его интерфейсы только для чтения и редактирования текста.

Изменить GridView, установив флажок Разрешить изменение GridView s смарт-тега. Кроме того, установите флажки включить разбиение на страницы и включить сортировку.

> [!NOTE]
> Необходимо ознакомиться с Настройка интерфейса редактирования GridView s? В этом случае обращаться к [Настройка интерфейса изменения данных](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) учебника.


[![Включите поддержку GridView для редактирования, сортировку и разбиение по страницам](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**Рис. 6**: Включение поддержки GridView для редактирования, сортировки и разбиения на страницы ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image14.png))


После внесения этих изменений GridView, GridView и ObjectDataSource s должна выглядеть следующим образом:


[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

Как показано на рис. 7, изменяемого элемента управления GridView перечислены имя, категорию и цену всех продуктов в базе данных. Теперь пора проверить функциональные возможности сортировки страницы s результаты страницы по ним и измените запись.


[![Каждый продукт s имя, категорию и цена указана в Sortable, Pageable, изменяемого элемента управления GridView](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**Рис. 7**: s каждый продукт имя, категорию и цена указана в Sortable, Pageable, изменяемого элемента управления GridView ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image17.png))


## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>Шаг 3: Изучение при ObjectDataSource является запрос данных

`Products` GridView извлекает свои данные для отображения путем вызова `Select` метод `ProductsDataSource` ObjectDataSource. Этот элемент управления ObjectDataSource создает экземпляр s уровня бизнес-логики `ProductsBLL` класса и вызывает его `GetProducts()` метод, который в свою очередь вызывает s уровня доступа к данным `ProductsTableAdapter` s `GetProducts()` метод. Метод DAL подключается к базе данных Northwind и выдает настроенного `SELECT` запроса. Эти данные затем возвращается к DAL, который упаковывает в `NorthwindDataTable`. Для МЕТОДА, который возвращает его в элемент управления ObjectDataSource, которая возвращает его в GridView, возвращается объект DataTable. Затем создается в GridView `GridViewRow` объекта для каждого `DataRow` в DataTable и каждый `GridViewRow` со временем к просмотру в HTML, который возвращается клиенту и отображается в браузере посетителя s.

Эту последовательность событий происходит каждый раз необходимо привязать к его базовым данным GridView. Это происходит при первом посещении страницы, при переходе от одной страницы данных в другую, при сортировке в GridView, или при изменении данных s GridView по его встроенным, изменение или удаление интерфейсов. Если состояние представления GridView s отключена, при каждой обратной передаче также будет привязывается GridView. GridView можно также явно привязывается к его данным путем вызова его `DataBind()` метод.

Чтобы полностью оценить частоту, с которой данные извлекаются из базы данных, позволяют выводится сообщение о данных, который повторно получаются s. Добавить веб-управления Label над элементом управления GridView с именем `ODSEvents`. Очистить его `Text` и установите его `EnableViewState` свойства `False`. Под метки, добавьте кнопку веб-элемент управления и задайте его `Text` свойство обратной передачи.


[![Добавить метки и кнопку на страницу над элементом управления GridView](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**Рис. 8**: Добавление страницы выше GridView метка и кнопка ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image20.png))


При выполнении рабочего процесса доступа к данным, ObjectDataSource s `Selecting` событие срабатывает перед созданием базового объекта и его настроенный метод вызывается. Создайте обработчик событий для этого события и добавьте следующий код:


[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

Каждый раз, когда элемент управления ObjectDataSource делает запрос к архитектуре для данных, метки будут отображаться возникает событие выделение текста.

Посетите эту страницу в браузере. При первом посещении страницы, инициированные события Selecting текст отображается. Нажмите кнопку обратной передачи и обратите внимание, что текст исчезает (предполагая, что GridView s `EnableViewState` свойству `True`, значение по умолчанию). Это происходит потому, при обратной передаче GridView перестраивается из состояния представления и поэтому t включать в элемент управления ObjectDataSource для своих данных. Сортировка, разбиение по страницам и изменение данных, однако вызывает GridView для повторной привязки к источнику данных, и поэтому при выборе событие отобразится текст.


[![Всякий раз, когда GridView, привязывается к источнику данных, сработавшего события Selecting отображается](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**Рис. 9**: каждый раз, когда GridView повторно привязываются к источнику данных, будут выведены сработавшего события Selecting ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image23.png))


[![Нажав кнопку вызывает обратную передачу GridView перестраиваются заново из состояния представления](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**Рис. 10**: нажатие кнопки обратной передачи GridView перестраиваются заново из состояния представления ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image26.png))


Может показаться лишних затрат для получения данных базы данных каждый раз, страниц или отсортированных данных. В конце концов так как мы re разбиении по умолчанию, элемент управления ObjectDataSource извлеченные все записи при отображении на первой странице. Даже если GridView не предоставляет сортировку и разбиение по страницам поддержки, необходимо получить данные из базы данных каждый раз, когда сначала просмотре любым пользователем (и на каждой обратной передачи, если состояние просмотра отключено). Но если GridView отображаются те же данные для всех пользователей, эти запросы дополнительные базы данных избыточной. Почему бы не кэшировать результаты, возвращенные `GetProducts()` метод и привязка GridView теми кэшированные результаты?

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>Шаг 4: Кэширование данных с помощью элемент управления ObjectDataSource

Просто задать несколько свойств, можно настроить элемент управления ObjectDataSource автоматически кэшировать его полученных данных в кэше данных ASP.NET. В следующем списке перечислены относящиеся к кэшированию свойства ObjectDataSource:

- [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) должно быть присвоено `True` для включения кэширования. Значение по умолчанию — `False`.
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) время в секундах, кэширование данных. Значение по умолчанию — 0. ObjectDataSource будет кэшировать данные, только если `EnableCaching` — `True` и `CacheDuration` задано значение больше нуля.
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) может быть присвоено `Absolute` или `Sliding`. Если `Absolute`, ObjectDataSource кэширует его полученные данные для `CacheDuration` секунды; Если `Sliding`, истечения срока действия данных только после того, что не осуществлялся для `CacheDuration` секунд. Значение по умолчанию — `Absolute`.
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) это свойство используется для связывания записей кэша ObjectDataSource s с существующие зависимости в кэше. Записи данных s ObjectDataSource может быть преждевременно извлекается из кэша, пометив его связанными `CacheKeyDependency`. Это свойство чаще всего используется для связи с кэшем s ObjectDataSource зависимость кэша SQL, раздел будет рассматриваться в будущем [с помощью кэш-зависимости SQL](using-sql-cache-dependencies-vb.md) учебника.

Позволяет настроить s `ProductsDataSource` ObjectDataSource кэширования данных на 30 секунд на абсолютной шкале. Набор ObjectDataSource s `EnableCaching` свойства `True` и его `CacheDuration` свойство до 30. Оставить `CacheExpirationPolicy` свойства, значение по умолчанию `Absolute`.


[![Настройка ObjectDataSource кэширования данных на 30 секунд](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**Рис. 11**: Настройка ObjectDataSource кэширования данных на 30 секунд ([Просмотр полноразмерное изображение](caching-data-with-the-objectdatasource-vb/_static/image29.png))


Сохранить изменения и возвратиться к этой странице в браузере. При выборе сработавшего события будет отображаться текст при первом посещении страницы, как изначально данных не находится в кэше. Но при этом не последующих обратных передачах запустить, нажав кнопку обратной передачи, сортировка, разбиение по страницам или кнопки редактирования или "Отмена" *не* текста, инициированные повторно отобразить события Selecting. Это вызвано `Selecting` событие возникает, только когда элемент управления ObjectDataSource получает данные из базового объекта; `Selecting` событий не выполняется, если данные извлекаются из кэша данных.

Через 30 секунд данных будет удалена из кэша. Данные также будет удалена из кэша, если элемент управления ObjectDataSource s `Insert`, `Update`, или `Delete` методы вызываются. В результате после 30 секунд или обновления была нажата кнопка, сортировка, разбиение по страницам, или кнопки редактирования или "Отмена" приведет к ObjectDataSource для получения данных из базового объекта, отображение события Selecting возникает текст при `Selecting` вызывается событие. Эти возвращаемые результаты помещаются обратно в кэш данных.

> [!NOTE]
> Если вы видите текст сработавшего события Selecting часто, даже в том случае, если предполагается, что элемент управления ObjectDataSource и при работе с кэшированными данными возможно из-за нехватки памяти. Если не хватает памяти, данные, добавленные в кэш, ObjectDataSource может были очистки для. Если t ObjectDataSource указаны правильно кэшировать данные или только кэш данных время от времени, закройте часть приложений для освобождения памяти и повторите попытку.


Рис. 12 показан ObjectDataSource s, кэширование рабочего процесса. При возникновении события Selecting текст отображается на экране, поскольку данные не находился в кэше и должны были быть получены из базового объекта. При отсутствии этот текст, однако он s, так как данные были доступны из кэша. Когда данные возвращаются из кэша существует s не вызов базового объекта и, следовательно, без запроса базы данных выполнена.


![ObjectDataSource сохраняет и извлекает данные из кэша данных](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**Рис. 12**: ObjectDataSource хранит и извлекает данные из кэша данных


Каждое приложение ASP.NET имеет свой собственный кэш данных экземпляра, s, общими для всех страниц и посетителей. Это означает, что данные, хранящиеся в кэше данных ObjectDataSource аналогично совместно всех пользователей, посетите веб-сайт. Чтобы проверить это, откройте `ObjectDataSource.aspx` страницы в браузере. При первом просмотре страницы, будет отображаться текст сработавшего события Selecting (предполагается, что данные, добавленные в кэш с предыдущих тестов к этому моменту исключен). Откройте второй экземпляр браузера и скопируйте и вставьте URL-адрес из первого экземпляра браузера на второй. Во втором экземпляре браузера сработавшего события Selecting текст не отображается, поскольку он s, используя те же кэшированные данные, что и первый.

При вставке его полученных данных в кэше, ObjectDataSource использует значения ключа кэша, содержащего: `CacheDuration` и `CacheExpirationPolicy` значения свойств; тип базовой бизнес-объекта, используемого ObjectDataSource, который указывается через [ `TypeName` свойство](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) (`ProductsBLL`, в этом примере); значение `SelectMethod` свойства, а также имени и значения параметров в `SelectParameters` коллекции; и значения его `StartRowIndex`и `MaximumRows` свойств, которые используются при реализации [пользовательское разбиение по страницам](../paging-and-sorting/paging-and-sorting-report-data-vb.md).

Значение ключа кэша, дополнительно как сочетание этих свойств гарантирует уникальных записей кэша, как изменить эти значения. Например, в предыдущих учебниках мы рассмотрели применение хранить `ProductsBLL` класса s `GetProductsByCategoryID(categoryID)`, возвращающий всех продуктов для определенной категории. Один пользователь можете прийти к Напитки страницы и представления, который имеет `CategoryID` 1. Если элемент управления ObjectDataSource кэшированные результаты без учета `SelectParameters` значений, когда другого пользователя на страницу для просмотра приправы при Напитки продукты были в кэше, d увидят кэшированный напитков продуктов, а не приправы. Изменив ключ кэша для этих свойств, которые включают значения `SelectParameters`, ObjectDataSource обслуживает отдельную запись кэша для напитков и приправы.

## <a name="stale-data-concerns"></a>Устаревшие данные проблемы

ObjectDataSource автоматически исключает его элементы из кэша, если один из его `Insert`, `Update`, или `Delete` методы вызваны. Это помогает защититься от устаревшие данные при очистке записей кэша, при изменении данных на странице. Тем не менее существует возможность ObjectDataSource использование кэширования, чтобы по-прежнему отображаться устаревшие данные. В самом простом случае она может быть вызвано данные изменять непосредственно в базе данных. Может быть администратором базы данных только что была скрипт, который изменяет некоторые записи в базе данных.

Этот сценарий также может развертывать более тонкая способом. Хотя элемент управления ObjectDataSource исключает его элементы из кэша при вызове одного из его методы изменения данных, удаленными кэшированного элементами предназначены для ObjectDataSource s определенного сочетания значений свойств (`CacheDuration`, `TypeName`, `SelectMethod`, и т. д.). Если у вас есть два ObjectDataSources, которые используют разные `SelectMethods` или `SelectParameters`, но по-прежнему можете обновить те же данные, то один ObjectDataSource может обновить строку и сделать недействительным записей кэша, но соответствующая строка для второй элемент управления ObjectDataSource по-прежнему будет предоставляться из кэша. Я рекомендую для создания страниц, поведение которых эта функция. Создание страницы, которая отображает изменяемого элемента управления GridView, который извлекает данные из ObjectDataSource, который использует кэширование и настроен для получения данных из `ProductsBLL` класса s `GetProducts()` метод. Добавьте еще один редактируемые GridView и ObjectDataSource на этой странице (или другое), но для этого второй ObjectDataSource имеют его использовать `GetProductsByCategoryID(categoryID)` метода. Поскольку два ObjectDataSources `SelectMethod` свойства отличаются, они ll каждый имеет свои собственные кэшированные значения. При редактировании продуктов в одной таблице, при очередном привязка данных к другой таблице (путем разбиения на страницы, сортировку и так далее), он по-прежнему использовать старый, кэшированные данные и не отражают изменения, внесенные в других сетке.

Иными словами только используйте кэше на основе времени, если вы готовы потенциально устаревшие данные и использовать более короткие кэше для сценариев, где важна актуальность данных. Если устаревшие данные неприемлем, отказ от кэширования или использовать кэш-зависимости SQL (предполагается, что базы данных во время кэширования). В будущем учебнике мы изучим зависимости кэша SQL.

## <a name="summary"></a>Сводка

В этом учебнике мы рассмотрели ObjectDataSource s встроенные возможности кэширования. Просто задать несколько свойств, можно настроить элемент управления ObjectDataSource кэшировать результаты, возвращаемые из указанного `SelectMethod` в кэш данных ASP.NET. `CacheDuration` И `CacheExpirationPolicy` свойства указывают длительность кэширования элемента, так и абсолютный или скользящий срок действия. `CacheKeyDependency` Связывает все записи кэша ObjectDataSource s с существующие зависимости в кэше. Это позволяет исключить из кэша записей s ObjectDataSource перед достигается на основе времени окончания срока действия и обычно используется с зависимости кэша SQL.

Поскольку элемент управления ObjectDataSource просто кэширует его значения в кэше данных, мы удалось реплицировать ObjectDataSource s встроенных функциональных возможностей программными средствами. Он t имеет смысла для этого на уровне представления, так как ObjectDataSource предлагает эта функциональность без дополнительной настройки, но мы реализовали возможности кэширования, в отдельном слое архитектуры. Чтобы сделать это, нам нужно будет повторить ту же логику, используется элемент управления ObjectDataSource. Мы изучим, как программным образом работать с использованием данных кэша в архитектуре в обучении Далее.

Программирование довольны!

## <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения по темам, рассматриваемые в этом учебнике см. в следующих ресурсах:

- [Кэширование ASP.NET: Методики и рекомендации](https://msdn.microsoft.com/library/aa478965.aspx)
- [Кэширования руководство по архитектуре для приложений .NET Framework](https://msdn.microsoft.com/library/ee817645.aspx)
- [Кэширование вывода в ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>Об авторе

[Скотт Митчелл](http://www.4guysfromrolla.com/ScottMitchell.shtml), автор семи ASP/ASP.NET и основателя из [4GuysFromRolla.com](http://www.4guysfromrolla.com), работает с веб-технологиями Майкрософт с 1998 года. Скотт — независимый консультант, trainer и записи. Его последняя книга — [ *диспетчерами учат самостоятельно ASP.NET 2.0 в течение 24 часов*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Он может быть достигнута по [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) или через его блог, который можно найти в [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Благодарности

Этот учебник ряд прошел проверку многие полезные рецензентов. Основной рецензент этого учебника было Мерфи Тереза д. Объясняются моих последующих статей для MSDN? Если Да, напишите мне по [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Назад](using-sql-cache-dependencies-cs.md)
> [Вперед](caching-data-in-the-architecture-vb.md)
