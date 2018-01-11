---
title: "Страниц Razor с Entity Framework Core - учебник № 1 по 8."
author: rick-anderson
description: "Показано, как создать приложение страниц Razor с помощью Entity Framework Core"
keywords: "ASP.NET Core, Entity Framework Core, учебник"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/intro
ms.openlocfilehash: 86f9eceb5b8646e371811fa4611a4509ff652231
ms.sourcegitcommit: 2d23ea501e0213bbacf65298acf1c8bd17209540
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a><span data-ttu-id="3978b-104">Приступая к работе со страницами Razor и Entity Framework Core, с помощью Visual Studio (1, 8)</span><span class="sxs-lookup"><span data-stu-id="3978b-104">Getting started with Razor Pages and Entity Framework Core using Visual Studio (1 of 8)</span></span>

<span data-ttu-id="3978b-105">По [Tom Dykstra](https://github.com/tdykstra) и [Рик Андерсон](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3978b-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="3978b-106">Contoso университета образец веб-приложения показано, как создавать веб-приложения ASP.NET MVC 2.0 ядра с помощью основных Entity Framework (EF) 2.0 и Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3978b-106">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="3978b-107">Пример приложения является веб-сайт для вымышленной компании Contoso университета.</span><span class="sxs-lookup"><span data-stu-id="3978b-107">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="3978b-108">Он включает функции, такие как допуском студента, создание курса и инструктора назначения.</span><span class="sxs-lookup"><span data-stu-id="3978b-108">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="3978b-109">Эта страница является первой в серию учебников, в которых объясняется, как для создания примера приложения Contoso университета.</span><span class="sxs-lookup"><span data-stu-id="3978b-109">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="3978b-110">Загрузить или просмотреть завершенное приложение.</span><span class="sxs-lookup"><span data-stu-id="3978b-110">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="3978b-111">[Инструкции по загрузке](xref:tutorials/index#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="3978b-111">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3978b-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3978b-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

<span data-ttu-id="3978b-113">Знакомство с [страниц Razor](xref:mvc/razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="3978b-113">Familiarity with [Razor Pages](xref:mvc/razor-pages/index).</span></span> <span data-ttu-id="3978b-114">Новый программисты должны заполнить [приступить к работе со страницами Razor](xref:tutorials/razor-pages/razor-pages-start) перед запуском этой серии.</span><span class="sxs-lookup"><span data-stu-id="3978b-114">New programmers should complete [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) before starting this series.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3978b-115">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3978b-115">Troubleshooting</span></span>

<span data-ttu-id="3978b-116">Если возникли проблемы, не удается устранить, обычно можно найти решения путем сравнения код, чтобы [завершения этапа](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) или [завершенного проекта](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span><span class="sxs-lookup"><span data-stu-id="3978b-116">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) or [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span></span> <span data-ttu-id="3978b-117">Список распространенных ошибок и способы их устранения см. в разделе [раздел "Устранение неполадок" последнего учебника в серии](xref:data/ef-mvc/advanced#common-errors).</span><span class="sxs-lookup"><span data-stu-id="3978b-117">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="3978b-118">Если вы не нашли нужную информацию существует, можно разместить вопрос StackOverflow.com для [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) или [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span><span class="sxs-lookup"><span data-stu-id="3978b-118">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="3978b-119">Эта серия учебников основан на выполняемые операции в предыдущих учебниках.</span><span class="sxs-lookup"><span data-stu-id="3978b-119">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="3978b-120">Рекомендуется сохранить копию проекта после каждого успешного завершения учебника.</span><span class="sxs-lookup"><span data-stu-id="3978b-120">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="3978b-121">Если возникли проблемы, можно начать сначала из предыдущего учебника вместо вернуться в начало.</span><span class="sxs-lookup"><span data-stu-id="3978b-121">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="3978b-122">Кроме того, вы можете загрузить [завершения этапа](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) и начать заново с помощью завершенной рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3978b-122">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="3978b-123">Contoso университета веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3978b-123">The Contoso University web app</span></span>

<span data-ttu-id="3978b-124">Приложения, созданного в этих учебниках является веб-сайта основные университета.</span><span class="sxs-lookup"><span data-stu-id="3978b-124">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="3978b-125">Пользователи могут просматривать и обновлять студента курса и инструктора сведения.</span><span class="sxs-lookup"><span data-stu-id="3978b-125">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="3978b-126">Ниже представлены несколько экранов, созданный в учебнике.</span><span class="sxs-lookup"><span data-stu-id="3978b-126">Here are a few of the screens created in the tutorial.</span></span>

![Страница индекса студентов](intro/_static/students-index.png)

![Страница изменения студентов](intro/_static/student-edit.png)

<span data-ttu-id="3978b-129">Приближается к создаваемой с помощью встроенных шаблонов стиля пользовательского интерфейса этого сайта.</span><span class="sxs-lookup"><span data-stu-id="3978b-129">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="3978b-130">Учебник основное внимание уделяется Core EF со страницами Razor не пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3978b-130">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="3978b-131">Создание страниц Razor веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3978b-131">Create a Razor Pages web app</span></span>

* <span data-ttu-id="3978b-132">В меню **Файл** Visual Studio откройте меню **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="3978b-132">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="3978b-133">Создайте новое веб-приложение ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3978b-133">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="3978b-134">Назовите проект **ContosoUniversity**.</span><span class="sxs-lookup"><span data-stu-id="3978b-134">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="3978b-135">Очень важно для проекта имя *ContosoUniversity* , пространства имен совпадение, если код является скопированные и вставленные.</span><span class="sxs-lookup"><span data-stu-id="3978b-135">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="3978b-136">![Новое веб-приложение ASP.NET Core](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="3978b-136">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="3978b-137">Выберите в раскрывающемся списке **ASP.NET Core 2.0**, а затем **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="3978b-137">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="3978b-138">![Веб-приложение (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="3978b-138">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="3978b-139">Нажмите клавишу **F5**, чтобы запустить приложение в режиме отладки, или **CTRL-F5**, чтобы запустить его без подключения отладчика.</span><span class="sxs-lookup"><span data-stu-id="3978b-139">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="3978b-140">Настройка стиля узла</span><span class="sxs-lookup"><span data-stu-id="3978b-140">Set up the site style</span></span>

<span data-ttu-id="3978b-141">Некоторые изменения настройки сайта меню, макета и домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="3978b-141">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="3978b-142">Откройте *Pages/_Layout.cshtml* и внесите следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="3978b-142">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="3978b-143">Изменить все вхождения «ContosoUniversity» на «Contoso University».</span><span class="sxs-lookup"><span data-stu-id="3978b-143">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="3978b-144">Нет трех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="3978b-144">There are three occurrences.</span></span>

* <span data-ttu-id="3978b-145">Добавление пунктов меню для **учащихся**, **курсы**, **инструкторов**, и **отделы**и удалите **контакт** меню.</span><span class="sxs-lookup"><span data-stu-id="3978b-145">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="3978b-146">Изменения выделены.</span><span class="sxs-lookup"><span data-stu-id="3978b-146">The changes are highlighted.</span></span> <span data-ttu-id="3978b-147">(Разметка является *не* отображается.)</span><span class="sxs-lookup"><span data-stu-id="3978b-147">(All the markup is *not* displayed.)</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

<span data-ttu-id="3978b-148">В *Pages/Index.cshtml*, замените содержимое файла следующим кодом, чтобы заменить текст о ASP.NET и MVC на текст об этом приложении:</span><span class="sxs-lookup"><span data-stu-id="3978b-148">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="3978b-149">Нажмите клавиши CTRL+F5, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="3978b-149">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="3978b-150">Домашняя страница отображается с вкладками, созданные в следующих учебниках:</span><span class="sxs-lookup"><span data-stu-id="3978b-150">The home page is displayed with tabs created in the following tutorials:</span></span>

![Домашняя страница университета Contoso](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="3978b-152">Создание модели данных</span><span class="sxs-lookup"><span data-stu-id="3978b-152">Create the data model</span></span>

<span data-ttu-id="3978b-153">Создание классов сущностей для приложения Contoso университета.</span><span class="sxs-lookup"><span data-stu-id="3978b-153">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="3978b-154">Начните со следующих трех сущностей:</span><span class="sxs-lookup"><span data-stu-id="3978b-154">Start with the following three entities:</span></span>

![Схема модели курса регистрации студента данных](intro/_static/data-model-diagram.png)

<span data-ttu-id="3978b-156">Имеется отношение "один ко многим" между `Student` и `Enrollment` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-156">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="3978b-157">Имеется отношение "один ко многим" между `Course` и `Enrollment` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-157">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="3978b-158">Студент может зарегистрироваться в любое количество курсов.</span><span class="sxs-lookup"><span data-stu-id="3978b-158">A student can enroll in any number of courses.</span></span> <span data-ttu-id="3978b-159">Курс может иметь любое количество студентов, зарегистрированных в нем.</span><span class="sxs-lookup"><span data-stu-id="3978b-159">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="3978b-160">В следующих разделах создается класс для каждого из этих сущностей.</span><span class="sxs-lookup"><span data-stu-id="3978b-160">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="3978b-161">Сущность Student</span><span class="sxs-lookup"><span data-stu-id="3978b-161">The Student entity</span></span>

![Схема entity студента](intro/_static/student-entity.png)

<span data-ttu-id="3978b-163">Создание *моделей* папки.</span><span class="sxs-lookup"><span data-stu-id="3978b-163">Create a *Models* folder.</span></span> <span data-ttu-id="3978b-164">В *моделей* папки, создайте файл класса с именем *Student.cs* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3978b-164">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="3978b-165">`ID` Свойство становится столбец первичного ключа таблицы базы данных (DB), соответствующий этому классу.</span><span class="sxs-lookup"><span data-stu-id="3978b-165">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="3978b-166">По умолчанию основные EF интерпретирует свойство, которое называется `ID` или `classnameID` как первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="3978b-166">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="3978b-167">`Enrollments` Свойство является свойством навигации.</span><span class="sxs-lookup"><span data-stu-id="3978b-167">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="3978b-168">Свойства ссылки навигации к другим сущностям, которые относятся к этой сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-168">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="3978b-169">В этом случае `Enrollments` свойство `Student entity` хранит все `Enrollment` сущностей, которые относятся к, `Student`.</span><span class="sxs-lookup"><span data-stu-id="3978b-169">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="3978b-170">Например, если строка студента в базе данных имеет две связанные строки регистрации `Enrollments` свойства навигации содержит этих двух `Enrollment` сущностей.</span><span class="sxs-lookup"><span data-stu-id="3978b-170">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="3978b-171">Связанный с ним `Enrollment` строка является строкой, содержащей этого студента значение первичного ключа в `StudentID` столбца.</span><span class="sxs-lookup"><span data-stu-id="3978b-171">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="3978b-172">Например, предположим, что студента с Идентификатором = 1 имеет две строки `Enrollment` таблицы.</span><span class="sxs-lookup"><span data-stu-id="3978b-172">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="3978b-173">`Enrollment` Таблица содержит две строки с `StudentID` = 1.</span><span class="sxs-lookup"><span data-stu-id="3978b-173">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="3978b-174">`StudentID`является внешним ключом в `Enrollment` , указывающее студента в таблицу `Student` таблицы.</span><span class="sxs-lookup"><span data-stu-id="3978b-174">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="3978b-175">Если свойство навигации может содержать несколько сущностей, свойства навигации должен быть тип списка, например `ICollection<T>`.</span><span class="sxs-lookup"><span data-stu-id="3978b-175">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="3978b-176">`ICollection<T>`можно указать, или тип, такой как `List<T>` или `HashSet<T>`.</span><span class="sxs-lookup"><span data-stu-id="3978b-176">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="3978b-177">Когда `ICollection<T>` —, EF Core создает `HashSet<T>` коллекции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3978b-177">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="3978b-178">Свойства навигации, которые содержат несколько сущностей исходят от отношений "многие ко многим" и один ко многим.</span><span class="sxs-lookup"><span data-stu-id="3978b-178">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="3978b-179">Сущность регистрации</span><span class="sxs-lookup"><span data-stu-id="3978b-179">The Enrollment entity</span></span>

![Схема entity регистрации](intro/_static/enrollment-entity.png)

<span data-ttu-id="3978b-181">В *моделей* папке создайте *«Enrollment.cs» в качестве* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3978b-181">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="3978b-182">`EnrollmentID` Свойство является первичным ключом.</span><span class="sxs-lookup"><span data-stu-id="3978b-182">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="3978b-183">Использует эту сущность `classnameID` шаблона вместо `ID` как `Student` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-183">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="3978b-184">Обычно разработчики выбрать один шаблон и использовать его во всей модели данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-184">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="3978b-185">В этом руководстве с помощью идентификатора без classname отображается для упрощения реализации наследования в модели данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-185">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="3978b-186">`Grade` Свойство `enum`.</span><span class="sxs-lookup"><span data-stu-id="3978b-186">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="3978b-187">Знак вопроса после `Grade` объявление типа указывает, что `Grade` свойство имеет значение NULL.</span><span class="sxs-lookup"><span data-stu-id="3978b-187">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="3978b-188">Степень, которую имеет значение null отличается от нуля оценку — значение null означает оценку не известен или еще не назначена.</span><span class="sxs-lookup"><span data-stu-id="3978b-188">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="3978b-189">`StudentID` Свойство внешнего ключа, и соответствующее свойство навигации `Student`.</span><span class="sxs-lookup"><span data-stu-id="3978b-189">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="3978b-190">`Enrollment` Сущности связан с одним `Student` сущности, поэтому свойство содержит один `Student` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-190">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="3978b-191">`Student` Сущности отличается от `Student.Enrollments` свойство навигации, которое содержит несколько `Enrollment` сущностей.</span><span class="sxs-lookup"><span data-stu-id="3978b-191">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="3978b-192">`CourseID` Свойство внешнего ключа, и соответствующее свойство навигации `Course`.</span><span class="sxs-lookup"><span data-stu-id="3978b-192">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="3978b-193">`Enrollment` Сущности связан с одним `Course` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-193">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="3978b-194">EF Core интерпретирует свойство как внешний ключ, если он имеет имя `<navigation property name><primary key property name>`.</span><span class="sxs-lookup"><span data-stu-id="3978b-194">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="3978b-195">Например`StudentID` для `Student` свойство навигации, поскольку `Student` первичного ключа сущности является `ID`.</span><span class="sxs-lookup"><span data-stu-id="3978b-195">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="3978b-196">Свойства внешнего ключа может также называться `<primary key property name>`.</span><span class="sxs-lookup"><span data-stu-id="3978b-196">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="3978b-197">Например `CourseID` с момента `Course` первичного ключа сущности является `CourseID`.</span><span class="sxs-lookup"><span data-stu-id="3978b-197">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="3978b-198">Сущность курса</span><span class="sxs-lookup"><span data-stu-id="3978b-198">The Course entity</span></span>

![Схема entity курса](intro/_static/course-entity.png)

<span data-ttu-id="3978b-200">В *моделей* папке создайте *Course.cs* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3978b-200">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="3978b-201">`Enrollments` Свойство является свойством навигации.</span><span class="sxs-lookup"><span data-stu-id="3978b-201">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="3978b-202">Объект `Course` сущности могут быть связаны с любым количеством `Enrollment` сущностей.</span><span class="sxs-lookup"><span data-stu-id="3978b-202">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="3978b-203">`DatabaseGenerated` Атрибут позволяет приложению указать первичный ключ, а не наличие базы данных он сформирован.</span><span class="sxs-lookup"><span data-stu-id="3978b-203">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="3978b-204">Создать контекст базы данных SchoolContext</span><span class="sxs-lookup"><span data-stu-id="3978b-204">Create the SchoolContext DB context</span></span>

<span data-ttu-id="3978b-205">Основной класс, который координирует EF основные функциональные возможности для заданной модели данных — класс контекста базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-205">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="3978b-206">Контекст данных является производным от `Microsoft.EntityFrameworkCore.DbContext`.</span><span class="sxs-lookup"><span data-stu-id="3978b-206">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="3978b-207">Контекст данных указывает, какие сущности включаются в модель данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-207">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="3978b-208">В этом проекте класс с именем `SchoolContext`.</span><span class="sxs-lookup"><span data-stu-id="3978b-208">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="3978b-209">В папку проекта, создайте папку с именем *данные*.</span><span class="sxs-lookup"><span data-stu-id="3978b-209">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="3978b-210">В *данные* создания папок *SchoolContext.cs* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3978b-210">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="3978b-211">Этот код создает `DbSet` свойство для каждого набора сущностей.</span><span class="sxs-lookup"><span data-stu-id="3978b-211">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="3978b-212">В терминологии EF основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3978b-212">In EF Core terminology:</span></span>

* <span data-ttu-id="3978b-213">Обычно набор сущностей соответствует таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-213">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="3978b-214">Сущность соответствует строке таблицы.</span><span class="sxs-lookup"><span data-stu-id="3978b-214">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="3978b-215">`DbSet<Enrollment>`и `DbSet<Course>` можно опустить.</span><span class="sxs-lookup"><span data-stu-id="3978b-215">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="3978b-216">EF ядро включает их неявно поскольку `Student` ссылки на сущности `Enrollment` сущности и `Enrollment` ссылки на сущности `Course` сущности.</span><span class="sxs-lookup"><span data-stu-id="3978b-216">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="3978b-217">Для этого учебника оставьте `DbSet<Enrollment>` и `DbSet<Course>` в `SchoolContext`.</span><span class="sxs-lookup"><span data-stu-id="3978b-217">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="3978b-218">При создании базы данных основной EF создает таблицы, которые имеют имена, то же, что `DbSet` имена свойств.</span><span class="sxs-lookup"><span data-stu-id="3978b-218">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="3978b-219">Имена свойств для коллекций, обычно во множественном числе (учащихся вместо студента).</span><span class="sxs-lookup"><span data-stu-id="3978b-219">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="3978b-220">Разработчики используют различные ли имена таблиц должны быть во множественном числе.</span><span class="sxs-lookup"><span data-stu-id="3978b-220">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="3978b-221">Для этих учебников по умолчанию переопределяется путем указания имен таблиц в единственном числе в класс DbContext.</span><span class="sxs-lookup"><span data-stu-id="3978b-221">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="3978b-222">Чтобы указать имена таблиц в единственном числе, добавьте следующий выделенный код:</span><span class="sxs-lookup"><span data-stu-id="3978b-222">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="3978b-223">Регистрация контекста с помощью внедрения зависимости</span><span class="sxs-lookup"><span data-stu-id="3978b-223">Register the context with dependency injection</span></span>

<span data-ttu-id="3978b-224">Включает ASP.NET Core [внедрения зависимостей](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="3978b-224">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="3978b-225">Службы (такие как контекста данных Entity FRAMEWORK Core) регистрируются с помощью внедрения зависимости во время запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="3978b-225">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="3978b-226">Компоненты, которые требуют этих служб (например, страниц Razor) предоставляются этим службам через параметры конструктора.</span><span class="sxs-lookup"><span data-stu-id="3978b-226">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="3978b-227">Далее в этом учебнике показан конструктор код, который возвращает экземпляр контекста базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-227">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="3978b-228">Чтобы зарегистрировать `SchoolContext` как служба, откройте *файла Startup.cs*и добавьте выделенные строки к `ConfigureServices` метод.</span><span class="sxs-lookup"><span data-stu-id="3978b-228">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="3978b-229">Имя строки подключения передается в контекст путем вызова метода на `DbContextOptionsBuilder` объекта.</span><span class="sxs-lookup"><span data-stu-id="3978b-229">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="3978b-230">Для локальной разработки [система конфигурации ASP.NET Core](xref:fundamentals/configuration/index) считывает строку подключения из *appsettings.json* файла.</span><span class="sxs-lookup"><span data-stu-id="3978b-230">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="3978b-231">Добавить `using` инструкции для `ContosoUniversity.Data` и `Microsoft.EntityFrameworkCore` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="3978b-231">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="3978b-232">Выполните построение проекта.</span><span class="sxs-lookup"><span data-stu-id="3978b-232">Build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="3978b-233">Откройте *appsettings.json* и добавьте строку подключения, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="3978b-233">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="3978b-234">Предыдущий строка соединения использует `ConnectRetryCount=0` для предотвращения [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) прекратит.</span><span class="sxs-lookup"><span data-stu-id="3978b-234">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="3978b-235">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="3978b-235">SQL Server Express LocalDB</span></span>

<span data-ttu-id="3978b-236">В строке соединения указывается база данных LocalDB SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3978b-236">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="3978b-237">LocalDB — это облегченная версия SQL Server Express Database Engine и предназначен для разработки приложений, а не использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3978b-237">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="3978b-238">LocalDB запускается по требованию в пользовательском режиме, поэтому настройки не слишком сложны.</span><span class="sxs-lookup"><span data-stu-id="3978b-238">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="3978b-239">По умолчанию создает LocalDB *.mdf* DB файлы в `C:/Users/<user>` каталога.</span><span class="sxs-lookup"><span data-stu-id="3978b-239">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="3978b-240">Добавьте код для инициализации базы данных с тестовыми данными</span><span class="sxs-lookup"><span data-stu-id="3978b-240">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="3978b-241">EF Core создает пустой базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-241">EF Core creates an empty DB.</span></span> <span data-ttu-id="3978b-242">В этом разделе *начальное значение* метод создается его заполнение тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-242">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="3978b-243">В *данные* папки, создайте новый файл класса с именем *DbInitializer.cs* и добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="3978b-243">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="3978b-244">Код проверяет наличие любого студентов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-244">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="3978b-245">Если в базе данных нет учащихся, базы данных запускается с тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="3978b-245">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="3978b-246">Он загружает тестовых данных в массивы вместо `List<T>` коллекций для оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="3978b-246">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="3978b-247">`EnsureCreated` Метод автоматически создает базу данных для контекста базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-247">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="3978b-248">Если существует база данных, `EnsureCreated` возвращает без изменения базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-248">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="3978b-249">В *Program.cs*, изменить `Main` метод делать следующее:</span><span class="sxs-lookup"><span data-stu-id="3978b-249">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="3978b-250">Получите экземпляр контекста DB контейнер внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3978b-250">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="3978b-251">Вызовите метод инициализации, передав ему контекст.</span><span class="sxs-lookup"><span data-stu-id="3978b-251">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="3978b-252">Dispose контекст при завершении метода начальное значение.</span><span class="sxs-lookup"><span data-stu-id="3978b-252">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="3978b-253">В следующем коде показано обновленное *Program.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="3978b-253">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="3978b-254">При первом запуске приложения создается и заполняется тестовыми данными базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-254">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="3978b-255">При обновлении модели данных:</span><span class="sxs-lookup"><span data-stu-id="3978b-255">When the data model is updated:</span></span>
* <span data-ttu-id="3978b-256">Удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-256">Delete the DB.</span></span>
* <span data-ttu-id="3978b-257">Обновите метод начальное значение.</span><span class="sxs-lookup"><span data-stu-id="3978b-257">Update the seed method.</span></span>
* <span data-ttu-id="3978b-258">Запустите приложение и создать новые базы данных для задания начальных значений.</span><span class="sxs-lookup"><span data-stu-id="3978b-258">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="3978b-259">На следующих занятиях рассматривается базы данных обновляется при изменений, без удаления и повторного создания базы данных в модели данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-259">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="3978b-260">Добавление средств формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="3978b-260">Add scaffold tooling</span></span>

<span data-ttu-id="3978b-261">В этом разделе консоли диспетчера пакетов (PMC) используется для добавления кода создания Visual Studio веб-пакета.</span><span class="sxs-lookup"><span data-stu-id="3978b-261">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="3978b-262">Этот пакет необходим для работы ядра формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="3978b-262">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="3978b-263">В меню **Сервис** последовательно выберите пункты **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3978b-263">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="3978b-264">В пакет Диспетчер консоли (PMC), введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3978b-264">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="3978b-265">Предыдущая команда добавляет в файл *.csproj пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="3978b-265">The previous command adds the NuGet packages to the *.csproj file:</span></span>

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="3978b-266">Формировать модели</span><span class="sxs-lookup"><span data-stu-id="3978b-266">Scaffold the model</span></span>

* <span data-ttu-id="3978b-267">Откройте окно командной строки в папке проекта (папке, где находятся файлы *Program.cs*, *Startup.cs* и *.csproj* файлов).</span><span class="sxs-lookup"><span data-stu-id="3978b-267">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="3978b-268">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3978b-268">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
<span data-ttu-id="3978b-269">Если создается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="3978b-269">If the following error is generated:</span></span>

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

<span data-ttu-id="3978b-270">Выполните команду еще раз и оставьте комментарий в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3978b-270">Run the command again and leave a comment at the bottom of the page.</span></span>

<span data-ttu-id="3978b-271">Если возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="3978b-271">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="3978b-272">Откройте окно командной строки в папке проекта (папке, где находятся файлы *Program.cs*, *Startup.cs* и *.csproj* файлов).</span><span class="sxs-lookup"><span data-stu-id="3978b-272">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>


<span data-ttu-id="3978b-273">Выполните построение проекта.</span><span class="sxs-lookup"><span data-stu-id="3978b-273">Build the project.</span></span> <span data-ttu-id="3978b-274">Сборки приводит к возникновению ошибки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3978b-274">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="3978b-275">Глобальная замена `_context.Student` для `_context.Students` (то есть, добавить «s» `Student`).</span><span class="sxs-lookup"><span data-stu-id="3978b-275">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="3978b-276">7 вхождений обнаружены и обновлены.</span><span class="sxs-lookup"><span data-stu-id="3978b-276">7 occurrences are found and updated.</span></span> <span data-ttu-id="3978b-277">Мы надеемся, что исправление [этой ошибки](https://github.com/aspnet/Scaffolding/issues/633) в следующем выпуске.</span><span class="sxs-lookup"><span data-stu-id="3978b-277">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="3978b-278">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="3978b-278">Test the app</span></span>

<span data-ttu-id="3978b-279">Запустите приложение и выберите **учащихся** ссылку.</span><span class="sxs-lookup"><span data-stu-id="3978b-279">Run the app and select the **Students** link.</span></span> <span data-ttu-id="3978b-280">В зависимости от ширины обозревателя **учащихся** ссылка появляется в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3978b-280">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="3978b-281">Если **учащихся** ссылка не отображается, щелкните значок навигации в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="3978b-281">If the **Students** link is not visible, click the navigation icon in the upper right corner.</span></span>

![Домашняя страница Contoso университета узкий](intro/_static/home-page-narrow.png)

<span data-ttu-id="3978b-283">Тест **создать**, **изменить**, и **сведения** ссылки.</span><span class="sxs-lookup"><span data-stu-id="3978b-283">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="3978b-284">Представление базы данных</span><span class="sxs-lookup"><span data-stu-id="3978b-284">View the DB</span></span>

<span data-ttu-id="3978b-285">При запуске приложения, `DbInitializer.Initialize` вызовов `EnsureCreated`.</span><span class="sxs-lookup"><span data-stu-id="3978b-285">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="3978b-286">`EnsureCreated`Определяет, существует ли базы данных и при необходимости создает один.</span><span class="sxs-lookup"><span data-stu-id="3978b-286">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="3978b-287">Если в базе данных нет учащихся `Initialize` метод добавляет учащихся.</span><span class="sxs-lookup"><span data-stu-id="3978b-287">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="3978b-288">Откройте **обозреватель объектов SQL Server** (SSOX) из **представление** меню в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3978b-288">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="3978b-289">В SSOX, щелкните **(localdb) \MSSQLLocalDB > базы данных > ContosoUniversity1**.</span><span class="sxs-lookup"><span data-stu-id="3978b-289">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="3978b-290">Разверните **таблиц** узла.</span><span class="sxs-lookup"><span data-stu-id="3978b-290">Expand the **Tables** node.</span></span>

<span data-ttu-id="3978b-291">Щелкните правой кнопкой мыши **студента** и нажмите кнопку **данные представления** создания столбцов и строк, вставляемых в таблицу.</span><span class="sxs-lookup"><span data-stu-id="3978b-291">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="3978b-292">*.Mdf* и *.ldf* файлы базы данных находятся в *C:\Users\\ <yourusername>*  папки.</span><span class="sxs-lookup"><span data-stu-id="3978b-292">The *.mdf* and *.ldf* DB files are in the *C:\Users\\<yourusername>* folder.</span></span>

<span data-ttu-id="3978b-293">`EnsureCreated`вызывается при запуске приложения, что позволяет следующий рабочий процесс:</span><span class="sxs-lookup"><span data-stu-id="3978b-293">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="3978b-294">Удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-294">Delete the DB.</span></span>
* <span data-ttu-id="3978b-295">Изменения схемы базы данных (например, добавить `EmailAddress` поля).</span><span class="sxs-lookup"><span data-stu-id="3978b-295">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="3978b-296">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="3978b-296">Run the app.</span></span>

<span data-ttu-id="3978b-297">`EnsureCreated`Создает базы данных с`EmailAddress` столбца.</span><span class="sxs-lookup"><span data-stu-id="3978b-297">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="3978b-298">Соглашения</span><span class="sxs-lookup"><span data-stu-id="3978b-298">Conventions</span></span>

<span data-ttu-id="3978b-299">Объем кода, написанного в порядке для основных компонентов EF Создание завершения DB сводится к минимуму из-за использования соглашения или предположения, что делает EF Core.</span><span class="sxs-lookup"><span data-stu-id="3978b-299">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="3978b-300">Имена `DbSet` свойства используются в качестве имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="3978b-300">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="3978b-301">Для сущностей, не ссылается `DbSet` свойство класса сущности, имена используются в качестве имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="3978b-301">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="3978b-302">Имена свойств сущности используются для имен столбцов.</span><span class="sxs-lookup"><span data-stu-id="3978b-302">Entity property names are used for column names.</span></span>

* <span data-ttu-id="3978b-303">Свойства сущности, которые называются Идентификатором или classnameID распознаются как свойства основного ключа.</span><span class="sxs-lookup"><span data-stu-id="3978b-303">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="3978b-304">Свойство интерпретируется как свойство внешнего ключа, если он называется  *<navigation property name> <primary key property name>*  (например, `StudentID` для `Student` свойство навигации с момента `Student` — первичный ключ сущности `ID`).</span><span class="sxs-lookup"><span data-stu-id="3978b-304">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="3978b-305">Свойства внешнего ключа, можно назвать  *<primary key property name>*  (например, `EnrollmentID` с момента `Enrollment` первичного ключа сущности является `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="3978b-305">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="3978b-306">Можно переопределить обычным образом.</span><span class="sxs-lookup"><span data-stu-id="3978b-306">Conventional behavior can be overridden.</span></span> <span data-ttu-id="3978b-307">Например имена таблиц можно явно указать, как показано выше в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3978b-307">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="3978b-308">Можно явно задать имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="3978b-308">The column names can be explicitly set.</span></span> <span data-ttu-id="3978b-309">Первичные и внешние ключи могут задаваться явным образом.</span><span class="sxs-lookup"><span data-stu-id="3978b-309">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="3978b-310">Асинхронный код</span><span class="sxs-lookup"><span data-stu-id="3978b-310">Asynchronous code</span></span>

<span data-ttu-id="3978b-311">Асинхронное программирование является режимом по умолчанию для ASP.NET Core и EF Core.</span><span class="sxs-lookup"><span data-stu-id="3978b-311">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="3978b-312">Ограниченное число потоков, доступных на веб-сервере, и в случае высокой загрузки все доступные потоки быть используется.</span><span class="sxs-lookup"><span data-stu-id="3978b-312">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="3978b-313">В этом случае сервер может обработать новые запросы, пока не освободятся потоков.</span><span class="sxs-lookup"><span data-stu-id="3978b-313">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="3978b-314">С синхронным кодом большое количество потоков может блокировали они не выполняя фактически действия из-за ожидания завершения ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="3978b-314">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="3978b-315">Асинхронный код когда процесс ожидает ввода-вывода завершить, свой поток освобождается для сервера, используемые для обработки других запросов.</span><span class="sxs-lookup"><span data-stu-id="3978b-315">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="3978b-316">В результате асинхронного кода обеспечивает более эффективное использование ресурсов сервера и что сервер включен для обработки большего объема трафика без задержек.</span><span class="sxs-lookup"><span data-stu-id="3978b-316">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="3978b-317">Во время выполнения асинхронного кода вызвать небольшого количества временных затрат.</span><span class="sxs-lookup"><span data-stu-id="3978b-317">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="3978b-318">В ситуациях, сниженным трафиком снижение производительности незначительно, при в ситуациях с высоким трафиком, является существенным потенциальное улучшение производительности.</span><span class="sxs-lookup"><span data-stu-id="3978b-318">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="3978b-319">В следующем коде `async` ключевое слово, `Task<T>` возвращаемое значение, `await` ключевое слово, и `ToListAsync` метод делает код более асинхронного выполнения.</span><span class="sxs-lookup"><span data-stu-id="3978b-319">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="3978b-320">`async` Ключевое слово указывает компилятору:</span><span class="sxs-lookup"><span data-stu-id="3978b-320">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="3978b-321">Создает обратные вызовы для части тела метода.</span><span class="sxs-lookup"><span data-stu-id="3978b-321">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="3978b-322">Автоматически создавать [задачи](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) возвращаемый объект.</span><span class="sxs-lookup"><span data-stu-id="3978b-322">Automatically create the [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that is returned.</span></span> <span data-ttu-id="3978b-323">Дополнительные сведения см. в разделе [тип возвращаемого значения задачи](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span><span class="sxs-lookup"><span data-stu-id="3978b-323">For more information, see [Task Return Type](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="3978b-324">Тип возвращаемого значения неявный `Task` представляет выполняющуюся работу.</span><span class="sxs-lookup"><span data-stu-id="3978b-324">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="3978b-325">`await` Ключевое слово указывает компилятору на необходимость разделить на две части метода.</span><span class="sxs-lookup"><span data-stu-id="3978b-325">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="3978b-326">Первая часть завершается с операцией, которая запускается в асинхронном режиме.</span><span class="sxs-lookup"><span data-stu-id="3978b-326">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="3978b-327">Вторая часть переводится в метод обратного вызова, вызываемый после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="3978b-327">The second part is put into a callback method that is called when the operation completes.</span></span>

* <span data-ttu-id="3978b-328">`ToListAsync`асинхронная версия `ToList` метода расширения.</span><span class="sxs-lookup"><span data-stu-id="3978b-328">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="3978b-329">Некоторые аспекты, которые следует учитывать при написании асинхронного кода, использующего EF ядра:</span><span class="sxs-lookup"><span data-stu-id="3978b-329">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="3978b-330">Только инструкции, вызывающие запросов или команд, отправляемых в базе данных выполняются асинхронно.</span><span class="sxs-lookup"><span data-stu-id="3978b-330">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="3978b-331">Содержащий, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, и `SaveChangesAsync`.</span><span class="sxs-lookup"><span data-stu-id="3978b-331">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="3978b-332">Сюда не входят инструкции, которые просто изменить `IQueryable`, такие как `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span><span class="sxs-lookup"><span data-stu-id="3978b-332">It does not include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="3978b-333">EF контекста не является однопоточным безопасный: не пытайтесь выполнить несколько операций параллельно.</span><span class="sxs-lookup"><span data-stu-id="3978b-333">An EF Core context is not threaded safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="3978b-334">Чтобы воспользоваться преимуществами повышение производительности для асинхронного кода, убедитесь, что библиотека пакетов (например, для разбиения на страницы) используют async вызывающие EF основные методы, которые отправляют запросы к базе данных.</span><span class="sxs-lookup"><span data-stu-id="3978b-334">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="3978b-335">Дополнительные сведения об асинхронном программировании в .NET см. в разделе [Обзор Async](https://docs.microsoft.com/dotnet/articles/standard/async).</span><span class="sxs-lookup"><span data-stu-id="3978b-335">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="3978b-336">В следующем уроке основные CRUD (Создание, чтение, обновление и удаление) операции проверяются.</span><span class="sxs-lookup"><span data-stu-id="3978b-336">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="3978b-337">Вперед</span><span class="sxs-lookup"><span data-stu-id="3978b-337">Next</span></span>](xref:data/ef-rp/crud)