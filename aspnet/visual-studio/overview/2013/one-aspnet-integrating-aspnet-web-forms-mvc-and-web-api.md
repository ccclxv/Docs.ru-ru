---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'Практическое лабораторное занятие: Один ASP.NET: интеграция веб-форм ASP.NET, MVC и веб-API | Документы Microsoft'
author: rick-anderson
description: ASP.NET — это платформа для создания веб-сайтов, приложений и служб с помощью специальных технологий, таких как MVC, веб-API и другие. С расширением ASP.NET h...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 55109723e566a9f7c66c1a59414377b05dbec760
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>Практическое лабораторное занятие: Один ASP.NET: интеграция веб-форм ASP.NET, MVC и веб-API
====================
по [Web лагеря команды](https://twitter.com/webcamps)

[Загрузите комплект учебных материалов лагеря Web](http://aka.ms/webcamps-training-kit)

> ASP.NET — это платформа для создания веб-сайтов, приложений и служб с помощью специальных технологий, таких как MVC, веб-API и другие. С расширением ASP.NET с момента его создания и явных должны иметь эти технологии интеграции, предпринимались последних в работе по направлению к **One ASP.NET**.
> 
> Visual Studio 2013 вводит новую систему единой проектов, в которой можно построить приложение и использовать все технологии ASP.NET в одном проекте. Эта функция избавляет от необходимости выбора одной технологии в начале проекта и манипулятор с ним и вместо этого рекомендует использование нескольких платформ ASP.NET в рамках одного проекта.
> 
> Все образцы кода и фрагменты кода включаются в Web лагеря комплект учебных материалов, доступных в [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).


<a id="Overview"></a>
## <a name="overview"></a>Обзор

<a id="Objectives"></a>
### <a name="objectives"></a>Цели

В этой практической вы узнаете, как:

- Создать веб-сайт, на основе **One ASP.NET** тип проекта
- Использование разных **ASP.NET** платформ, например **MVC** и **веб-API** в одном проекте
- Определить основные компоненты **ASP.NET** приложения
- Воспользоваться преимуществами **формирование шаблонов ASP.NET** framework автоматически создавать контроллеры и представления для выполнения операций CRUD, основанные на классах вашей модели
- Предоставлять тот же набор сведений в машины - и восприятия форматы, используя правильное средство для каждого задания

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Предварительные требования

Для завершения этой практической требуется следующее:

- [Visual Studio Express 2013 для Web](https://www.microsoft.com/visualstudio/) или выше
- [Visual Studio 2013 с обновлением 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>Установка

Чтобы выполнить упражнения в этой практической, необходимо настроить среду.

1. Откройте проводник и найдите в лаборатории **источника** папки.
2. Щелкните правой кнопкой мыши **Setup.cmd** и выберите **Запуск от имени администратора** для запуска процесса установки, будет настроить среду и установить фрагменты кода Visual Studio для этой лабораторной работы.
3. Если отображается диалоговое окно контроля учетных записей, подтвердите действие для продолжения.

> [!NOTE]
> Убедитесь, что все зависимости для этой лабораторной работы вы вернули перед запуском программы установки.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Фрагменты кода

В документе лаборатории будет предложено вставлять блоки кода. Visual Studio к фрагментам кода, к которому можно получить из в Visual Studio 2013, чтобы избежать необходимости вручную добавить большая часть кода предоставляется для удобства.

> [!NOTE]
> Каждого упражнения сопровождается начальный решений, расположенный в **начать** папку расчетов, позволяющий выполнить каждого упражнения независимо от других. Имейте в виду, что фрагменты кода, которые добавляются во время упражнения, отсутствуют на их запуск решения и могут не работать до завершения этого упражнения. В исходном коде для упражнения, вы также найдете **окончания** папку, содержащую решение Visual Studio с кодом, полученный в результате выполнения действий в соответствующий упражнении. Эти решения можно использовать как рекомендации, если вам нужна дополнительная помощь, отвечая на этой практической.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>Упражнения

Данная практическая работа включает следующие упражнения:

1. [Создание нового проекта Web Forms](#Exercise1)
2. [Создание контроллера MVC с помощью формирования шаблонов](#Exercise2)
3. [Создание контроллера Web API, с помощью формирования шаблонов](#Exercise3)

Предполагаемое время для выполнения этого занятия: **60 минут**

> [!NOTE]
> При первом запуске Visual Studio, необходимо выбрать одну из коллекций предварительно определенных параметров. Каждая предопределенная коллекция соответствует конкретному стилю разработки и определяет макетов окон, поведение редактора, фрагменты кода IntelliSense и параметры диалогового окна. В этой лаборатории описаны действия, необходимые для выполнения данной задачи в Visual Studio при использовании **обычные параметры разработки** коллекции. При выборе другого набора параметров для среды разработки может быть отличия в этапах, которые следует принимать во внимание.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>Упражнение 1: Создание нового проекта Web Forms

В этом упражнении вы создадите новый узел веб-форм в Visual Studio 2013 с помощью **One ASP.NET** единого проекта, которые позволят легко интегрировать компоненты веб-форм, MVC и веб-API в одном приложении. Затем исследовать создаваемого решения и определения его частей, и наконец вы увидите веб-сайта в действии.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>Задача 1 – Создание нового сайта с помощью единый интерфейс ASP.NET

В этой задаче будет начать создание нового веб-узла в Visual Studio на основе **One ASP.NET** тип проекта. **Один ASP.NET** объединяет все технологии ASP.NET и дает возможность комбинировать и сопоставлять их в случае необходимости. Затем будет распознавать различные компоненты веб-форм, MVC и веб-API, находящихся рядом друг с другом в приложении.

1. Откройте **Visual Studio Express 2013 для Web** и выберите **файл | Создать проект...**  для запуска нового решения.

    ![Создание нового проекта](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *Создание нового проекта*
2. В **новый проект** выберите **веб-приложение ASP.NET** под **Visual C# | Web** вкладку и убедитесь, что **.NET Framework 4.5** выбран. Назовите проект *MyHybridSite*, выберите **расположение** и нажмите кнопку **ОК**.

    ![Новый проект веб-приложения ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *Создание нового проекта веб-приложения ASP.NET*
3. В **новый проект ASP.NET** выберите **Web Forms** шаблона и выберите **MVC** и **веб-API** параметры. Кроме того, убедитесь, что **проверки подлинности** включен режим **индивидуальные учетные записи**. Нажмите кнопку **ОК** , чтобы продолжить.

    ![Создание нового проекта с помощью шаблона веб-формы, включая компоненты веб-API и MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Создание нового проекта с помощью шаблона веб-формы, включая компоненты веб-API и MVC*
4. Теперь можно просмотреть структуру создаваемого решения.

    ![Изучение созданного решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *Изучение созданного решения*

    1. **Учетная запись:** эта папка содержит страницы веб-формы для регистрации, выполните вход и управление учетными записями пользователей приложения. Эта папка будет добавлена при **отдельных учетных записей пользователей** выбран параметр проверки подлинности во время настройки шаблона проекта веб-форм.
    2. **Модели:** эта папка будет содержать классы, представляющие данные приложения.
    3. **Контроллеры** и **представления**: этих папок являются обязательными для **ASP.NET MVC** и **веб-API ASP.NET** компонентов. Вы исследуете технологии MVC и веб-API при следующем выполнении упражнений.
    4. **Default.aspx**, **Contact.aspx** и **About.aspx** файлы, предварительно определенные страницы веб-форм, которые можно использовать в качестве начальных точек для создания страниц, относящиеся к вашей приложение. Программная логика этих файлов находится в отдельном файле называют &quot;кода&quot; файл, который имеет &quot;. aspx.vb&quot; или &quot;. aspx.cs&quot; расширения (в зависимости от язык, используемый). Логику кода выполняется на сервере и динамически создает выходные данные HTML для страницы.
    5. **Site.Master** и **Site.Mobile.Master** страницы определяют внешний вид и стандартное поведение всех страниц в приложении.
5. Дважды щелкните **Default.aspx** файл для просмотра содержимого страницы.

    ![Изучение страницу Default.aspx](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Изучение страницу Default.aspx*

    > [!NOTE]
    > **Страницы** директивы в начало файла определяет атрибуты, страницы веб-форм. Например **MasterPageFile** атрибут задает путь к главному страницы — в этом случае *Site.Master* страниц и **Inherits** определяет атрибут класса с выделенным кодом для страницы для наследования. Этот класс находится в файле определяется **CodeBehind** атрибута.
    > 
    > **Asp: Content** управления содержит фактическое содержимое страницы (текст, разметку и элементы управления) и сопоставляется с **asp: ContentPlaceHolder** управления на главной странице. В этом случае будет отображено содержимое страницы внутри *тегу* элемент управления, определенный в *Site.Master* страницы.
6. Разверните **приложения\_запустить** папки и обратите внимание, **WebApiConfig.cs** файла. Visual Studio этот файл включен в состав созданный решения вы включили веб-API при настройке проекта с помощью шаблона One ASP.NET.
7. Откройте **WebApiConfig.cs** файла. В *WebApiConfig* вы найдете конфигурации, связанные с веб-API, который сопоставляет HTTP класс направляет в **контроллеров веб-API**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. Откройте **RouteConfig.cs** файла. Внутри *RegisterRoutes* вы найдете конфигурации, связанной с MVC, который соответствует маршруту HTTP в метод **контроллеров MVC**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>Задача 2 – запуск решения

В этой задаче будет запустите созданный решение, исследовать приложения, а также некоторые функции, например перезаписи URL-адресов и встроенной проверки подлинности.

1. Чтобы запустить решение, нажмите клавиши **F5** или нажмите кнопку **запустить** кнопку, расположенную на панели инструментов. Домашняя страница приложения следует открывать в браузере.

    ![Запуск решения](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Проверьте, вызываемого страниц веб-форм. Чтобы сделать это, добавьте **/contact.aspx** URL-адрес в адресной строке и нажмите клавишу **ввод**.

    ![Понятные URL-адреса](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *Понятные URL-адреса*

    > [!NOTE]
    > Как видите, URL-адрес примет **или обратитесь**. Начиная с **ASP.NET 4**, были добавлены возможности маршрутизации URL-адрес веб-форм, можно создать URL-адреса, например *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* вместо  *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*. Дополнительные сведения см. в [маршрутизации URL-адрес](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).
3. Теперь вы исследуете поток проверки подлинности, который интегрируется в приложение. Чтобы сделать это, нажмите кнопку **зарегистрировать** в правом верхнем углу страницы.

    ![Регистрация нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *Регистрация нового пользователя*
4. В **зарегистрировать** введите **имя пользователя** и **пароль**, а затем нажмите кнопку **зарегистрировать**.

    ![Страница «Регистрация»](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *Страница «Регистрация»*
5. Приложение регистрирует новую учетную запись, и пользователь прошел проверку.

    ![Пользователь прошел проверку подлинности](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *Пользователь прошел проверку подлинности*
6. Вернитесь в Visual Studio и нажмите клавишу **SHIFT + F5** остановить отладку.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>Упражнение 2: Создание контроллер MVC с помощью формирования шаблонов

В этом упражнении будет воспользоваться преимуществами платформы формирование шаблонов ASP.NET, предоставляемые Visual Studio для создания контроллера ASP.NET MVC 5 с действиями и представлениями Razor для выполнения операций CRUD без написания ни единой строки кода. В процессе формирования шаблонов будет использоваться Entity Framework Code First для создания контекста данных и схему базы данных в базе данных SQL.

**Сначала о Entity Framework код**

Entity Framework (EF) является объектно реляционного сопоставления (ORM), который позволяет создавать приложения для доступа к данным путем программирования с концептуальной моделью приложения а не напрямую с помощью реляционной схеме хранения.

Процесс моделирования Entity Framework Code First можно использовать собственный домен классы для представления модели, использующая EF при выполнении запросов, функции отслеживания изменений и обновление. С помощью Code First рабочего процесса разработки, вы не обязательно должны начинаться приложения путем создания базы данных или указание схемы. Вместо этого можно написать стандартных классов .NET, определяющие наиболее подходящий объектами модели домена приложения и Entity Framework будет создана база данных автоматически.

> [!NOTE]
> Дополнительные сведения об Entity Framework [здесь](../../../entity-framework.md).


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>Задача 1 – Создание новой модели

Теперь мы определим **лицо** класс, который будет использовать в процессе формирования шаблонов для создания контроллера MVC и представления, модель. Начнем с создания **лицо** класс модели и операций CRUD в контроллере автоматически создается с помощью функции формирования шаблонов.

1. Откройте **Visual Studio Express 2013 для Web** и **MyHybridSite.sln** решение находится в **источника/Ex2-MvcScaffolding/начало** папки. Кроме того можно продолжить с решением, полученный в предыдущем упражнении.
2. В **обозревателе решений**, щелкните правой кнопкой мыши **моделей** папки **MyHybridSite** проект и выберите **добавить | Класс...** .

    ![Добавление класса Person модели](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Добавление класса Person модели*
3. В **Добавление нового элемента** диалоговое окно, имя файла *Person.cs* и нажмите кнопку **добавить**.

    ![Создание класса модели лица](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Создание класса модели лица*
4. Замените содержимое **Person.cs** файла следующим кодом. Нажмите клавишу **сочетание клавиш CTRL + S** для сохранения изменений.

    (Фрагмент - кода *PersonClass BringingTogetherOneAspNet - Ex2 -*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. В **обозревателе решений**, щелкните правой кнопкой мыши **MyHybridSite** проект и выберите **построения**, или нажмите клавишу **CTRL + SHIFT + B** для сборки проекта.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>Задача 2 – Создание контроллер MVC

Теперь, когда **лицо** модель создана, вы будете использовать формирование шаблонов ASP.NET MVC с Entity Framework для создания действия CRUD контроллера и представления для **лицо**.

1. В **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров** папки **MyHybridSite** проект и выберите **добавить | Новый элемент формирования шаблонов...** .

    ![Создание нового контроллера формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *Создание нового контроллера формирования шаблонов*
2. В **Добавление формирования шаблонов** выберите **контроллер MVC 5 с представлениями, использующий Entity Framework** и нажмите кнопку **Add.**

    ![При выборе контроллер MVC 5 с представлениями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *При выборе контроллер MVC 5 с представлениями и Entity Framework*
3. Задать *MvcPersonController* как **имя контроллера**выберите **использовать асинхронные действия контроллера** и выберите **лица (MyHybridSite.Models)**  как **класс модели**.

    ![Добавление контроллера MVC с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *Добавление контроллера MVC с помощью формирования шаблонов*
4. В разделе **класс контекста данных**, нажмите кнопку **новый контекст данных...** .

    ![Создание нового контекста данных](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *Создание нового контекста данных*
5. В **новый контекст данных** диалоговом имя новому контексту данных *PersonContext* и нажмите кнопку **добавить**.

    ![Создание нового PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *Создание нового типа PersonContext*
6. Нажмите кнопку **добавить** для создания нового контроллера для **лицо** с помощью формирования шаблонов. Visual Studio создаст действия контроллера, контекст пользователя данных и представлений Razor.

    ![После создания контроллер MVC с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *После создания контроллер MVC с помощью формирования шаблонов*
7. Откройте **MvcPersonController.cs** файла в **контроллеров** папки. Обратите внимание, что методы действия CRUD были созданы автоматически.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > Выбрав **использовать асинхронные действия контроллера** флажок из формирование шаблонов параметров в предыдущих шагах, Visual Studio создает асинхронные методы действия для всех действий, для которых требуется доступ к контексту данных пользователя. Рекомендуется использовать асинхронные методы действия для долго выполняющихся, не связаны с ЦП запросами, чтобы избежать блокировки веб-сервера от выполнения операций во время обработки запроса.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>Задача 3 – Запуск решения

В этой задаче будет выполняться представления для решения еще раз, чтобы убедиться, что **лицо** работают надлежащим образом. Будет добавлен новый пользователь, чтобы проверить, успешно сохранены в базе данных.

1. Нажмите клавишу **F5** для запуска решения.
2. Перейдите к **/MvcPerson**. Появится представление формирования шаблонов, показывающий список людей.
3. Нажмите кнопку **создать новый** для добавления нового пользователя.

    ![Переход к формирования шаблонов представлений MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *Переход к формирования шаблонов представлений MVC*
4. В **создать** просмотреть, укажите **имя** и **возраст** человека и нажмите кнопку **создать**.

    ![Добавление нового пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *Добавление нового пользователя*
5. Новый пользователь будет добавлен в список. В списке элементов выберите **сведения** для отображения представления сведений пользователя. Затем в **сведения** щелкните **списка** чтобы вернуться к представлению списка.

    ![Представление сведений пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *Представление сведений пользователя*
6. Нажмите кнопку **удалить** ссылку, чтобы удалить пользователя. В **удаление** щелкните **удаление** для подтверждения операции.

    ![Удаление пользователя](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *Удаление пользователя*
7. Вернитесь в Visual Studio и нажмите клавишу **SHIFT + F5** остановить отладку.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>Упражнение 3: Создание контроллера Web API, с помощью формирования шаблонов

Платформа веб-API является частью стека ASP.NET и предназначены для упрощения реализации службы HTTP, как правило, отправки и получения данных в формате JSON или XML через RESTful API.

В этом упражнении будет использовать формирование шаблонов ASP.NET попытку создать контроллер веб-API. Применяются те же **лицо** и **PersonContext** классы из предыдущего упражнения для предоставления данных того же пользователя в формате JSON. Вы увидите, как можно предоставить те же ресурсы по-разному, в то же приложение ASP.NET.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>Задача 1 – Создание контроллера Web API

В этой задаче вы создадите новый **контроллер Web API** , будет представлять данные пользователя в машину потребляемые формат JSON.

1. Если еще не открыт, откройте **Visual Studio Express 2013 для Web** и откройте **MyHybridSite.sln** решение находится в **источника/Ex3-WebAPI/начало** папки. Кроме того можно продолжить с решением, полученный в предыдущем упражнении.

    > [!NOTE]
    > Если вы запустите решение Begin с Упражнение 3, нажмите клавиши **CTRL + SHIFT + B** для построения решения.
2. В **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров** папки **MyHybridSite** проект и выберите **добавить | Новый элемент формирования шаблонов...** .

    ![Создание нового контроллера формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *Создание нового контроллера формирования шаблонов*
3. В **Добавление формирования шаблонов** выберите **веб-API** в левой панели, затем **Web API 2 контроллер с действиями, использующий Entity Framework** в средней области и нажмите кнопку  **Добавите.**

    ![При выборе 2 контроллер Web API с действиями и Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "при выборе Web API 2 контроллер с действиями и Entity Framework")

    *Выбор контроллера Web API 2 с действиями и Entity Framework*
4. Задать *ApiPersonController* как **имя контроллера**выберите **использовать асинхронные действия контроллера** и выберите **лица (MyHybridSite.Models)**  и **PersonContext (MyHybridSite.Models)** как **модель** и **контекст данных** классы соответственно. Затем нажмите кнопку **Добавить**.

    ![Добавление контроллера Web API с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Добавление контроллера веб-API с помощью формирования шаблонов")

    *Добавление контроллера веб-API с помощью формирования шаблонов*
5. Visual Studio создаст **ApiPersonController** класс с четырьмя действиями CRUD для работы с данными.

    ![После создания контроллера веб-API с помощью формирования шаблонов](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "после создания контроллера веб-API с помощью формирования шаблонов")

    *После создания контроллера веб-API с помощью формирования шаблонов*
6. Откройте **ApiPersonController.cs** файл и проверьте *GetPeople* метода действия. Этот метод отправляет запрос в поле db **PersonContext** тип для получения данных пользователей.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. Обратите внимание, комментарий выше определении метода. Он предоставляет URI, который представляет это действие, который будет использоваться в следующей задаче.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > По умолчанию должен перехватывать запросы к веб-API */api* путь для предотвращения конфликтов с контроллеров MVC. Если необходимо изменить эту настройку, см. [маршрутизации в ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>Задача 2 – запуск решения

В этой задаче будут использованы в Internet Explorer **средств разработчика F12** для проверки полного ответа от контроллера веб-API. Вы увидите, как можно записывать сетевой трафик, чтобы получить больше возможностей регулировать данные приложения.

> [!NOTE]
> Убедитесь, что **Internet Explorer** выбран в **запустить** кнопку, расположенную на панели инструментов Visual Studio.
> 
> ![Параметр Internet Explorer](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **Средств разработчика F12** имеют широкий набор функциональных возможностей, не включенные в это практическая работа. Если вы хотите узнать больше о ней, см. [с помощью средств разработчика F12](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).


1. Нажмите клавишу **F5** для запуска решения.

    > [!NOTE]
    > Чтобы правильно выполнить эту задачу, приложение должно иметь данные. Если базы данных пуст, можно вернуться к задаче 3 в упражнении 2 и выполните действия по созданию нового пользователя с помощью представлений MVC.
2. В браузере, нажмите клавишу **F12** Открытие **средств разработчика** панель. Нажмите клавишу **CTRL** + **4** или нажмите кнопку **сети** значок и нажмите кнопку с зеленой стрелкой, чтобы начать отслеживать сетевой трафик.

    ![Запуск записи сетевого трафика веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "записи сетевого трафика запуск веб-API")

    *Запуск записи сетевого трафика веб-API*
3. Добавление **api/ApiPerson** URL-адрес в адресной строке браузера. Теперь будет проверять сведения об ответе от **ApiPersonController**.

    ![Получение данных пользователя с помощью веб-API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "получение данных пользователя с помощью веб-API")

    *Получение данных по продажам через веб-API*

    > [!NOTE]
    > После завершения загрузки, будет предложено задать действие с помощью загруженного файла. Не закрывайте диалоговое окно для просмотра содержимого ответа с помощью окна инструментов для разработчиков.
4. Теперь будет проверять текст ответа. Чтобы сделать это, нажмите кнопку **сведения** и нажмите кнопку **текст ответа**. Можно проверить, что загруженные данные приведен список объектов со свойствами **идентификатор**, **имя** и **возраст** , которые соответствуют **лицо** класс.

    ![Просмотр веб-текст ответа API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "просмотра веб-текст ответа API")

    *Текст ответа API просмотра Web*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>Задача 3 – Добавление веб-страницы справки API

При создании веб-API, полезно создать страницу справки, чтобы другие разработчики знали способ вызова API. Можно создать и вручную обновить страницы документации, но лучше автоматически создавать их, чтобы избежать необходимости делать работ по обслуживанию. В этой задаче используется пакет Nuget для автоматического создания страниц справки веб-API в решение.

1. Из **средства** в Visual Studio, выберите пункт меню **диспетчер пакетов библиотеки**, а затем нажмите кнопку **консоль диспетчера пакетов**.
2. В **консоль диспетчера пакетов** окно, выполните следующую команду:

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft.AspNet.WebApi.HelpPage** пакет устанавливает необходимые сборки и добавляет представлений MVC для страницы справки, в разделе **областей или HelpPage** папки.

    ![Область HelpPage](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage области")

    *HelpPage области*
3. По умолчанию с помощью страницы имеют заполнитель строки для документации. Комментарии XML-документации можно использовать для создания документации. Чтобы включить эту функцию, откройте **HelpPageConfig.cs** файл, расположенный в **HelpPage области приложений и\_запустить** папки и раскомментируйте следующую строку:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. В **обозревателе решений**, щелкните правой кнопкой мыши проект **MyHybridSite**выберите **свойства** и нажмите кнопку **построения** вкладки.

    ![Вкладка Построение](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "построения раздела")

    *Вкладка Построение*
5. В разделе **вывода**выберите **XML-файл документации**. В поле ввода введите **приложения\_Data/XmlDocument.xml**.

    ![Вывод раздела вкладка построение](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "вывода раздела вкладка построение")

    *Выходные данные раздела вкладка построение*
6. Нажмите клавишу **CTRL** + **S** для сохранения изменений.
7. Откройте **ApiPersonController.cs** файл из **контроллеров** папки.
8. Введите новую строку между *GetPeople* сигнатуру метода и */ / api/ApiPerson GET* комментарий, а затем введите три косые черты.

    > [!NOTE]
    > Visual Studio автоматически добавляет XML-элементы, которые определяют документацию по методу.
9. Добавьте текст сводки и возвращаемое значение для *GetPeople* метод. Он должен выглядеть следующим образом.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. Нажмите клавишу **F5** для запуска решения.
11. Добавление **/help** URL-адрес в адресной строке, чтобы перейти к странице справки.

    ![Страница справки веб-API ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "страница справки веб-API ASP.NET")

    *Страница справки веб-API ASP.NET*

    > [!NOTE]
    > Основное содержимое страницы — это таблица, API-функций, сгруппированных по контроллера. Записи таблицы создаются динамически с помощью **IApiExplorer** интерфейса. Если добавить или обновить контроллер API, таблицы автоматически обновляется при очередном построения приложения.
    > 
    > **API** столбец содержит метод HTTP и относительного URI. **Описание** столбец содержит сведения, которые были извлечены из документации по данному методу.
12. Обратите внимание, что описание, которое вы добавили над определением метода отображается в столбце «Описание».

    ![Описание метода API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "описание метода API")

    *Описание метода API*
13. Выберите один из методов API, чтобы перейти на страницу с более подробными сведениями, включая примеры текстов ответа.

    ![Сведения о странице сведений о](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "страницу подробных сведений")

    *Страница подробные сведения*

* * *

<a id="Summary"></a>
## <a name="summary"></a>Сводка

Выполнив этой практической вы узнали, как:

- Создание нового веб-приложения, используя единый интерфейс ASP.NET в Visual Studio 2013
- Интегрировать несколько технологий ASP.NET в один отдельный проект
- Создать из классов модели с помощью формирования шаблонов ASP.NET MVC контроллеры и представления
- Создание контроллеров веб-API, которые используют функции, такие как асинхронного программирования и доступа к данным через Entity Framework
- Автоматически создавать веб-страницы справки API контроллеров
