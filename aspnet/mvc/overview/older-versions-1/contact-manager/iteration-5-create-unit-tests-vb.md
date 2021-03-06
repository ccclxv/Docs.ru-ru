---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 'Итерации #5 – Создание модульных тестов (Visual Basic) | Документы Microsoft'
author: microsoft
description: В пятой итерации сделан нашего приложения проще в обслуживании и изменить, добавив модульных тестов. Мы макета наших классов модели данных и создания модульных тестов для o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: fe59792a1e1a7950a318e7e893b3da12d53a8efa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2018
---
<a name="iteration-5--create-unit-tests-vb"></a>Итерации #5 – Создание модульных тестов (Visual Basic)
====================
по [Microsoft](https://github.com/microsoft)

[Загрузить исходный код](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> В пятой итерации сделан нашего приложения проще в обслуживании и изменить, добавив модульных тестов. Мы макета наших классов модели данных и создания модульных тестов для наших контроллеров и логику проверки.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Создание приложения ASP.NET MVC управления контактами (Visual Basic)

В этой серии учебники мы создаем всего приложения управления контактами от начала и завершения. Приложение диспетчера контактов позволяет хранить контактные данные - имена, номера телефонов и адресов электронной почты — список людей.

Мы постройте приложение в нескольких итерациях. С каждой итерацией постепенно мы улучшить приложение. Это несколько итераций предназначена для того, чтобы позволяют понять причину для каждого изменения.

- Итерации #1 - создать приложение. В первой итерации мы создадим диспетчера контактов простейшим способом невозможно. Добавлена поддержка для основных операций базы данных: создание, чтение, обновление и удаление (CRUD).

- Итерации #2 — сделать приложение поиска работы с низким приоритетом. В этой итерации нам улучшить внешний вид приложения, изменив значение по умолчанию главной страницы представления ASP.NET MVC и каскадные таблицы стилей.

- Итерации #3 - Добавление проверки формы. В третьем проходе добавим проверки базовой формы. Мы запретить отправки формы, не завершая обязательные поля. Мы также для проверки адреса электронной почты и номера телефонов.

- Итерации #4 - сделать приложение слабо. В этой третьей итерации мы воспользоваться преимуществами нескольких шаблонов разработки программного обеспечения, чтобы упростить обслуживание и изменить приложение диспетчера контактов. Например мы выполнили рефакторинг наше приложение, чтобы использовать шаблон репозитория и шаблон внедрения зависимостей.

- Итерации #5 - Создание модульных тестов. В пятой итерации сделан нашего приложения проще в обслуживании и изменить, добавив модульных тестов. Мы макета наших классов модели данных и создания модульных тестов для наших контроллеров и логику проверки.

- Итерация 6 # — с помощью управляемой тестами разработки. В итерации этого шестой мы добавим новые функциональные возможности наше приложение, сначала написание модульных тестов и писать код для модульных тестов. В этой итерации добавим групп контактов.

- Итерации #7. Добавление функциональности Ajax. В седьмой итерации мы повысить скорость реагирования и производительности приложения, добавляя поддержку Ajax.


## <a name="this-iteration"></a>Этой итерации

В предыдущих итерациях приложение диспетчера контактов мы оптимизировали приложению быть более слабо. Мы запятыми приложение в различных контроллера, службы и слои репозитория. Каждый уровень взаимодействует с нижнего уровня через интерфейсы.

Мы оптимизировали приложение, чтобы сделать удобнее для обслуживания и изменения приложения. Например если необходимо использовать новые технологии доступа к данным, мы можем просто изменить уровня репозитория не касаясь контроллер или уровня службы. Сделав диспетчера контактов слабо, мы хранять сделать приложение более устойчивым, чтобы изменить.

Но что произойдет, если необходимо добавить новый компонент в приложение диспетчера контактов? Или, что произойдет, если мы будем устранять ошибки? Жаль, что, но также и проверенные истину написание кода состоит в том всякий раз, когда touch кода создается риск возникновения новых ошибок.

Например один день нормально, менеджеру по работе с вас могут попросить добавить новый компонент диспетчера контактов. Можно добавить поддержку групп обратитесь к менеджеру. Она хочет, чтобы пользователи могли упорядочить свои контакты в группы, такие как друзья, Business и т. д.

Чтобы реализовать этот новый компонент, необходимо изменить все три уровня приложения диспетчера контактов. Необходимо добавить новые функции для контроллеров, уровень службы и хранилище. Сразу после запуска изменения кода, то существует риск критические функции, которые работали перед.

Рефакторинг нашего приложения в отдельные слои, как мы делали в предыдущих итерациях был хорошо. Было хорошо, так как он позволяет нам вносить изменения в все слои, не затрагивая остальной части приложения. Если вы хотите сделать удобнее для обслуживания и изменять код в составе слоя, необходимо создать модульные тесты для кода.

Используется модульного теста для тестирования отдельный блок кода. Эти блоки кода, меньше, чем слои всего приложения. Как правило чтобы убедиться, является ли конкретный метод в коде работает нужным образом, предполагается, что используется модульного теста. Например создается модульный тест для метода CreateContact(), предоставляемые классом ContactManagerService.

Модульные тесты на работу приложения, точно так же, как средство подстраховки. Каждый раз при изменении кода в приложении, можно запустить набор модульных тестов для проверки, разбивает ли изменять существующие функциональные возможности. Модульные тесты сделать код можно изменить. Модульные тесты сделать весь код в приложении более устойчивым к изменения.

В этой итерации мы добавим модульные тесты наше приложение диспетчера контактов. Таким образом, в следующей итерации, можно добавить контакт группы для нашего приложения, не беспокоясь о критических существующие функциональные возможности.

> [!NOTE] 
> 
> Существуют различные платформы, включая NUnit, xUnit.net и MbUnit модульного тестирования. В этом учебнике мы используем платформе модульного тестирования входящих в состав Visual Studio. Тем не менее можно легко использовать один из этих альтернативных платформ.


## <a name="what-gets-tested"></a>Что возвращает тестирования

В идеальном мире весь код должен покрывать модульных тестов. В идеальном мире бы идеальным подстраховки. Вы бы иметь возможность измените любую строку кода в приложении, чтобы узнать, выполнив модульные тесты ли это изменение было передано существующие функциональные возможности.

Тем не менее мы не хотите динамической t в идеальном мире. На практике при написании модульных тестов можно сосредоточиться на написание тестов для бизнес-логики (например, логика проверки). В частности вы *не* создавать модульные тесты для данных доступ к логику или логику представления.

Чтобы быть полезным, модульные тесты должны выполняться очень быстро. Можно легко накапливаются сотни (или даже тысячами) модульных тестов для приложения. Если модульные тесты занять много времени для запуска, а затем позволяет избежать их выполнении. Другими словами, длительные модульные тесты — бесполезными для ежедневных кодирования в целях.

По этой причине обычно вы не создаете модульных тестов для кода, взаимодействующая с базой данных. Запустив сотни модульных тестов для активной базы данных будет слишком медленно. Вместо этого макета базы данных и написать код, который взаимодействует с базой данных макетов (мы обсудим имитации базы данных ниже).

Аналогично обычно не написании модульных тестов для представления. Для проверки представления, необходимо запустить веб-сервера. Поскольку для настройки веб-сервера является относительно медленным процессом, создании модульных тестов для представления не рекомендуется.

Если представление содержит сложной логики следует рассмотреть, переместив логику в вспомогательные методы. Можно создавать модульные тесты для вспомогательных методов, которые выполняются не задействовав веб-сервера.

> [!NOTE] 
> 
> Во время записи тестов для логики доступа к данным или логики представления, рекомендуется не при написании модульных тестов, эти тесты может быть очень полезной при функционального построения или интеграции тестов.


> [!NOTE] 
> 
> ASP.NET MVC является обработчик представлений Web Forms. Хотя обработчик представлений Web Forms зависит от веб-сервера, может быть других обработчиков представлений.


## <a name="using-a-mock-object-framework"></a>С помощью макетов объекта платформы

При создании модульных тестов, почти всегда необходимо воспользоваться преимуществами платформы создания объекта. Это платформа для создания объекта позволяет создавать макеты и заглушки для классов в вашем приложении.

Например framework макета объекта можно использовать для создания имитационную версию класса репозитория. Таким образом, вы можно использовать класс макета репозитория вместо класса реальные репозитория в модульных тестах. С помощью макета репозитория дает возможность избежать выполнения кода базы данных при выполнении модульного теста.

Visual Studio включает платформу для создания объекта. Тем не менее имеются несколько инфраструктур макета объекта коммерческих с открытым исходным кодом для платформы .NET framework:

1. Заказа - эта платформа доступна в соответствии с открытой лицензией BSD. Вы можете загрузить заказа из [ https://code.google.com/p/moq/ ](https://code.google.com/p/moq/).
2. Фиктивных Rhino - эта платформа доступна в соответствии с открытой лицензией BSD. Вы можете загрузить Rhino фиктивных из [ http://ayende.com/projects/rhino-mocks.aspx ](http://ayende.com/projects/rhino-mocks.aspx).
3. Typemock изолятор - это коммерческих framework. Можно загрузить ознакомительную версию с [ http://www.typemock.com/ ](http://www.typemock.com/).

В этом учебнике решила использовать заказа. Однако можно легко использовать фиктивных Rhino или изолятор Typemock создание макетов объектов для приложения диспетчера контактов.

Прежде чем использовать заказа, необходимо выполнить следующие действия:

1. .
2. Прежде чем вы распаковать загрузки, убедитесь в том, щелкните правой кнопкой мыши файл и нажмите кнопку с многоточием **Unblock** (см. рис. 1).
3. Распакуйте загрузки.
4. Добавьте ссылку на сборку заказа в тестовый проект, выбрав параметр меню **проект, добавить ссылку на** Открытие **добавить ссылку** диалогового окна. Вкладка "Обзор" перейдите к папке, куда было распаковано заказа и выберите сборку Moq.dll. Нажмите кнопку **ОК** кнопку (см. рис. 2).


[![Разблокирование заказа](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**На рисунке 01**: разблокирование заказа ([Просмотр полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image2.png))


[![Ссылки после добавления заказа](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**На рисунке 02**: ссылки после добавления заказа ([Просмотр полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image4.png))


## <a name="creating-unit-tests-for-the-service-layer"></a>Создание модульных тестов для уровня службы

Разрешить s начните с создания набора модульных тестов для наших уровень службы s приложение диспетчера контактов. Мы будем использовать эти тесты, чтобы проверить логику проверки.

Создайте новую папку с именем моделей в проекте ContactManager.Tests. Затем щелкните правой кнопкой мыши папку модели и выберите **Add, новый тест**. **Добавление нового теста** появляется диалоговое окно, показанное на рис. 3. Выберите **модульного теста** шаблона и назовите новый тест ContactManagerServiceTest.vb. Нажмите кнопку **ОК** кнопку, чтобы добавить в проект тестов новый тест.

> [!NOTE] 
> 
> Как правило требуется структуру папки тестового проекта в соответствии со структурой папок проекта ASP.NET MVC. Например поместите контроллера тестов в папку Controllers, модель тестов в папку Models и так далее.


[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**На рисунке 03**: Models\ContactManagerServiceTest.cs ([Просмотр полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image6.png))


Изначально требуется протестировать метод CreateContact(), предоставляемые классом ContactManagerService. Мы создадим следующие пять тестов:

- CreateContact() - тесты, CreateContact() возвращает значение true, если допустимый контакт передается в метод.
- CreateContactRequiredFirstName() - тесты, что сообщение об ошибке добавляется в состояние модели после контакта с отсутствует имя первого передается методу CreateContact().
- CreateContactRequredLastName() - тесты, сообщение об ошибке добавляется в состояние модели после контакта с отсутствует Фамилия передается методу CreateContact().
- CreateContactInvalidPhone() - тесты, что сообщение об ошибке добавляется в состояние модели после контакта с недопустимыми номерами телефонов передается методу CreateContact().
- CreateContactInvalidEmail() - тесты, что сообщение об ошибке добавляется в состояние модели после контакта с недопустимый адрес электронной почты передается методу CreateContact()...

Первый тест проверяет, что допустимый контакт не будет создавать ошибку проверки. Остальные тесты проверки всех правил проверки.

В список 1 содержится код для этих тестов.

**Листинг 1 - Models\ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]


Так как мы используем контакт класс в список 1, необходимо добавить ссылку на платформу Entity Framework Microsoft нашей тестовый проект. Добавьте ссылку на сборку System.Data.Entity.


Листинг 1 содержит метод с именем Initialize(), отмеченный атрибутом [TestInitialize]. Этот метод автоматически вызывается перед выполнением каждого из модульных тестов (она называется 5 раз непосредственно перед каждым из модульных тестов). Метод Initialize() создает макет репозитория с следующую строку кода:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

Эта строка кода заказа используется для создания макета репозитория из интерфейса IContactManagerRepository. Вместо фактического EntityContactManagerRepository макета репозитория используется для предотвращения доступа к базе данных при запуске каждого модульного теста. Макета репозитория реализует методы интерфейса IContactManagerRepository, но фактически t Дон методы выполнять никаких действий.

> [!NOTE] 
> 
> При использовании framework заказа, является различие между \_mockRepository и \_mockRepository.Object. Первое относится к классу макетов (из IContactManagerRepository), который содержит методы для указания того, как будет вести себя макета репозитория. Последнее относится к фактическое макета репозитория, который реализует интерфейс IContactManagerRepository.


При создании экземпляра класса ContactManagerService, макета репозитория используется в метод Initialize(). Все отдельные модульные тесты используют этот экземпляр класса ContactManagerService.

Листинг 1 содержит пять методов, которые соответствуют каждому из модульных тестов. Каждый из этих методов является помеченной атрибутом [TestMethod]. При выполнении модульных тестов, вызывается любой метод, который имеет этот атрибут. Другими словами любой метод, отмеченный атрибутом [TestMethod] — это модульный тест.

Первый модульный тест, с именем CreateContact(), проверяет, что вызов CreateContact() возвращает значение true, если допустимый экземпляр класса контакта передается в метод. Тест создает экземпляр класса контакта, вызывает метод CreateContact() и проверяет, что CreateContact() возвращает значение true.

Остальные тесты убедитесь, что при вызове метода CreateContact() Недопустимый контакт затем метод возвращает значение false, и сообщение об ошибке проверки ожидаемого добавляется состояние модели. Например тест CreateContactRequiredFirstName() создает экземпляр класса контакта с пустой строки для свойства «имя». Затем метод CreateContact() вызывается с недопустимый контакт. Наконец тест проверяет, что CreateContact() возвращает значение false и состояния модели содержит сообщение об ошибке проверки ожидаемого «требуется имя.»

Можно выполнять модульные тесты в список 1, выбрав параметр меню **теста запустите все тесты в решении (CTRL + R, A)**. Результаты тестов отображаются в окне результатов теста (см. рис. 4).


[![Результаты теста](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**На рисунке 04**: результаты теста ([Просмотр полноразмерное изображение](iteration-5-create-unit-tests-vb/_static/image8.png))


## <a name="creating-unit-tests-for-controllers"></a>Создание модульных тестов для контроллеров

Приложение ASP.NET MVC управления потоком взаимодействия с пользователем. При тестировании контроллер, необходимо проверить ли контроллер возвращает правой действие результат и представления данных. Также может потребоваться проверить, является ли контроллер взаимодействует с классами модели так, как ожидалось.

Например список 2 содержит два модульных теста для контроллера контакт Create() метод. Первый модульный тест проверяет, что при допустимый контакт передается методу Create(), а затем метод Create() перенаправляет действие индекса. Другими словами Если передать допустимый контакт, Create() метод должен вернуть RedirectToRouteResult, который представляет действие индекса.

Мы не хотите t требуется протестировать ContactManager уровень службы, когда мы тестируем слоя контроллера. Таким образом мы макета уровень службы на следующий код в методе Initialize:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

В модульном тесте CreateValidContact() мы макета поведение вызывающих уровень службы CreateContact() метод следующий код:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

Эта строка кода приводит к макетов служба ContactManager возвращают значение true при вызове его метода CreateContact(). Путем имитации уровень службы, можно проверить поведение нашей контроллера без необходимости выполнения любого кода в уровне службы.

Второй модульный тест проверяет, что действие Create() возвращает представления создания, если методу передается недопустимый контакт. Мы возникновение уровень службы CreateContact() метода, возвращающего значение false с следующую строку кода:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

Если метод Create() работает как ожидается, затем он должен возвращать представления создания при уровень службы возвращает значение false. В этом случае контроллер может отобразить сообщения об ошибках проверки в режиме создания, и у пользователя есть исправить, недопустимые свойства контакта.


Если вы планируете создать модульные тесты для контроллеров необходимо возвращать имена явное представление из действий контроллера. Например не получить следующим образом:

Возвращает View()

Вместо этого получить следующим образом:

Возвращает View("Create")

При отсутствии явной при возврате представление ViewResult.ViewName свойство возвращает пустую строку.


**Листинг 2 - Controllers\ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>Сводка

В этой итерации мы создали модульных тестов для нашего приложения диспетчера контактов. Мы эти модульные тесты можно выполнять в любое время, чтобы убедиться, что приложение по-прежнему работает так, которую мы предполагаем. Модульные тесты действуют как средство подстраховки, если для приложения позволяет нам безопасно изменить нашего приложения в будущем.

Мы создали два набора модульных тестов. Во-первых мы протестировали логику проверки путем создания модульных тестов для наших уровня службы. Далее мы протестировали логику потока управления путем создания модульных тестов для наших слоя контроллера. При тестировании наш уровень службы, мы изолируются наши тесты для нашей службы слоя из наших уровня репозитория имитации нашей уровня репозитория. При тестировании на уровне контроллера, мы изолируются наши тесты для наших слоя контроллера имитации уровня службы.

В следующей итерации мы изменить приложение диспетчера контактов, чтобы он поддерживал группы контактов. Мы добавим эти новые командлеты для нашего приложения с помощью процесса разработки программного обеспечения, называемого управляемой тестами разработки.

> [!div class="step-by-step"]
> [Назад](iteration-4-make-the-application-loosely-coupled-vb.md)
> [Вперед](iteration-6-use-test-driven-development-vb.md)
