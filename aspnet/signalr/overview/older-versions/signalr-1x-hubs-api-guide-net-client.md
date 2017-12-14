---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: "Справочник по API концентраторов ASP.NET SignalR - клиент .NET (SignalR 1.x) | Документы Microsoft"
author: pfletcher
description: "В этом документе содержатся вводные сведения с помощью API концентраторов SignalR версии 2 в таких клиентов .NET, магазин Windows (WinRT), WPF, Silverlight и недостатки..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 9cf99ba7887e7db847097a63c0a964ef5d461a9d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="7758f-103">Справочник по API концентраторов ASP.NET SignalR - клиент .NET (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="7758f-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>
====================
<span data-ttu-id="7758f-104">по [Флетчера Патрик](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7758f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="7758f-105">В этом документе содержатся вводные сведения с помощью API концентраторов SignalR версии 2 в таких клиентов .NET, магазин Windows (WinRT), WPF, Silverlight и консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="7758f-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="7758f-106">API концентраторов SignalR позволяет вносить удаленные вызовы процедур (RPC) с сервера на подключенных клиентов и от клиентов к серверу.</span><span class="sxs-lookup"><span data-stu-id="7758f-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="7758f-107">В серверном коде определять методы, которые могут быть вызваны клиентов и вызова методов, которые выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="7758f-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="7758f-108">В клиентском коде определяют методы, которые могут быть вызваны с сервера и вызывать методы, которые выполняются на сервере.</span><span class="sxs-lookup"><span data-stu-id="7758f-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="7758f-109">SignalR обеспечивает всех коммуникаций клиент сервер для вас.</span><span class="sxs-lookup"><span data-stu-id="7758f-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="7758f-110">SignalR также предлагает API нижнего уровня, который называется постоянные подключения.</span><span class="sxs-lookup"><span data-stu-id="7758f-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="7758f-111">Общие сведения о SignalR, концентраторов и постоянные подключения или учебник, в котором показано, как построить полное приложение SignalR см. [SignalR — начало работы](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="7758f-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="7758f-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="7758f-112">Overview</span></span>

<span data-ttu-id="7758f-113">Этот документ содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="7758f-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="7758f-114">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="7758f-115">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="7758f-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="7758f-116">Соединения между доменами от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="7758f-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="7758f-117">Настройка соединения</span><span class="sxs-lookup"><span data-stu-id="7758f-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="7758f-118">Как задать максимальное число одновременных подключений клиентов WPF</span><span class="sxs-lookup"><span data-stu-id="7758f-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="7758f-119">Как задать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="7758f-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="7758f-120">Как задать метод транспорта</span><span class="sxs-lookup"><span data-stu-id="7758f-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="7758f-121">Как задать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="7758f-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="7758f-122">Практическое задание сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="7758f-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="7758f-123">Создание прокси-сервера концентратора</span><span class="sxs-lookup"><span data-stu-id="7758f-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="7758f-124">Как определить на стороне клиента, сервер может вызывать методы</span><span class="sxs-lookup"><span data-stu-id="7758f-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="7758f-125">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="7758f-126">Методы с параметрами, указание типов параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="7758f-127">Методы с параметрами, указав динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="7758f-128">Удаление обработчика</span><span class="sxs-lookup"><span data-stu-id="7758f-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="7758f-129">Способ вызова методов сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="7758f-130">Как обрабатывать события времени жизни соединений</span><span class="sxs-lookup"><span data-stu-id="7758f-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="7758f-131">Способ обработки ошибок</span><span class="sxs-lookup"><span data-stu-id="7758f-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="7758f-132">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="7758f-133">WPF, Silverlight и образцы кода приложения консоли для методов клиента, сервер может вызывать</span><span class="sxs-lookup"><span data-stu-id="7758f-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="7758f-134">Для клиентских проектов .NET образца см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7758f-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="7758f-135">[Андрей armenta / SignalR образцы](https://github.com/gustavo-armenta/SignalR-Samples) на GitHub.com (примеры приложений WinRT, Silverlight, консоль).</span><span class="sxs-lookup"><span data-stu-id="7758f-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="7758f-136">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) на GitHub.com (например, WPF).</span><span class="sxs-lookup"><span data-stu-id="7758f-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="7758f-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) на GitHub.com (пример консольного приложения).</span><span class="sxs-lookup"><span data-stu-id="7758f-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="7758f-138">Документацию по программированию сервера или клиентов JavaScript см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7758f-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="7758f-139">Справочник по API концентраторов SignalR - сервера</span><span class="sxs-lookup"><span data-stu-id="7758f-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="7758f-140">Справочник по API концентраторов SignalR - клиент JavaScript</span><span class="sxs-lookup"><span data-stu-id="7758f-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="7758f-141">Ссылки на разделы справки по API, до версии .NET 4.5 API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7758f-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="7758f-142">Если вы используете .NET 4, см. раздел [версии .NET 4 разделов API](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="7758f-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="7758f-143">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-143">Client setup</span></span>

<span data-ttu-id="7758f-144">Установка [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) пакет NuGet (не [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) пакета).</span><span class="sxs-lookup"><span data-stu-id="7758f-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="7758f-145">Данный пакет поддерживает WinRT, Silverlight, WPF, консольное приложение и клиенты Windows Phone для .NET 4 и .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="7758f-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="7758f-146">Версия SignalR, у вас есть на стороне клиента отличается от версии, у вас есть на сервере, SignalR часто является возможность адаптироваться к разницу.</span><span class="sxs-lookup"><span data-stu-id="7758f-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="7758f-147">Например при отпускании SignalR версии 2.0 и установки, на сервере, сервер будет поддерживать клиентов, имеющих 1.1.x установлен, а также клиенты, имеющие 2.0 установлена.</span><span class="sxs-lookup"><span data-stu-id="7758f-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="7758f-148">Если разница между версию на сервере и на клиентском компьютере слишком велико, SignalR вызывает `InvalidOperationException` исключения, когда клиент пытается установить соединение.</span><span class="sxs-lookup"><span data-stu-id="7758f-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="7758f-149">Сообщение об ошибке «`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`».</span><span class="sxs-lookup"><span data-stu-id="7758f-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="7758f-150">Как установить соединение</span><span class="sxs-lookup"><span data-stu-id="7758f-150">How to establish a connection</span></span>

<span data-ttu-id="7758f-151">Перед установкой соединения необходимо создать `HubConnection` объекта и создать учетную запись-посредник.</span><span class="sxs-lookup"><span data-stu-id="7758f-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="7758f-152">Чтобы установить соединение, вызовите `Start` метод `HubConnection` объекта.</span><span class="sxs-lookup"><span data-stu-id="7758f-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="7758f-153">Для клиентов JavaScript необходимо зарегистрировать по крайней мере один обработчик событий перед вызовом `Start` метод, чтобы установить соединение.</span><span class="sxs-lookup"><span data-stu-id="7758f-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="7758f-154">Это не требуется для клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="7758f-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="7758f-155">Для клиентов JavaScript, созданный код прокси автоматически создает учетных записей-посредников для всех концентраторов, которые существуют на сервере, и регистрация обработчика — это как можно указать, какие концентраторов клиент планирует использовать.</span><span class="sxs-lookup"><span data-stu-id="7758f-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="7758f-156">Но для клиента .NET создать прокси-серверы концентратора вручную, поэтому SignalR предполагается, что вы используете любой концентратора, создать прокси для.</span><span class="sxs-lookup"><span data-stu-id="7758f-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="7758f-157">В примере кода используется значение по умолчанию «/ signalr» URL-адрес для подключения к службе SignalR.</span><span class="sxs-lookup"><span data-stu-id="7758f-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="7758f-158">Сведения о том, как задать другой базовый URL-адрес см. в разделе [API концентраторов руководство - Server - /signalr URL-адрес для ASP.NET SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="7758f-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="7758f-159">`Start` Метод выполняется асинхронно.</span><span class="sxs-lookup"><span data-stu-id="7758f-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="7758f-160">Чтобы убедиться в том, последующие строки кода, которые не выполняются до после установки подключения, используйте `await` в асинхронном методе ASP.NET 4.5 или `.Wait()` в синхронный метод.</span><span class="sxs-lookup"><span data-stu-id="7758f-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="7758f-161">Не используйте `.Wait()` в клиенте WinRT.</span><span class="sxs-lookup"><span data-stu-id="7758f-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="7758f-162">Класс `HubConnection` является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="7758f-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="7758f-163">Соединения между доменами от клиентов Silverlight</span><span class="sxs-lookup"><span data-stu-id="7758f-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="7758f-164">Сведения о том, как разрешить междоменные подключения от клиентов Silverlight см. в разделе [внесения службы через границы домена](https://msdn.microsoft.com/en-us/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="7758f-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/en-us/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="7758f-165">Настройка соединения</span><span class="sxs-lookup"><span data-stu-id="7758f-165">How to configure the connection</span></span>

<span data-ttu-id="7758f-166">Перед установкой соединения можно указать любой из следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="7758f-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="7758f-167">Ограничение одновременных подключений.</span><span class="sxs-lookup"><span data-stu-id="7758f-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="7758f-168">Параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="7758f-168">Query string parameters.</span></span>
- <span data-ttu-id="7758f-169">Метод транспорта.</span><span class="sxs-lookup"><span data-stu-id="7758f-169">The transport method.</span></span>
- <span data-ttu-id="7758f-170">Заголовки HTTP.</span><span class="sxs-lookup"><span data-stu-id="7758f-170">HTTP headers.</span></span>
- <span data-ttu-id="7758f-171">Сертификаты клиентов.</span><span class="sxs-lookup"><span data-stu-id="7758f-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="7758f-172">Как задать максимальное число одновременных подключений клиентов WPF</span><span class="sxs-lookup"><span data-stu-id="7758f-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="7758f-173">В WPF клиентов может потребоваться увеличить максимальное количество одновременных подключений, значение по умолчанию 2.</span><span class="sxs-lookup"><span data-stu-id="7758f-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="7758f-174">Рекомендуемое значение — 10.</span><span class="sxs-lookup"><span data-stu-id="7758f-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="7758f-175">Дополнительные сведения см. в разделе [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/en-us/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="7758f-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/en-us/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="7758f-176">Как задать параметры строки запроса</span><span class="sxs-lookup"><span data-stu-id="7758f-176">How to specify query string parameters</span></span>

<span data-ttu-id="7758f-177">Если вы хотите отправлять данные на сервер при подключении клиента, можно добавить параметры строки запроса для объекта соединения.</span><span class="sxs-lookup"><span data-stu-id="7758f-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="7758f-178">В следующем примере показано, как параметра строки запроса в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="7758f-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="7758f-179">Приведенный ниже показано, как прочитать параметр строки запроса в серверном коде.</span><span class="sxs-lookup"><span data-stu-id="7758f-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="7758f-180">Как задать метод транспорта</span><span class="sxs-lookup"><span data-stu-id="7758f-180">How to specify the transport method</span></span>

<span data-ttu-id="7758f-181">В составе процесса подключения клиента SignalR обычно запрашивает у сервера для определения наиболее транспорта, который поддерживается с сервера и клиента.</span><span class="sxs-lookup"><span data-stu-id="7758f-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="7758f-182">Если вы уже знаете, какие транспорта, который вы хотите использовать, вы можете обойти этот процесс согласования.</span><span class="sxs-lookup"><span data-stu-id="7758f-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="7758f-183">Чтобы указать метод транспорта, передайте объект транспорта к методу Start.</span><span class="sxs-lookup"><span data-stu-id="7758f-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="7758f-184">Приведенный ниже показано, как задать метод транспорта в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="7758f-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="7758f-185">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/en-us/library/jj918090(v=vs.111).aspx) пространство имен включает следующие классы, которые можно использовать для указания транспорта.</span><span class="sxs-lookup"><span data-stu-id="7758f-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/en-us/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="7758f-186">[LongPollingTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="7758f-186">[LongPollingTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="7758f-187">[ServerSentEventsTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="7758f-187">[ServerSentEventsTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="7758f-188">[WebSocketTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (доступен только в том случае, если сервер и клиент используют .NET 4.5.)</span><span class="sxs-lookup"><span data-stu-id="7758f-188">[WebSocketTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="7758f-189">[AutoTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (автоматически выбирает лучший транспорта, поддерживаемые клиентом и сервером.</span><span class="sxs-lookup"><span data-stu-id="7758f-189">[AutoTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="7758f-190">Это стандартный транспорт.</span><span class="sxs-lookup"><span data-stu-id="7758f-190">This is the default transport.</span></span> <span data-ttu-id="7758f-191">Это в для передачи `Start` метод действует так же, как в объекте, не передавая.)</span><span class="sxs-lookup"><span data-stu-id="7758f-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="7758f-192">ForeverFrame транспорта не включены в этот список, поскольку он используется только в браузерах.</span><span class="sxs-lookup"><span data-stu-id="7758f-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="7758f-193">Сведения о проверке метод транспорта в серверном коде см. в разделе [ASP.NET руководство по API концентраторов SignalR - Server - способы получения сведений о клиенте из контекстного свойства](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="7758f-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="7758f-194">Дополнительные сведения о транспортов и в случае ошибки см. в разделе [Общие сведения о SignalR - транспорта и в случае ошибки](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="7758f-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="7758f-195">Как задать заголовки HTTP</span><span class="sxs-lookup"><span data-stu-id="7758f-195">How to specify HTTP headers</span></span>

<span data-ttu-id="7758f-196">Чтобы задать заголовки HTTP, используйте `Headers` свойство для объекта connection.</span><span class="sxs-lookup"><span data-stu-id="7758f-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="7758f-197">Следующий пример демонстрирует добавление заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="7758f-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="7758f-198">Практическое задание сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="7758f-198">How to specify client certificates</span></span>

<span data-ttu-id="7758f-199">Чтобы добавить сертификаты клиентов, используйте `AddClientCertificate` метод для объекта connection.</span><span class="sxs-lookup"><span data-stu-id="7758f-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="7758f-200">Создание прокси-сервера концентратора</span><span class="sxs-lookup"><span data-stu-id="7758f-200">How to create the Hub proxy</span></span>

<span data-ttu-id="7758f-201">Для определения методов на стороне клиента, можно вызвать концентратор с сервера, а также вызывать методы концентратора на сервере, создайте прокси-сервер для концентратора путем вызова `CreateHubProxy` для объекта connection.</span><span class="sxs-lookup"><span data-stu-id="7758f-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="7758f-202">Строка передается в `CreateHubProxy` является именем класса концентратора или имя, указанное в `HubName` атрибута, если она использовалась на сервере.</span><span class="sxs-lookup"><span data-stu-id="7758f-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="7758f-203">Совпадение имен регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="7758f-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="7758f-204">**Класс концентратора на сервере**</span><span class="sxs-lookup"><span data-stu-id="7758f-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="7758f-205">**Создайте клиентский прокси для класса концентратора**</span><span class="sxs-lookup"><span data-stu-id="7758f-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="7758f-206">Если вы устанавливаете класса концентратора `HubName` атрибут, используйте его.</span><span class="sxs-lookup"><span data-stu-id="7758f-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="7758f-207">**Класс концентратора на сервере**</span><span class="sxs-lookup"><span data-stu-id="7758f-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="7758f-208">**Создайте клиентский прокси для класса концентратора**</span><span class="sxs-lookup"><span data-stu-id="7758f-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="7758f-209">Прокси-объект является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="7758f-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="7758f-210">На самом деле, если вы вызываете `HubConnection.CreateHubProxy` несколько раз с одинаковым `hubName`, будут получены в кэше же `IHubProxy` объекта.</span><span class="sxs-lookup"><span data-stu-id="7758f-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="7758f-211">Как определить на стороне клиента, сервер может вызывать методы</span><span class="sxs-lookup"><span data-stu-id="7758f-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="7758f-212">Чтобы определить метод, который можно вызвать сервера, использовать прокси-сервер `On` метода для регистрации обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="7758f-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="7758f-213">Метод совпадение имен регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="7758f-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="7758f-214">Например `Clients.All.UpdateStockPrice` на сервере будет выполняться `updateStockPrice`, `updatestockprice`, или `UpdateStockPrice` на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="7758f-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="7758f-215">Разные клиентские платформы имеют различные требования к написание кода в метод для обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7758f-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="7758f-216">В примерах предназначены для клиентов WinRT (.NET для магазина Windows).</span><span class="sxs-lookup"><span data-stu-id="7758f-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="7758f-217">WPF, Silverlight и консольного приложения примеры приведены в [отдельный раздел далее в этом разделе](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="7758f-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="7758f-218">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-218">Methods without parameters</span></span>

<span data-ttu-id="7758f-219">Если метод обработка не имеют параметров, используйте перегруженный неуниверсальных `On` метод:</span><span class="sxs-lookup"><span data-stu-id="7758f-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="7758f-220">**Серверный код вызова клиентского метода без параметров**</span><span class="sxs-lookup"><span data-stu-id="7758f-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="7758f-221">**WinRT клиентский код для метода вызвана с сервера без параметров ([примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="7758f-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="7758f-222">Методы с параметрами, указывающих типы параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="7758f-223">Если метод обработка имеет параметры, укажите типы параметров как универсальные типы `On` метод.</span><span class="sxs-lookup"><span data-stu-id="7758f-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="7758f-224">Существуют перегрузки универсального `On` метод, чтобы указать параметры до 8 (4 на Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="7758f-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="7758f-225">В следующем примере отправляется один параметр `UpdateStockPrice` метода.</span><span class="sxs-lookup"><span data-stu-id="7758f-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="7758f-226">**Вызов клиентского метода с параметром серверного кода**</span><span class="sxs-lookup"><span data-stu-id="7758f-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="7758f-227">**Класс Stock, используемое для параметра**</span><span class="sxs-lookup"><span data-stu-id="7758f-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="7758f-228">**WinRT клиентский код для метода вызвана с сервера с параметром ([примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="7758f-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="7758f-229">Методы с параметрами, указав динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="7758f-230">В качестве альтернативы для задания параметров, универсальных типов `On` метод, параметры можно указать в качестве динамических объектов:</span><span class="sxs-lookup"><span data-stu-id="7758f-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="7758f-231">**Вызов клиентского метода с параметром серверного кода**</span><span class="sxs-lookup"><span data-stu-id="7758f-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="7758f-232">**Класс Stock, используемое для параметра**</span><span class="sxs-lookup"><span data-stu-id="7758f-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="7758f-233">**WinRT клиентский код для метода вызвана с сервера с параметром, с помощью динамического объекта для параметра ([примеры WPF и Silverlight далее в этом разделе](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="7758f-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="7758f-234">Удаление обработчика</span><span class="sxs-lookup"><span data-stu-id="7758f-234">How to remove a handler</span></span>

<span data-ttu-id="7758f-235">Чтобы удалить обработчик, вызовите его `Dispose` метод.</span><span class="sxs-lookup"><span data-stu-id="7758f-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="7758f-236">**Клиентский код для метода с названием с сервера**</span><span class="sxs-lookup"><span data-stu-id="7758f-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="7758f-237">**Клиентский код для удаления обработчика**</span><span class="sxs-lookup"><span data-stu-id="7758f-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="7758f-238">Способ вызова методов сервера от клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-238">How to call server methods from the client</span></span>

<span data-ttu-id="7758f-239">Чтобы вызвать метод на сервере, используйте `Invoke` метод для прокси-сервера концентратора.</span><span class="sxs-lookup"><span data-stu-id="7758f-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="7758f-240">Если метод сервера не имеет возвращаемого значения, используйте перегруженный неуниверсальных `Invoke` метод.</span><span class="sxs-lookup"><span data-stu-id="7758f-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="7758f-241">**Серверный код для метода, который не имеет возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="7758f-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="7758f-242">**Код клиента, вызов метода, который не имеет возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="7758f-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="7758f-243">Если возвращаемое значение метода сервера, задать возвращаемый тип как универсальный тип `Invoke` метод.</span><span class="sxs-lookup"><span data-stu-id="7758f-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="7758f-244">**Серверный код для метода, который имеет возвращаемое значение и принимает параметр сложный тип**</span><span class="sxs-lookup"><span data-stu-id="7758f-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="7758f-245">**Биржевая класс, используемый для параметра и возвращаемого значения**</span><span class="sxs-lookup"><span data-stu-id="7758f-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="7758f-246">**Код клиента, вызов метода, который имеет возвращаемое значение и принимает параметр сложного типа в методе async ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="7758f-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="7758f-247">**Код клиента, вызов метода, который имеет возвращаемое значение и принимает сложного параметра типа, в синхронный метод**</span><span class="sxs-lookup"><span data-stu-id="7758f-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="7758f-248">`Invoke` Метод выполняется асинхронно и возвращает `Task` объекта.</span><span class="sxs-lookup"><span data-stu-id="7758f-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="7758f-249">Если не указать `await` или `.Wait()`, следующая строка кода будет выполняться до завершения выполнения метода, который можно вызывать.</span><span class="sxs-lookup"><span data-stu-id="7758f-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="7758f-250">Как обрабатывать события времени жизни соединений</span><span class="sxs-lookup"><span data-stu-id="7758f-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="7758f-251">SignalR обеспечивает следующее подключение события времени жизни, которые можно обрабатывать:</span><span class="sxs-lookup"><span data-stu-id="7758f-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="7758f-252">`Received`: Возникает при получении данных для соединения.</span><span class="sxs-lookup"><span data-stu-id="7758f-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="7758f-253">Предоставляет полученных данных.</span><span class="sxs-lookup"><span data-stu-id="7758f-253">Provides the received data.</span></span>
- <span data-ttu-id="7758f-254">`ConnectionSlow`: Возникает, если клиент обнаруживает подключение медленное или часто удаление.</span><span class="sxs-lookup"><span data-stu-id="7758f-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="7758f-255">`Reconnecting`: Возникает в случае транспорта начинает повторное подключение.</span><span class="sxs-lookup"><span data-stu-id="7758f-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="7758f-256">`Reconnected`: Возникает, когда была повторно присоединена транспорта.</span><span class="sxs-lookup"><span data-stu-id="7758f-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="7758f-257">`StateChanged`: Возникает при изменении состояния подключения.</span><span class="sxs-lookup"><span data-stu-id="7758f-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="7758f-258">Предоставляет состояния старое и новое состояние.</span><span class="sxs-lookup"><span data-stu-id="7758f-258">Provides the old state and the new state.</span></span> <span data-ttu-id="7758f-259">Сведения о подключения содержатся значения состояния [перечисление ConnectionState](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="7758f-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="7758f-260">`Closed`: Возникает, когда произойдет отключение соединения.</span><span class="sxs-lookup"><span data-stu-id="7758f-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="7758f-261">Например, если вы хотите отображать предупреждающие сообщения для ошибок, которые не являются неустранимыми, но нарушить временное подключение, таких как низкая или слишком частой удаление соединения, обрабатывают `ConnectionSlow` событий.</span><span class="sxs-lookup"><span data-stu-id="7758f-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="7758f-262">Дополнительные сведения см. в разделе [понимание и обработка события времени жизни соединений в SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="7758f-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="7758f-263">Способ обработки ошибок</span><span class="sxs-lookup"><span data-stu-id="7758f-263">How to handle errors</span></span>

<span data-ttu-id="7758f-264">Если подробные сообщения об ошибках на сервере не включен явно, объект исключения, которое возвращает SignalR после возникновения ошибки содержит минимум информации об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7758f-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="7758f-265">Например, если вызов `newContosoChatMessage` завершается ошибкой, содержит сообщение об ошибке в объекте ошибки «`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`» отправки подробных сообщений об ошибках на клиентах в рабочей среде не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.</span><span class="sxs-lookup"><span data-stu-id="7758f-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="7758f-266">Для обработки ошибок, которые вызывает SignalR, можно добавить обработчик `Error` событий для объекта connection.</span><span class="sxs-lookup"><span data-stu-id="7758f-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="7758f-267">Для обработки ошибок из вызовов методов, необходимо заключите код в блок try-catch.</span><span class="sxs-lookup"><span data-stu-id="7758f-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="7758f-268">Как включить ведение журнала на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="7758f-268">How to enable client-side logging</span></span>

<span data-ttu-id="7758f-269">Чтобы включить ведение журнала на стороне клиента, задайте `TraceLevel` и `TraceWriter` свойства для объекта connection.</span><span class="sxs-lookup"><span data-stu-id="7758f-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="7758f-270">WPF, Silverlight и образцы кода приложения консоли для методов клиента, сервер может вызывать</span><span class="sxs-lookup"><span data-stu-id="7758f-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="7758f-271">Примеры кода, приведенный выше, для определения методов клиента, сервер может вызывать применяются к клиентам WinRT.</span><span class="sxs-lookup"><span data-stu-id="7758f-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="7758f-272">В следующих примерах показано эквивалентный код для WPF, Silverlight и консоли приложений-клиентов.</span><span class="sxs-lookup"><span data-stu-id="7758f-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="7758f-273">Методы без параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-273">Methods without parameters</span></span>

<span data-ttu-id="7758f-274">**WPF клиентский код для метода вызвана с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="7758f-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="7758f-275">**Код клиента Silverlight для метода вызвана с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="7758f-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="7758f-276">**Код клиента приложения консоли для метода вызвана с сервера без параметров**</span><span class="sxs-lookup"><span data-stu-id="7758f-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="7758f-277">Методы с параметрами, указывающих типы параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="7758f-278">**WPF клиентский код для метода с названием с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="7758f-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="7758f-279">**Код клиента Silverlight для вызвана с сервера с параметром метода**</span><span class="sxs-lookup"><span data-stu-id="7758f-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="7758f-280">**Код клиента приложения консоли для метода вызвана с сервера с параметром**</span><span class="sxs-lookup"><span data-stu-id="7758f-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="7758f-281">Методы с параметрами, указав динамических объектов для параметров</span><span class="sxs-lookup"><span data-stu-id="7758f-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="7758f-282">**WPF клиентский код для метода с названием с сервера с параметром, с помощью динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="7758f-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="7758f-283">**Код клиента Silverlight для вызвана с сервера с параметром, с помощью динамического объекта для параметра метода**</span><span class="sxs-lookup"><span data-stu-id="7758f-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="7758f-284">**Код клиента приложения консоли для метода вызвана с сервера с параметром, с помощью динамического объекта для параметра**</span><span class="sxs-lookup"><span data-stu-id="7758f-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]