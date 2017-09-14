---
title: "Добавление модели в приложение ASP.NET Core MVC"
author: rick-anderson
description: "Добавление модели в простое приложение ASP.NET Core."
keywords: "ASP.NET Core, MVC, шаблоны, формирование шаблонов"
ms.author: riande
manager: wpickett
ms.date: 03/30/2017
ms.topic: get-started-article
ms.assetid: 8dc28498-eeee-1638-b903-b593059e9f39
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/adding-model
ms.openlocfilehash: 4a158802a19011cbb45da1b3ca43d67706efe4cd
ms.sourcegitcommit: d9e2c99c837078fcac0e315025f8fbfbd45ea6e8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model1.md)]

* <span data-ttu-id="4a8bf-104">Щелкните папку *Models* правой кнопкой мыши и выберите пункт **Добавить** > **Новый файл**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-104">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span> 
* <span data-ttu-id="4a8bf-105">В диалоговом окне **Новый файл** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-105">In the **New File** dialog:</span></span>

  * <span data-ttu-id="4a8bf-106">Выберите на левой панели пункт **Общие**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-106">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="4a8bf-107">Выберите в центральной области **Пустой класс**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-107">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="4a8bf-108">Назовите класс **Movie** и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-108">Name the class **Movie** and select **New**.</span></span>

<span data-ttu-id="4a8bf-109">Добавьте в класс `Movie` следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="4a8bf-109">Add the following properties to the `Movie` class:</span></span>

<span data-ttu-id="4a8bf-110">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]</span><span class="sxs-lookup"><span data-stu-id="4a8bf-110">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]</span></span>

<span data-ttu-id="4a8bf-111">Поле `ID` является обязательным для первичного ключа базы данных.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-111">The `ID` field is required by the database for the primary key.</span></span>

<span data-ttu-id="4a8bf-112">Выполните сборку проекта, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-112">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="4a8bf-113">Теперь в вашем приложении **M**VC есть **M**одель.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-113">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="prepare-the-project-for-scaffolding"></a><span data-ttu-id="4a8bf-114">Подготовка проекта для формирования шаблонов</span><span class="sxs-lookup"><span data-stu-id="4a8bf-114">Prepare the project for scaffolding</span></span>

- <span data-ttu-id="4a8bf-115">Щелкните файл проекта правой кнопкой мыши и последовательно выберите параметры **Сервис > Изменить файл**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-115">Right click on the project file, and then select **Tools > Edit File**.</span></span>

  ![представление указанного выше шага](adding-model/_static/1.png)

- <span data-ttu-id="4a8bf-117">Добавьте в файл *MvcMovie.csproj* следующие выделенные пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="4a8bf-117">Add the following highlighted NuGet packages to the *MvcMovie.csproj* file:</span></span>
             
  <span data-ttu-id="4a8bf-118">[!code-csharp[Main](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]</span><span class="sxs-lookup"><span data-stu-id="4a8bf-118">[!code-csharp[Main](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]</span></span>

- <span data-ttu-id="4a8bf-119">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-119">Save the file.</span></span>

- <span data-ttu-id="4a8bf-120">Создайте файл *Models/MvcMovieContext.cs* и добавьте следующий класс `MvcMovieContext`: [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span><span class="sxs-lookup"><span data-stu-id="4a8bf-120">Create a *Models/MvcMovieContext.cs* file and add the following `MvcMovieContext` class:  [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span></span>
   
- <span data-ttu-id="4a8bf-121">Откройте файл *Startup.cs* и добавьте два использования: [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span><span class="sxs-lookup"><span data-stu-id="4a8bf-121">Open the *Startup.cs* file and add two usings:  [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span></span>

- <span data-ttu-id="4a8bf-122">Добавьте контекст базы данных в файл *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="4a8bf-122">Add the database context to the *Startup.cs* file:</span></span>

   <span data-ttu-id="4a8bf-123">[!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]</span><span class="sxs-lookup"><span data-stu-id="4a8bf-123">[!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]</span></span>

  <span data-ttu-id="4a8bf-124">За счет этого Entity Framework будет знать, какие классы модели входят в модель данных.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-124">This tells Entity Framework which model classes are included in the data model.</span></span> <span data-ttu-id="4a8bf-125">Вы определяете один *набор сущностей* объектов Movie, который будут представлен в базу данных как таблица Movie.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-125">You're defining one *entity set* of Movie objects, which will be represented in the database as a Movie table.</span></span>

- <span data-ttu-id="4a8bf-126">Выполните сборку проекта, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-126">Build the project to verify there are no errors.</span></span>

## <a name="scaffold-the-moviecontroller"></a><span data-ttu-id="4a8bf-127">Формирование шаблонов для MovieController</span><span class="sxs-lookup"><span data-stu-id="4a8bf-127">Scaffold the MovieController</span></span>

<span data-ttu-id="4a8bf-128">Откройте окно терминала в папке проекта и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-128">Open a terminal window in the project folder and run the following commands:</span></span>

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
<span data-ttu-id="4a8bf-129">Если возникает ошибка `No executable found matching command "dotnet-aspnet-codegenerator", verify`.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-129">If you get the error `No executable found matching command "dotnet-aspnet-codegenerator", verify`:</span></span>

 * <span data-ttu-id="4a8bf-130">Вы находитесь в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-130">You are in the project directory.</span></span> <span data-ttu-id="4a8bf-131">В папке проекта имеются файлы *Program.cs*, *Startup.cs* и *.csproj*.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-131">The project directory has the *Program.cs*, *Startup.cs* and *.csproj* files.</span></span>
 * <span data-ttu-id="4a8bf-132">Ваша версия — 1.1 или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-132">Your dotnet version is 1.1 or higher.</span></span> <span data-ttu-id="4a8bf-133">Запустите `dotnet`, чтобы узнать версию.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-133">Run `dotnet` to get the version.</span></span>
 * <span data-ttu-id="4a8bf-134">Вы добавили элемент `<DotNetCliToolReference>` в [файл MvcMovie.csproj](#prepare-the-project-for-scaffolding).</span><span class="sxs-lookup"><span data-stu-id="4a8bf-134">You have added the `<DotNetCliToolReference>` elment to the [MvcMovie.csproj file](#prepare-the-project-for-scaffolding).</span></span>
 
<!--
> [!NOTE]
> If you get an error when the scaffolding command runs, see [issue 444 in the scaffolding repository](https://github.com/aspnet/scaffolding/issues/444) for a workaround.
-->

<span data-ttu-id="4a8bf-135">Ядро формирование шаблонов создает следующее.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-135">The scaffolding engine creates the following:</span></span>

* <span data-ttu-id="4a8bf-136">Контроллер фильмов (*Controllers/MoviesController.cs*)</span><span class="sxs-lookup"><span data-stu-id="4a8bf-136">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="4a8bf-137">Файлы представления Razor для страниц Create, Delete, Edit и Index (*Views/Movies/\*.cshtml*)</span><span class="sxs-lookup"><span data-stu-id="4a8bf-137">Razor view files for Create, Delete, Details, Edit and Index pages (*Views/Movies/\*.cshtml*)</span></span>

<span data-ttu-id="4a8bf-138">Автоматическое создание методов и представлений действия [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (создание, чтение, обновление и удаление) называется *формированием шаблонов*.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-138">The automatic creation of [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="4a8bf-139">Вскоре вы получите полнофункциональное веб-приложение, позволяющее управлять базой данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-139">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

### <a name="add-the-files-to-visual-studio"></a><span data-ttu-id="4a8bf-140">Добавление файлов в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a8bf-140">Add the files to Visual Studio</span></span>

* <span data-ttu-id="4a8bf-141">Добавьте файл *MovieController.cs* в проект Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-141">Add the *MovieController.cs* file to the Visual Studio project:</span></span>

  * <span data-ttu-id="4a8bf-142">Щелкните папку *Controllers* правой кнопкой мыши и выберите пункт **Добавить > Добавить файлы**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-142">Right-click on the *Controllers* folder and select **Add > Add Files**.</span></span>
  * <span data-ttu-id="4a8bf-143">Выберите файл *MovieController.cs*.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-143">Select the *MovieController.cs* file.</span></span>

* <span data-ttu-id="4a8bf-144">Добавьте папку *Movies* и представления.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-144">Add the *Movies* folder and views:</span></span>

  * <span data-ttu-id="4a8bf-145">Щелкните папку *Views* правой кнопкой мыши и выберите пункт **Добавить > Добавить существующую папку**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-145">Right-click on the *Views* folder and select **Add > Add Existing Folder**.</span></span>
  * <span data-ttu-id="4a8bf-146">Перейдите к папку *Views*, выберите *Views\Movies* и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-146">Navigate to the *Views* folder, select *Views\Movies*, and then select **Open**.</span></span>
  * <span data-ttu-id="4a8bf-147">В диалоговом окне **Выберите файлы для добавления из папки Movies** выберите вариант **Включить все** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-147">In the **Select files to add from Movies** dialog, select **Include All**, and then **OK**.</span></span>

[!INCLUDE[adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model3.md)]

<span data-ttu-id="4a8bf-148">Теперь у вас есть база данных и страницы для отображения, редактирования, обновления и удаления данных.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-148">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="4a8bf-149">В следующем руководстве мы будем работать с базой данных.</span><span class="sxs-lookup"><span data-stu-id="4a8bf-149">In the next tutorial, we'll work with the database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a8bf-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4a8bf-150">Additional resources</span></span>

* [<span data-ttu-id="4a8bf-151">Вспомогательные функции тегов</span><span class="sxs-lookup"><span data-stu-id="4a8bf-151">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="4a8bf-152">Глобализация и локализация</span><span class="sxs-lookup"><span data-stu-id="4a8bf-152">Globalization and localization</span></span>](xref:fundamentals/localization)

>[!div class="step-by-step"]
<span data-ttu-id="4a8bf-153">[Назад: Добавление представления](adding-view.md)
[Далее: Работа с SQL](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="4a8bf-153">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  