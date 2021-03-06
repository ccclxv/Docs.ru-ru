---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: "Сопоставление пользователей SignalR с подключениями | Документы Microsoft"
author: tfitzmac
description: "В этом разделе показано, как сохранить сведения о пользователях и их соединения. Патрик Флетчера помогли записи в этом разделе. Версии программного обеспечения, используемого в этом разделе..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/30/2014
ms.topic: article
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: c4f95a3b65c57dd7cb7c5c7f1ee09daa17fa9616
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
<a name="mapping-signalr-users-to-connections"></a>Сопоставление пользователей SignalR для подключения
====================
по [Tom FitzMacken](https://github.com/tfitzmac)

> В этом разделе показано, как сохранить сведения о пользователях и их соединения.
> 
> Патрик Флетчера помогли записи в этом разделе.
> 
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемого в этом разделе
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR версии 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>Предыдущие версии этого раздела
> 
> Сведения о более ранних версий SignalR см. в разделе [более ранних версий SignalR](../older-versions/index.md).
> 
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
> 
> Оставьте отзыв на том, как вам понравилось этого учебника и что можно улучшить в комментарии в нижней части страницы. Если у вас есть вопросы, которые не связаны непосредственно для работы с учебником, их можно разместить [форум по ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).


## <a name="introduction"></a>Вступление

Каждый клиент, подключающийся к концентратору передает уникальный идентификатор соединения. Можно получить это значение в `Context.ConnectionId` свойства контекста концентратора. Если приложению необходимо сопоставить пользователя с идентификатором соединения и сохранить это сопоставление, можно использовать один из следующих:

- [Поставщик идентификатора пользователя (SignalR 2)](#IUserIdProvider)
- [Хранение в памяти](#inmemory), такие как словарь
- [Группа SignalR для каждого пользователя](#groups)
- [Постоянная, внешнего хранилища](#database), таких как базы данных или хранилище таблиц Azure

В этом разделе показана каждая из этих реализаций. Вы используете `OnConnected`, `OnDisconnected`, и `OnReconnected` методы `Hub` класса для отслеживания состояния подключения пользователя.

Зависит от оптимального подхода для приложения.

- Число веб-серверов размещается приложение.
- Нужно ли получить список подключенных пользователей.
- Следует ли сохранять сведения пользователей и групп, когда приложение или сервер перезагружается.
- Задержка при вызове внешнего сервера является ли проблема.

В следующей таблице показано, какой подход работает для этих рекомендациях.

|  | Более одного сервера | Получить список подключенных пользователей | Сохранять данные после перезагрузки | Оптимальной производительности |
| --- | --- | --- | --- | --- |
| ИД пользователя поставщика | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| In-memory |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Группы в однопользовательском режиме | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Постоянными, внешний | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>Поставщик IUserID

Эта функция позволяет пользователям указать идентификатор пользователя — в зависимости от IRequest через новый интерфейс IUserIdProvider.

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

По умолчанию, будет реализация, которая использует пользователя `IPrincipal.Identity.Name` имени пользователя. Чтобы изменить этот параметр, зарегистрируйте реализации `IUserIdProvider` с глобальных узлов, при запуске приложения:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

Из в концентраторе, вы сможете отправлять сообщения пользователям через следующие API:

**Отправка сообщения для определенного пользователя**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Хранение в памяти

Следующие примеры показывают, как сохранить сведения о соединении и пользователя в словарь, который хранится в памяти. Словарь использует `HashSet` для хранения идентификатора соединения. В любой момент пользователь может иметь несколько подключений к приложению SignalR. Например пользователь, который подключается с помощью нескольких устройств или несколько вкладок браузер будет иметь более одного идентификатор подключения.

Если приложение завершает работу, все данные теряются, но он будет повторно заполнен как пользователи повторно устанавливать их соединения. Хранение в памяти не работает, если в среде имеются несколько веб-сервера, поскольку каждый сервер в отдельную коллекцию соединений.

В первом примере класс, который управляет сопоставления пользователей для подключения. Ключ для HashSet будет имя пользователя.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Следующий пример показано, как использовать класс сопоставления подключения от концентратора. Экземпляр класса хранится в имени переменной `_connections`.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Группы в однопользовательском режиме

Можно создать группу для каждого пользователя и отправить сообщение в эту группу для достижения только данный пользователь. Имя каждой группы является имя пользователя. Если пользователь имеет более одного соединения, каждый идентификатор соединения добавляется к группе пользователей.

Не следует удалять вручную пользователя из группы при отключении пользователя. Это действие выполняется автоматически платформой SignalR.

Приведенный ниже показано, как реализовать группы одного пользователя.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Постоянные, внешние хранилища

В этом разделе показано, как использовать базы данных или хранилище таблиц Azure для хранения сведений о соединении. Этот способ подходит при наличии нескольких веб-серверов, так как каждый веб-сервер может взаимодействовать с одного репозитория данных. Если остановить веб-серверов, работает или повторного запуска приложения `OnDisconnected` метод не вызывается. Таким образом возможно, репозиторий данных будет записи идентификаторов подключений, которые больше не являются допустимыми. Чтобы удалить эти потерянные записи, вы можете сделать недействительной любые соединения, который был создан за пределами периодичностью, необходимые для вашего приложения. Примеры в этом разделе содержат значение для отслеживания, когда подключение было создано, но не показано, как удалить старые записи, поскольку вы можете сделать это в фоновом процессе.

### <a name="database"></a>База данных

Следующие примеры показывают, как сохранить сведения о соединении и пользователя в базе данных. Можно использовать любой технологии доступа к данным; Тем не менее в приведенном ниже примере показан способ определения модели с использованием платформы Entity Framework. Эти модели сущностей соответствующие таблицы базы данных и полей. Структуру данных может значительно различаться в зависимости от требований приложения.

В первом примере показан способ определения Пользовательская сущность, которая может быть связан с большого количества объектов подключения.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Затем в центре можно отслеживать состояние каждого соединения с приведенный ниже код.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Хранилище таблиц Azure

В следующем примере хранилища Azure таблицы как в примере базы данных. Он не включает все данные, что необходимо начать работу со службой хранилища Azure таблицы. Сведения см. в разделе [как использовать хранилище таблиц из .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

В следующем примере показано сущности таблицы для хранения сведений о соединении. Секционирование данных по имени пользователя и идентифицирует каждую сущность, идентификатор подключения, пользователь может иметь несколько подключений в любое время.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

В концентраторе отслеживать состояние соединения каждого пользователя.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
