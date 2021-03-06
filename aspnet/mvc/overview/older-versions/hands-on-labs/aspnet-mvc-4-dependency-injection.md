---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: Внедрение зависимостей в ASP.NET MVC 4 | Документы Microsoft
author: rick-anderson
description: 'Примечание: Это Практическое лабораторное занятие предполагается наличие базовых знаний о фильтрах ASP.NET MVC и ASP.NET MVC 4. Если вы не использовали фильтров ASP.NET MVC 4 перед мы rec...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: e6c24d03039f0e6005948a73348589627c9df2df
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-dependency-injection"></a>Внедрение зависимостей в ASP.NET MVC 4

По [Web лагеря команды](https://twitter.com/webcamps)

[Загрузите комплект учебных материалов лагеря Web](https://aka.ms/webcamps-training-kit)

Это Практическое лабораторное занятие предполагает иметь базовые знания об **ASP.NET MVC** и **фильтров ASP.NET MVC 4**. Если вы не использовали **фильтров ASP.NET MVC 4** раньше, мы рекомендуем перейти **настраиваемые действия ASP.NET MVC фильтры** Практическое лабораторное занятие.

> [!NOTE]
> Все образцы кода и фрагменты кода включаются в Web лагеря комплект учебных материалов, доступные в [выпуски Microsoft Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Проект для этой лаборатории доступен на [внедрения зависимостей ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).

В **объектно-ориентированное программирование** парадигме, совместной работы объектов в модели совместная работа которых содержится участников и пользователей. Естественно эта модель связи приводит к возникновению ошибки зависимости между объектами и компонентами, становится трудно управлять при увеличении сложности.

![Класс зависимости и сложности модели](aspnet-mvc-4-dependency-injection/_static/image1.png "класса зависимости и сложности модели")

*Класс зависимости и сложность модели*

Возможно, вы слышали о **шаблон фабрики** и разделения между интерфейсом и реализации с помощью служб, где клиентские объекты часто отвечают за расположение службы.

Шаблон внедрения зависимостей — конкретной реализации инверсии элемента управления. **Инверсии управления (IoC)** означает, что объекты не создавать другие объекты, на которые они используют для выполнения своих задач. Вместо этого они получить объекты, которые им необходимы из внешнего источника (например, файл конфигурации xml).

**Внедрения зависимости (DI)** означает, что это осуществляется без вмешательства объекта, обычно компонентом платформы, который передает параметры конструктора и задать свойства.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>Шаблон разработки (DI) внедрения зависимостей

На высоком уровне внедрения зависимостей предназначена, класс клиента (например *golfer*) требуется нечто, удовлетворяющий интерфейс (например *IClub*). Не проверяет, имеет конкретный тип (например *WedgeClub WoodClub IronClub,* или *PutterClub*), ему кто-то другой для обработки (например хорошо *caddy*). Сопоставитель зависимостей в ASP.NET MVC позволяет зарегистрировать где-нибудь еще логику зависимостей (например контейнера или *контейнера треф*).

![Диаграмма внедрения зависимостей](aspnet-mvc-4-dependency-injection/_static/image2.png "рисунке внедрения зависимости")

*Внедрение зависимостей - аналогию Гольф*

Ниже перечислены преимущества использования шаблона внедрения зависимостей и инверсии элемента управления.

- Уменьшает соединения классов
- Увеличивает повторное использование кода
- Повышает удобство поддержки кода
- Повышает тестирование приложения

> [!NOTE]
> Внедрение зависимостей, иногда сравнивается с абстрактный фабричного конструктивного шаблона, но есть небольшие различия между оба подхода. DI установлена платформа Framework над за тем, чтобы устранить зависимости, для вызова фабрики и зарегистрированных служб.


Теперь, когда вы знаете шаблон внедрения зависимостей, вы узнаете в этой лаборатории как они применяются в ASP.NET MVC 4. Сначала с помощью внедрения зависимости в **контроллеров** служба доступа к базе данных. Затем примените внедрения зависимостей для **представления** для использования службы и отображения сведений. Наконец можно расширить DI в ASP.NET MVC 4 фильтры, добавление пользовательского фильтра действий в решении.

В этой лаборатории практических вы узнаете, как:

- Интеграция ASP.NET MVC 4 с помощью Unity для внедрения зависимости, с помощью пакетов NuGet
- Используют внедрение зависимостей внутри контроллера ASP.NET MVC
- Используют внедрение зависимостей в представлении ASP.NET MVC
- Используют внедрение зависимостей в ASP.NET MVC фильтра действий

> [!NOTE]
> Эта лаборатория использует Unity.Mvc3 пакет NuGet для разрешения зависимостей, но можно адаптировать любую платформу внедрения зависимостей для работы с ASP.NET MVC 4.


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Предварительные требования

Необходимо иметь следующие элементы для этой лаборатории.

- [Microsoft Visual Studio Express 2012 для Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) или выше (чтение [приложение A](#AppendixA) инструкции по его установке).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Установка

**Установка фрагменты кода**

Для удобства большая часть кода, который вы планируете управлять вдоль этой лаборатории доступна как фрагменты кода Visual Studio. Чтобы установить фрагменты кода запуска **.\Source\Setup\CodeSnippets.vsi** файла.

Если вы не знакомы с фрагментов кода Visual Studio и хотите узнать о способах их использования, можно ссылаться в приложение из этого документа &quot; [с помощью фрагментов кода в приложении б](#AppendixB)&quot;.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Упражнения

Это Практическое лабораторное занятие состоит в выполнении следующих упражнений.

1. [Упражнение 1: Добавление контроллера](#Exercise1)
2. [Упражнение 2: Добавление представления](#Exercise2)
3. [Упражнение 3: Добавление фильтров](#Exercise3)

> [!NOTE]
> Каждого упражнения сопровождается **окончания** папку, содержащую полученное в результате решение, должен быть получен после завершения выполнения упражнений. Это решение можно использовать как руководство, если вам нужна дополнительная помощь при выполнении упражнений.


Предполагаемое время для выполнения этого занятия: **30 минут**.

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>Упражнение 1: Добавление контроллера

В этом упражнении вы узнаете, как использовать внедрение зависимостей в ASP.NET MVC Controllers интегрируя Unity с помощью пакета NuGet. По этой причине будут включены в контроллерах MvcMusicStore для отделения логики доступа к данным служб. В конструктор контроллера, который будет разрешен с помощью внедрения зависимости с помощью служб создается новая зависимость **Unity**.

Такой подход будет показано, как создать менее связанных приложений, которые являются более гибкими и простыми в обслуживании и тестировании. Также вы узнаете, как интегрировать ASP.NET MVC с помощью Unity.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>О службе StoreManager

MVC Music Store, предоставляемые в решении begin теперь включает службу, которая управляет контроллера хранилища данных с именем **StoreService**. Ниже Вы найдете реализации службы хранилища. Обратите внимание, что все методы возвращают сущности модели.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

**StoreController** из начала решение использует **StoreService**. Ссылки на данные были удалены из **StoreController**и теперь можно изменить текущий поставщик доступа к данным без изменения любой метод, который использует **StoreService**.

Вы найдете ниже, **StoreController** реализация имеет зависимость с **StoreService** внутри конструктора класса.

> [!NOTE]
> Зависимости, представленные в этом упражнении, связанные с **инверсии управления** (IoC).
> 
> **StoreController** конструктор класса принимает **IStoreService** параметру типа, который необходим для выполнения вызовов службы от внутри класса. Тем не менее **StoreController** не реализует конструктор по умолчанию (с без параметров), любой контроллер необходимы для работы с ASP.NET MVC.
> 
> Чтобы устранить зависимость, контроллер должна создаваться фабрикой абстрактным (класс, который возвращает любой объект указанного типа).


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> Вы получите ошибку при попытке создать StoreController без отправки объекта службы, как отсутствует конструктор без параметров объявлен класс.


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>Задача 1. запуск приложения

В этой задаче будет запускаться приложение Begin, который включает в себя контроллер хранилища, который отделяет доступа к данным от логики приложения службы.

При запуске приложения, получит сообщение об ошибке, как служба контроллера не передается как параметр по умолчанию:

1. Откройте **начать** решение находится в **вводится Source\Ex01 Controller\Begin**.

   1. Необходимо загрузить несколько отсутствующих пакетов NuGet прежде чем продолжить. Чтобы сделать это, нажмите кнопку **проекта** и выбрать пункт **управление пакетами NuGet**.
   2. В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.
   3. Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.

      > [!NOTE]
      > Одним из преимуществ использования NuGet является у вас не указан для отправки всех библиотек в вашем проекте, уменьшив размер проекта. С помощью NuGet Power Tools указав версий пакета в файле Packages.config можно для загрузки всех необходимых библиотек первый раз, при запуске проекта. Вот почему необходимо будет выполнить эти шаги после открытия существующего решения в этой лаборатории.
2. Нажмите клавишу **сочетание клавиш Ctrl + F5** для запуска приложения без отладки. Вы получите сообщение об ошибке &quot; **нет конструктора без параметров, определенные для этого объекта**&quot;:

    ![Ошибка при выполнении приложения начать ASP.NET MVC](aspnet-mvc-4-dependency-injection/_static/image3.png "ошибка во время выполнения приложения начать ASP.NET MVC")

    *Ошибка при выполнении приложения начать ASP.NET MVC*
3. Закройте браузер.

В следующих шагах вы будете работать решения хранилища музыки для внедрения зависимости, необходимые для этого контроллера.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>Задача 2 - включая Unity в решение MvcMusicStore

В этой задаче будет включать **Unity.Mvc3** пакет NuGet для решения.

> [!NOTE]
> Unity.Mvc3 пакет, предназначенный для ASP.NET MVC 3, но он является полностью совместимым с ASP.NET MVC 4.
> 
> Unity — например, контейнер внедрения зависимостей компактную, расширяемую с дополнительной поддержки и типа. Он является универсальным контейнером для использования в любом приложении .NET. Он предоставляет общие функции, найден в том числе механизмах внедрения зависимостей: создание объектов, абстракции требований путем указания зависимости во время выполнения и гибкость, откладывая конфигурации компонента в контейнер.


1. Установка **Unity.Mvc3** пакет NuGet в **MvcMusicStore** проекта. Чтобы сделать это, откройте **консоль диспетчера пакетов** из **представление** | **другие окна**.
2. Выполните следующую команду:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Установка пакета NuGet Unity.Mvc3](aspnet-mvc-4-dependency-injection/_static/image4.png "Установка пакета NuGet Unity.Mvc3")

    *Установка пакета NuGet Unity.Mvc3*
3. Один раз **Unity.Mvc3** пакет установлен, просмотрите файлы и папки, автоматически добавляет для упрощения конфигурации Unity.

    ![Установлен пакет Unity.Mvc3](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 пакета")

    *Установлен пакет Unity.Mvc3*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a>Задача 3 - регистрация Unity в приложении Global.asax.cs\_запуск

В этой задаче будет обновлена **приложения\_запустить** метод находится в **Global.asax.cs** вызов инициализатора загрузчика Unity и затем обновить регистрации файла загрузчика Службы и контроллер используется для внедрения зависимости.

1. Теперь будет подключать загрузчика, хранящийся в файле, который инициализирует контейнера Unity и сопоставителя зависимостей. Чтобы сделать это, откройте **Global.asax.cs** и добавьте следующий выделенный код в **приложения\_запустить** метод.

    (Фрагмент - кода *Unity инициализировать лаборатории внедрения зависимостей ASP.NET - Ex01 -*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. Откройте **Bootstrapper.cs** файла.
3. Включите следующие пространства имен: **MvcMusicStore.Services** и **MusicStore.Controllers**.

    (Фрагмент - кода *ASP.NET внедрения зависимостей лаборатории - Ex01 - загрузчика добавление пространств имен*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. Замените **BuildUnityContainer** метод содержимого со следующим кодом, который регистрирует контроллера хранилища и службы хранилища.

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex01 - хранилище регистра контроллера и службы*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Задача 4. запуск приложения

В этой задаче будет выполняться приложение, чтобы убедиться, что теперь загрузки после включения Unity.

1. Нажмите клавишу **F5** для запуска приложения, приложение теперь следует загрузить без отображения сообщения об ошибке.

    ![Запуск приложения с помощью внедрения зависимости](aspnet-mvc-4-dependency-injection/_static/image6.png "запуск приложения с помощью внедрения зависимости")

    *Запуск приложения с помощью внедрения зависимости*
2. Перейдите к **или сохранений**. Это вызовет **StoreController**, который создается с помощью **Unity**.

    ![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")

    *MVC Music Store*
3. Закройте браузер.

В следующих упражнениях вы узнаете, как расширить область внедрения зависимостей, чтобы использовать его внутри представления ASP.NET MVC и фильтры действий.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>Упражнение 2: Добавление представления

В этом упражнении вы узнаете, как использовать внедрение зависимостей в представлении с новыми функциями ASP.NET MVC 4 для интеграции Unity. Чтобы сделать это, будет вызываться пользовательская служба внутри представления обзор хранилища, который будет отображать сообщение и образ ниже.

Затем будет интегрировать проекта Unity и создать пользовательскую зависимость Сопоставитель для внедрения зависимостей.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>Задача 1. Создание представления, использующее службу

В этой задаче вы создадите представление, которое выполняет вызов службы для создания новых зависимостей. Служба состоит в простой службы обмена сообщениями, включенные в это решение.

1. Откройте **начать** решение находится в **вводится Source\Ex02 View\Begin** папки. В противном случае можно продолжить использование **окончания** решения получен путем выполнения в предыдущем упражнении.

   1. Если вы открыли указанных **начать** решение, необходимо будет загрузить несколько отсутствующих пакетов NuGet прежде чем продолжить. Чтобы сделать это, нажмите кнопку **проекта** и выбрать пункт **управление пакетами NuGet**.
   2. В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.
   3. Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.

      > [!NOTE]
      > Одним из преимуществ использования NuGet является у вас не указан для отправки всех библиотек в вашем проекте, уменьшив размер проекта. С помощью NuGet Power Tools указав версий пакета в файле Packages.config можно для загрузки всех необходимых библиотек первый раз, при запуске проекта. Вот почему необходимо будет выполнить эти шаги после открытия существующего решения в этой лаборатории.
      > 
      > Дополнительные сведения см. в разделе этой статьи: [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Включить **MessageService.cs** и **IMessageService.cs** классы находятся в **источника \Assets** папки в **/службы**. Для этого щелкните правой кнопкой мыши **службы** папку и выберите **Добавление существующего элемента**. Перейдите в расположение файлов и включить их.

    ![Добавление службы сообщений и интерфейс службы](aspnet-mvc-4-dependency-injection/_static/image8.png "Добавление службы сообщений и интерфейс службы")

    *Добавление службы сообщений и интерфейс службы*

    > [!NOTE]
    > **IMessageService** интерфейс определяет два свойства, реализуемый **MessageService** класса. Эти свойства -**сообщение** и **ImageUrl**-сохранить сообщение и URL-адрес изображения для отображения.
3. Создать папку **/страницы** в проекте корневой папки, а затем добавьте существующий класс **MyBasePage.cs** из **Source\Assets**. Базовой страницы, который будет наследовать имеет следующую структуру.

    ![Папка страниц](aspnet-mvc-4-dependency-injection/_static/image9.png "папок")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. Откройте **Browse.cshtml** просмотра из **/представления/Store** папки и сделать его наследуют **MyBasePage.cs**.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. В **Обзор** Просмотр, добавьте вызов **MessageService** для отображения изображения и сообщения, полученные службой.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>Задача 2 - включая Сопоставитель пользовательскую зависимость и активатор страницы представления

В предыдущей задаче введенный новой зависимости внутри представления для выполнения вызова служб внутри него. Теперь будет разрешить зависимость путем реализации интерфейсов внедрения зависимостей MVC ASP.NET **IViewPageActivator** и **IDependencyResolver**. В решение будет включать реализацию **IDependencyResolver** , будет работать с Получение службы с помощью Unity. Затем следует включить другую пользовательскую реализацию **IViewPageActivator** интерфейс, который предстоит решить создания представлений.

> [!NOTE]
> С момента ASP.NET MVC 3 реализацию для внедрения зависимостей упрощен интерфейсы для регистрации службы. **IDependencyResolver** и **IViewPageActivator** являются частью функции ASP.NET MVC 3 для внедрения зависимости.
> 
> **-IDependencyResolver** интерфейс заменяет предыдущие IMvcServiceLocator. Объекты, реализующие IDependencyResolver должен возвращать экземпляр службы или службы коллекции.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator** интерфейс обеспечивает более точное управление как просмотр страниц создаются через внедрения зависимостей. Классы, реализующие **IViewPageActivator** интерфейса можно создавать экземпляры представление, используя сведения о контексте.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. Создать /**фабрик** папку в корневой папке проекта.
2. Включить **CustomViewPageActivator.cs** решение из **/источники/активы/** для **фабрик** папки. Чтобы сделать это, щелкните правой кнопкой мыши **/Factories** выберите **добавить | Существующий элемент** , а затем выберите **CustomViewPageActivator.cs**. Этот класс реализует **IViewPageActivator** интерфейс для хранения контейнера Unity.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator** отвечает за управление созданием представления с помощью контейнера Unity.
3. Включить **UnityDependencyResolver.cs** файл из **/источники/активы** для **/Factories** папки. Чтобы сделать это, щелкните правой кнопкой мыши **/Factories** выберите **добавить | Существующий элемент** , а затем выберите **UnityDependencyResolver.cs** файла.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver** класс является пользовательской DependencyResolver для Unity. Если службу не удается найти внутри контейнера Unity, является invocated базового сопоставителя.

В следующей задаче будет зарегистрирован обе реализации для модели известно расположение службы и представления.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>Задача 3. Регистрация для внедрения зависимости в пределах контейнера Unity

В этой задаче будет помещено все предыдущие о вместе, чтобы сделать работать внедрения зависимостей.

До сих решения содержит следующие элементы:

- Объект **Обзор** представление, которое наследует от **MyBaseClass с помощью модификатора** и использует **MessageService**.
- Промежуточный класс -**MyBaseClass с помощью модификатора**-с внедрения зависимостей, объявленным для интерфейса службы.
- Службе - **MessageService** - и интерфейс **IMessageService**.
- Сопоставитель пользовательскую зависимость для Unity - **UnityDependencyResolver** -, реагирует на получение службы.
- Активатор страницы представления - **CustomViewPageActivator** -, создающее страницу.

Для вставки **Обзор** представления, теперь зарегистрируйте Сопоставитель пользовательскую зависимость в контейнере Unity.

1. Откройте **Bootstrapper.cs** файла.
2. Регистрация экземпляра **MessageService** в Unity контейнер для инициализации службы:

    (Фрагмент - кода *службу сообщение Register лаборатории - Ex02 - внедрения зависимостей ASP.NET*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. Добавьте ссылку на **MvcMusicStore.Factories** пространства имен.

    (Фрагмент - кода *пространство имен фабрики лаборатории - Ex02 - внедрения зависимостей ASP.NET*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. Зарегистрировать **CustomViewPageActivator** как активатор страницы представления в Unity контейнер:

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex02 - Register CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. Замените экземпляр по умолчанию сопоставителем зависимостей ASP.NET MVC 4 **UnityDependencyResolver**. Для этого замените **Initialise** метод содержимого с помощью следующего кода:

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex02 - обновления Сопоставитель зависимостей*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC предоставляет класс Сопоставитель зависимостей по умолчанию. Для работы с распознаватели пользовательскую зависимость, которая создана unity, должно быть заменено этим распознавателем.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Задача 4. запуск приложения

В этой задаче будет выполняться приложение, чтобы убедиться, что обозреватель хранилища использует службу и показывает образа и получить сообщение:

1. Нажмите клавишу **F5** для запуска приложения.
2. Нажмите кнопку **рок** в меню жанров и см. в разделе как **MessageService** подставленный к представлению и загрузке приветственное сообщение и изображения. В этом примере вводится для &quot; **рок**&quot;:

    ![Внедрение представления MVC Music Store -](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - представление внедрения")

    *MVC Music Store - представление внедрения*
3. Закройте браузер.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>Упражнение 3: Добавление фильтров действий

В предыдущей практической **настраиваемые фильтры действий** вы работали с путем внедрения кода и настройки фильтров. В этом упражнении вы узнаете, как ввести фильтры с внедрения зависимостей с помощью контейнера Unity. Чтобы сделать это, вы добавите в решение Music Store пользовательского фильтра действий, будет отслеживать действия узла.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>Задача 1 - включение фильтра отслеживания в решении

В этой задаче будут включены в Music Store пользовательского фильтра действий для событий трассировки. Основные понятия как пользовательского фильтра действий, всегда обрабатываются в предыдущем лаборатории &quot;пользовательских фильтров действий&quot;, необходимо просто добавить класс фильтра из папки Assets этой лабораторной и затем создать поставщик фильтра для Unity:

1. Откройте **начать** решение находится в **Source\Ex03 - Filter\Begin действие вводится** папки. В противном случае можно продолжить использование **окончания** решения получен путем выполнения в предыдущем упражнении.

   1. Если вы открыли указанных **начать** решение, необходимо будет загрузить несколько отсутствующих пакетов NuGet прежде чем продолжить. Чтобы сделать это, нажмите кнопку **проекта** и выбрать пункт **управление пакетами NuGet**.
   2. В **управление пакетами NuGet** диалоговое окно, нажмите кнопку **восстановить** чтобы скачивать отсутствующие пакеты.
   3. Наконец, постройте решение, нажав кнопку **построения** | **построить решение**.

      > [!NOTE]
      > Одним из преимуществ использования NuGet является у вас не указан для отправки всех библиотек в вашем проекте, уменьшив размер проекта. С помощью NuGet Power Tools указав версий пакета в файле Packages.config можно для загрузки всех необходимых библиотек первый раз, при запуске проекта. Вот почему необходимо будет выполнить эти шаги после открытия существующего решения в этой лаборатории.
      > 
      > Дополнительные сведения см. в разделе этой статьи: [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Включить **TraceActionFilter.cs** файл из **/источники/активы** для **/фильтрует** папки.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > Этот фильтр настраиваемое действие выполняет трассировку ASP.NET. Вы можете проверить &quot;локальный ASP.NET MVC 4 и динамические фильтры действий&quot; лаборатории для получения дополнительной справки.
3. Добавление пустой класс **FilterProvider.cs** в проект в папке **или фильтры.**
4. Добавить **System.Web.Mvc** и **Microsoft.Practices.Unity** пространства имен в **FilterProvider.cs**.

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex03 - фильтр поставщика добавление пространств имен*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. Сделайте класс наследовал от **IFilterProvider** интерфейса.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. Добавить **IUnityContainer** свойство в **FilterProvider** класса, а затем создать конструктор класса, чтобы назначить контейнера.

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex03 - фильтра Конструктор поставщика*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > Конструктор класса поставщика фильтра не создавая **новый** внутри объекта. Контейнера передается в качестве параметра, а зависимость решается путем Unity.
7. В **FilterProvider** , следует реализовать метод **GetFilters** из **IFilterProvider** интерфейса.

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex03 - фильтр поставщика GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>Задача 2 - регистрация и включение фильтра

В этой задаче будет включить отслеживание сайта. Для этого потребуется зарегистрировать фильтр в **Bootstrapper.cs BuildUnityContainer** метода для запуска трассировки:

1. Откройте **Web.config** находится в корневой каталог проекта, а также включение трассировки отслеживания в группе System.Web.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. Откройте **Bootstrapper.cs** корне проекта.
3. Добавьте ссылку на **MvcMusicStore.Filters** пространства имен.

    (Фрагмент - кода *ASP.NET внедрения зависимостей лаборатории - Ex03 - загрузчика добавление пространств имен*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. Выберите **BuildUnityContainer** метод и зарегистрировать фильтр в контейнере Unity. Необходимо зарегистрировать поставщик фильтра, а также действие фильтра.

    (Фрагмент - кода *ASP.NET зависимостей внедрения лаборатории - Ex03 - Register FilterProvider и ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Задача 3. запуск приложения

В этой задаче будет запустите приложение и проверить, что пользовательского фильтра действий трассировка действия:

1. Нажмите клавишу **F5** для запуска приложения.
2. Нажмите кнопку **рок** жанров меню. Можно указать несколько жанров, если вы хотите.

    ![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")

    *Приложение Music Store*
3. Перейдите к **/Trace.axd** для просмотра трассировки приложения и нажмите кнопку **Просмотр сведений о**.

    ![Журнал трассировки приложения](aspnet-mvc-4-dependency-injection/_static/image12.png "журнал трассировки приложения")

    *Журнал трассировки приложения*

    ![Трассировка приложения - сведения о запросе](aspnet-mvc-4-dependency-injection/_static/image13.png "трассировки приложения - сведения о запросе")

    *Трассировка приложения - сведения о запросе*
4. Закройте браузер.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Сводка

Выполнив это Практическое лабораторное занятие изучено используют внедрение зависимостей в ASP.NET MVC 4, интегрируя Unity с помощью пакета NuGet. Чтобы добиться этого, вы использовали внедрения зависимости внутри контроллеров, представлений и фильтры действий.

Были освещены следующие понятия:

- Возможности внедрения зависимостей ASP.NET MVC 4
- Интеграция с Unity с помощью пакета NuGet Unity.Mvc3
- Внедрение зависимостей в контроллерах
- Внедрение зависимостей в представлениях
- Внедрение зависимостей фильтров действий

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Приложение а. Установка Visual Studio Express 2012 для Web

Можно установить **Microsoft Visual Studio Express 2012 для Web** или другой &quot;Express&quot; версию, используя **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. Следующие инструкции описывают действия, необходимые для установки *Visual studio Express 2012 для Web* с помощью *Microsoft Web Platform Installer*.

1. Последовательно выберите пункты [ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Кроме того, если вы уже установили установщика веб-платформы, можно открыть его и выполните поиск продукта &quot; <em>Visual Studio Express 2012 для Web с пакетом Windows Azure SDK</em>&quot;.
2. Щелкните **установить сейчас**. Если у вас **Web Platform Installer** вы будете перенаправлены, чтобы загрузить и установить ее сначала.
3. Один раз **Web Platform Installer** открыто, нажмите кнопку **установить** для запуска программы установки.

    ![Установка Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "установка Visual Studio Express")

    *Установка Visual Studio Express*
4. Чтение всех продуктов лицензий и условия и нажмите кнопку **принимаю** для продолжения.

    ![Принятие условий лицензионного соглашения](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *Принятие условий лицензионного соглашения*
5. Дождитесь завершения процесса загрузки и установки.

    ![Ход установки](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *Ход выполнения установки*
6. По завершении установки нажмите кнопку **Готово**.

    ![Установка завершена](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *Установка завершена*
7. Нажмите кнопку **выхода** закрыть установщик веб-платформы.
8. Чтобы открыть Visual Studio Express для Web, перейдите к **запустить** экрана и начинается запись &quot; **VS Express**&quot;, выберите команду **VS Express для Web** Плитка.

    ![VS Express для Web плитки](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express для Web плитки*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Приложение б. фрагменты кода

С помощью фрагментов кода у вас есть весь код, который требуется под рукой. Документ лаборатории сообщает только при их использовании, как показано на следующем рисунке.

![Фрагменты кода Visual Studio для вставки кода в проекте](aspnet-mvc-4-dependency-injection/_static/image19.png "фрагменты кода с помощью Visual Studio вставьте код в проект")

*Фрагменты кода Visual Studio для вставки кода в проекте*

***Добавление фрагмента кода, с помощью клавиатуры (только C#)***

1. Поместите курсор в место вставки кода.
2. Начните вводить имя фрагмента (без пробелов и дефисы).
3. Смотрите, как IntelliSense отображает, совпадающие с именами фрагменты.
4. Выберите правильный фрагмент (или продолжите ввод, пока не будет выделен весь фрагмент имени).
5. Нажмите клавишу Tab дважды, чтобы вставить фрагмент в положении курсора.

![Начните вводить имя фрагмента](aspnet-mvc-4-dependency-injection/_static/image20.png "начните вводить имя фрагмента")

*Начните вводить имя фрагмента*

![Нажмите клавишу Tab, чтобы выделить выделенный фрагмент](aspnet-mvc-4-dependency-injection/_static/image21.png "нажмите клавишу Tab, чтобы выделить выделенный фрагмент")

*Нажмите клавишу Tab, чтобы выделить выделенный фрагмент*

![Снова нажмите клавишу Tab и фрагмент будет расширен](aspnet-mvc-4-dependency-injection/_static/image22.png "будет расширен, снова нажмите клавишу Tab и фрагмента кода")

*Снова нажмите клавишу Tab и фрагмент будет расширен*

***Добавление фрагмента кода, с помощью мыши (C#, Visual Basic и XML)*** 1. Щелкните правой кнопкой мыши место вставки фрагмента кода.

1. Выберите **вставить фрагмент** следуют **Мои фрагменты кода**.
2. Выберите соответствующий фрагмент из списка, щелкнув по ней.

![Щелкните правой кнопкой мыши место для вставки фрагмента кода и выбора вставить фрагмент](aspnet-mvc-4-dependency-injection/_static/image23.png "место для вставки фрагмента кода и выбора вставить фрагмент кода щелкните правой кнопкой мыши")

*Щелкните правой кнопкой мыши в место вставки фрагмента кода и выберите Вставить фрагмент*

![Выберите из списка, соответствующего фрагмента, щелкнув его](aspnet-mvc-4-dependency-injection/_static/image24.png "выбрать соответствующий фрагмент из списка, щелкнув по ней")

*Выберите соответствующий фрагмент из списка, щелкнув по ней*
