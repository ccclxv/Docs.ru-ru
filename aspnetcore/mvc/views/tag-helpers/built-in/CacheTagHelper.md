---
title: "Кэшировать вспомогательный тег в ядре ASP.NET MVC"
author: pkellner
description: "Показано, как работать с вспомогательный тег кэша"
keywords: "ASP.NET Core, вспомогательная функция тегов"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: c045d485-d1dc-4cea-a675-46be83b7a012
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/CacheTagHelper
ms.openlocfilehash: 31c362a70e44c7178efe1c35b28a02fd712ac2b4
ms.sourcegitcommit: 74a8ad9c1ba5c155d7c4303e67632a0922c38e86
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/20/2017
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="fc6d5-104">Кэшировать вспомогательный тег в ядре ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fc6d5-104">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="fc6d5-105">Автор: [Питер Кельнер (Peter Kellner)](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="fc6d5-105">By [Peter Kellner](http://peterkellner.net)</span></span> 


<span data-ttu-id="fc6d5-106">Вспомогательный тег кэша позволяет существенно повысить производительность приложения ASP.NET Core путем кэширования ее содержимое, чтобы внутренний поставщик кэша ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-106">The  Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="fc6d5-107">Значение по умолчанию задает представлений Razor `expires-after` до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-107">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="fc6d5-108">Приведенная ниже разметка Razor кэширует даты и времени:</span><span class="sxs-lookup"><span data-stu-id="fc6d5-108">The following Razor markup caches the date/time:</span></span>

```cshtml
<Cache>@DateTime.Now<Cache>
```

<span data-ttu-id="fc6d5-109">Первый запрос страницы, содержащей `CacheTagHelper` отобразит текущее значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-109">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="fc6d5-110">Дополнительные запросы покажет кэшированное значение, до истечения срока действия (по умолчанию 20 минут) или исключен с нехваткой памяти в кэше.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-110">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="fc6d5-111">Можно задать длительность кэширования со следующими атрибутами:</span><span class="sxs-lookup"><span data-stu-id="fc6d5-111">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="fc6d5-112">Кэшировать вспомогательные атрибуты тега</span><span class="sxs-lookup"><span data-stu-id="fc6d5-112">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="fc6d5-113">enabled</span><span class="sxs-lookup"><span data-stu-id="fc6d5-113">enabled</span></span>    


| <span data-ttu-id="fc6d5-114">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-114">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-115">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="fc6d5-115">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="fc6d5-116">boolean</span><span class="sxs-lookup"><span data-stu-id="fc6d5-116">boolean</span></span>           | <span data-ttu-id="fc6d5-117">«true» (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="fc6d5-117">"true" (default)</span></span>  |
|                   | <span data-ttu-id="fc6d5-118">"false"</span><span class="sxs-lookup"><span data-stu-id="fc6d5-118">"false"</span></span>   |


<span data-ttu-id="fc6d5-119">Определяет, кэшируются ли содержимое, заключенное в тег вспомогательный объект кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-119">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="fc6d5-120">Значение по умолчанию — `true`.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-120">The default is `true`.</span></span>  <span data-ttu-id="fc6d5-121">Если значение `false` этого вспомогательного объекта тег кэша не будет действовать кэширования на выводимых данных.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-121">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="fc6d5-122">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-122">Example:</span></span>

```cshtml
<Cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="fc6d5-123">Срок действия истекает в</span><span class="sxs-lookup"><span data-stu-id="fc6d5-123">expires-on</span></span> 

| <span data-ttu-id="fc6d5-124">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-124">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-125">Пример значения</span><span class="sxs-lookup"><span data-stu-id="fc6d5-125">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="fc6d5-126">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fc6d5-126">DateTimeOffset</span></span>    | <span data-ttu-id="fc6d5-127">«@new DateTime(2025,1,29,17,02,0)»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-127">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="fc6d5-128">Задает абсолютный срок действия.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-128">Sets an absolute expiration date.</span></span> <span data-ttu-id="fc6d5-129">Следующий пример будет кэшировать содержимое тега вспомогательный объект кэша до 17:02:00 на 29 января 2025.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-129">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="fc6d5-130">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-130">Example:</span></span>

```cshtml
<Cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="fc6d5-131">После истечения срока действия</span><span class="sxs-lookup"><span data-stu-id="fc6d5-131">expires-after</span></span>

| <span data-ttu-id="fc6d5-132">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-132">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-133">Пример значения</span><span class="sxs-lookup"><span data-stu-id="fc6d5-133">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="fc6d5-134">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc6d5-134">TimeSpan</span></span>    | <span data-ttu-id="fc6d5-135">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="fc6d5-135">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="fc6d5-136">Задает интервал времени с момента первого запроса для кэширования содержимого.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-136">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="fc6d5-137">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-137">Example:</span></span>

```cshtml
<Cache expires-on="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="fc6d5-138">скользящий срок действия истекает</span><span class="sxs-lookup"><span data-stu-id="fc6d5-138">expires-sliding</span></span>

| <span data-ttu-id="fc6d5-139">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-139">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-140">Пример значения</span><span class="sxs-lookup"><span data-stu-id="fc6d5-140">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="fc6d5-141">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc6d5-141">TimeSpan</span></span>    | <span data-ttu-id="fc6d5-142">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="fc6d5-142">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="fc6d5-143">Задает время, следует удалить запись кэша, если оно не было обращений.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-143">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="fc6d5-144">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-144">Example:</span></span>

```cshtml
<Cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="fc6d5-145">различаются по заголовок</span><span class="sxs-lookup"><span data-stu-id="fc6d5-145">vary-by-header</span></span>

| <span data-ttu-id="fc6d5-146">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-146">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-147">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-147">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-148">Строка</span><span class="sxs-lookup"><span data-stu-id="fc6d5-148">String</span></span>            | <span data-ttu-id="fc6d5-149">«User-Agent»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-149">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="fc6d5-150">«User-Agent, content-encoding»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-150">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="fc6d5-151">Принимает значение одного заголовка или список разделенных запятыми значений заголовка, запускающих обновление кэша, при их изменения.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-151">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="fc6d5-152">Следующий пример отслеживает значение заголовка `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-152">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="fc6d5-153">Пример будет кэшировать содержимое для каждого разные `User-Agent` представлены на веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-153">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="fc6d5-154">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-154">Example:</span></span>

```cshtml
<Cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="fc6d5-155">различаются по запроса</span><span class="sxs-lookup"><span data-stu-id="fc6d5-155">vary-by-query</span></span>

| <span data-ttu-id="fc6d5-156">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-156">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-157">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-157">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-158">Строка</span><span class="sxs-lookup"><span data-stu-id="fc6d5-158">String</span></span>            | <span data-ttu-id="fc6d5-159">«Обеспечить»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-159">"Make"</span></span>                |
|                   | <span data-ttu-id="fc6d5-160">«Создание модели»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-160">"Make,Model"</span></span> |

<span data-ttu-id="fc6d5-161">Принимает значение одного заголовка или список разделенных запятыми значений заголовка, которые запускают обновления кэша, при изменении значения заголовка.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-161">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="fc6d5-162">Следующий пример просматривает значения `Make` и `Model`.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-162">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="fc6d5-163">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-163">Example:</span></span>

```cshtml
<Cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="fc6d5-164">различаются по Маршрутизация</span><span class="sxs-lookup"><span data-stu-id="fc6d5-164">vary-by-route</span></span>

| <span data-ttu-id="fc6d5-165">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-165">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-166">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-166">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-167">Строка</span><span class="sxs-lookup"><span data-stu-id="fc6d5-167">String</span></span>            | <span data-ttu-id="fc6d5-168">«Обеспечить»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-168">"Make"</span></span>                |
|                   | <span data-ttu-id="fc6d5-169">«Создание модели»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-169">"Make,Model"</span></span> |

<span data-ttu-id="fc6d5-170">Принимает значение одного заголовка или список разделенных запятыми значений заголовка, которые запускают обновления кэша, когда изменение значения параметра данных маршрута.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-170">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="fc6d5-171">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-171">Example:</span></span>

<span data-ttu-id="fc6d5-172">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="fc6d5-172">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="fc6d5-173">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="fc6d5-173">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="fc6d5-174">различаются по cookie</span><span class="sxs-lookup"><span data-stu-id="fc6d5-174">vary-by-cookie</span></span>

| <span data-ttu-id="fc6d5-175">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-175">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-176">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-176">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-177">Строка</span><span class="sxs-lookup"><span data-stu-id="fc6d5-177">String</span></span>            | <span data-ttu-id="fc6d5-178">". AspNetCore.Identity.Application»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-178">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="fc6d5-179">". AspNetCore.Identity.Application,HairColor»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-179">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="fc6d5-180">Принимает значение одного заголовка или список разделенных запятыми значений заголовка, которые запускают обновления кэша, когда изменение (s) значения заголовка.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-180">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="fc6d5-181">Следующий пример просматривает файл cookie, связанные с ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-181">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="fc6d5-182">Когда пользователь проходит проверку подлинности запроса куки-файл задать активизирующий обновления кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-182">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="fc6d5-183">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-183">Example:</span></span>

```cshtml
<Cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="fc6d5-184">изменяться на уровне пользователей</span><span class="sxs-lookup"><span data-stu-id="fc6d5-184">vary-by-user</span></span>

| <span data-ttu-id="fc6d5-185">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-185">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-186">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-186">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-187">Boolean</span><span class="sxs-lookup"><span data-stu-id="fc6d5-187">Boolean</span></span>             | <span data-ttu-id="fc6d5-188">"true"</span><span class="sxs-lookup"><span data-stu-id="fc6d5-188">"true"</span></span>                  |
|                     | <span data-ttu-id="fc6d5-189">«false» (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="fc6d5-189">"false" (default)</span></span> |

<span data-ttu-id="fc6d5-190">Указывает, должна ли сбросить кэш, при изменении пользователя, выполнившего вход (или участника контекста).</span><span class="sxs-lookup"><span data-stu-id="fc6d5-190">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="fc6d5-191">Текущий пользователь, также называемая участника контекста запроса и можно просмотреть с помощью ссылки на представления Razor `@User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-191">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="fc6d5-192">Следующий пример просматривает текущего вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-192">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="fc6d5-193">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-193">Example:</span></span>

```cshtml
<Cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="fc6d5-194">С помощью этого атрибута сохраняет содержимое в кэше журнала и журнала цикла.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-194">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="fc6d5-195">При использовании `vary-by-user="true"`, журнала и журнала действий делает недействительным кэш для проверенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-195">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="fc6d5-196">Кэш становится недействительным, поскольку новое значение уникальный файл cookie создается при входе в систему.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-196">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="fc6d5-197">Кэш хранится для анонимных состояния при объекты cookie не существует или уже истек.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-197">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="fc6d5-198">Это означает, что если пользователь не входит в систему, будет поддерживаться кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-198">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="fc6d5-199">изменяющиеся</span><span class="sxs-lookup"><span data-stu-id="fc6d5-199">vary-by</span></span>

| <span data-ttu-id="fc6d5-200">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-200">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-201">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-201">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-202">Строка</span><span class="sxs-lookup"><span data-stu-id="fc6d5-202">String</span></span>             | <span data-ttu-id="fc6d5-203">"@Model"</span><span class="sxs-lookup"><span data-stu-id="fc6d5-203">"@Model"</span></span>                 |


<span data-ttu-id="fc6d5-204">Позволяет настраивать Возвращает кэшированные данные.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-204">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="fc6d5-205">При обновлении объект, упоминаемый в строковое значение атрибута изменяется, содержимое тега вспомогательный объект кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-205">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="fc6d5-206">Часто объединение строк значений модели назначаются данному атрибуту.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-206">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="fc6d5-207">По сути, это означает, что делает кэш недействительным обновления к любому из объединенных значений.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-207">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="fc6d5-208">В следующем примере предполагается визуализации представления суммы целочисленное значение между двумя параметрами маршрута метода контроллера `myParam1` и `myParam2`и возвращает, как свойство одной модели.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-208">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="fc6d5-209">При изменении этой суммы, содержимое тега вспомогательного метода кэша к просмотру и снова кэшируется.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-209">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="fc6d5-210">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-210">Example:</span></span>

<span data-ttu-id="fc6d5-211">Действие:</span><span class="sxs-lookup"><span data-stu-id="fc6d5-211">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="fc6d5-212">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="fc6d5-212">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="fc6d5-213">priority</span><span class="sxs-lookup"><span data-stu-id="fc6d5-213">priority</span></span>

| <span data-ttu-id="fc6d5-214">Тип атрибута</span><span class="sxs-lookup"><span data-stu-id="fc6d5-214">Attribute Type</span></span>    | <span data-ttu-id="fc6d5-215">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="fc6d5-215">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="fc6d5-216">Перечисления CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="fc6d5-216">CacheItemPriority</span></span>  | <span data-ttu-id="fc6d5-217">«Высокие»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-217">"High"</span></span>                   |
|                    | <span data-ttu-id="fc6d5-218">«Низкое»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-218">"Low"</span></span> |
|                    | <span data-ttu-id="fc6d5-219">«NeverRemove»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-219">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="fc6d5-220">«Normal»</span><span class="sxs-lookup"><span data-stu-id="fc6d5-220">"Normal"</span></span> |

<span data-ttu-id="fc6d5-221">Руководство вытеснения кэша поставщику встроенного кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-221">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="fc6d5-222">Веб-сервер будет вытеснять `Low` первым кэша записи при нехватке памяти.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-222">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="fc6d5-223">Пример.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-223">Example:</span></span>

```cshtml
<Cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="fc6d5-224">`priority` Атрибута не гарантирует определенный уровень хранения кэша.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-224">The `priority` attribute does not guarantee a specific level of cache retention.</span></span> <span data-ttu-id="fc6d5-225">`CacheItemPriority`— только это предложение.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-225">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="fc6d5-226">Задав этому атрибуту значение `NeverRemove` не гарантирует, что кэша всегда будет сохранено.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-226">Setting this attribute to `NeverRemove` does not guarantee that the cache will always be retained.</span></span> <span data-ttu-id="fc6d5-227">В разделе [дополнительные ресурсы](#additional-resources) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-227">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="fc6d5-228">Вспомогательный тег кэша зависит от [памяти служба кэша](xref:performance/caching/memory).</span><span class="sxs-lookup"><span data-stu-id="fc6d5-228">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="fc6d5-229">Вспомогательный тег кэша добавляет службу, если он не был добавлен.</span><span class="sxs-lookup"><span data-stu-id="fc6d5-229">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc6d5-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fc6d5-230">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>