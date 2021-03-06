---
title: Поставщики хранилища ключей в ASP.NET Core
author: rick-anderson
description: Дополнительные сведения о поставщиках хранилища ключей в ASP.NET Core и как настроить расположение хранилища ключей.
manager: wpickett
ms.author: riande
ms.date: 01/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/implementation/key-storage-providers
ms.openlocfilehash: e8b7804e93b812c2e710ab15510c2fbaa7c4866d
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2018
---
# <a name="key-storage-providers-in-aspnet-core"></a>Поставщики хранилища ключей в ASP.NET Core

<a name="data-protection-implementation-key-storage-providers"></a>

По умолчанию система защиты данных [использует эвристику](xref:security/data-protection/configuration/default-settings) для определения, где должны сохраняться материалом ключа шифрования. Разработчик может переопределить эвристика и вручную указать расположение.

> [!NOTE]
> При указании расположения явную сохраняемость ключа система защиты данных будет отменить регистрацию шифрования ключа по умолчанию в механизм rest, который предоставляется эвристика, поэтому ключи больше не шифруются при хранении. Рекомендуется, можно Дополнительно [укажите механизм явного ключа шифрования](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest-providers) для производственных приложений.

Система защиты данных поставляется с нескольких поставщиков хранилища ключей в поле.

## <a name="file-system"></a>Файловая система

Мы полагаем, во многих приложениях будет использовать файл на основе системы ключа репозитория. Чтобы настроить ее, вызовите [PersistKeysToFileSystem](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/src/Microsoft.AspNetCore.DataProtection/DataProtectionBuilderExtensions.cs) подпрограммы конфигурации, как показано ниже. Укажите `DirectoryInfo` команды в репозиторий, где должно храниться ключей.

```csharp
sc.AddDataProtection()
       // persist keys to a specific directory
       .PersistKeysToFileSystem(new DirectoryInfo(@"c:\temp-keys\"));
   ```

`DirectoryInfo` Может указывать на каталог на локальном компьютере или она может указывать на папку на общем сетевом ресурсе. Если каталогу на локальном компьютере (и рекомендуется только приложения на локальном компьютере необходимо использовать этот репозиторий), рассмотрите возможность использования [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest) для шифрования ключей при хранении. В противном случае рассмотрите возможность использования [сертификат X.509](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest) для шифрования ключей при хранении.

## <a name="azure-and-redis"></a>Azure и Redis

`Microsoft.AspNetCore.DataProtection.AzureStorage` И `Microsoft.AspNetCore.DataProtection.Redis` пакетов разрешено хранение ключей защиты данных в хранилище Azure или кэш Redis. Ключи могут совместно использоваться в нескольких экземплярах веб-приложения. Приложения ASP.NET Core могут совместно использовать файлы cookie проверки подлинности или защиту CSRF по нескольким серверам. Чтобы настроить в Azure, вызовите один из [PersistKeysToAzureBlobStorage](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/src/Microsoft.AspNetCore.DataProtection.AzureStorage/AzureDataProtectionBuilderExtensions.cs) перегрузки метода, как показано ниже.

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blob URI including SAS token>"));

    services.AddMvc();
}
```

См. также [Azure тестовый код](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/samples/AzureBlob/Program.cs).

Чтобы настроить Redis, вызовите один из [PersistKeysToRedis](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/src/Microsoft.AspNetCore.DataProtection.Redis/RedisDataProtectionBuilderExtensions.cs) перегрузки метода, как показано ниже.

```
public void ConfigureServices(IServiceCollection services)
{
    // Connect to Redis database.
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToRedis(redis, "DataProtection-Keys");

    services.AddMvc();
}
```

Более подробную информацию см. в следующих разделах:

- [StackExchange.Redis ConnectionMultiplexer](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Basics.md)
- [Кэш Redis для Azure](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache#connect-to-the-cache)
- [Тестовый код redis](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/samples/Redis/Program.cs).

## <a name="registry"></a>Реестр

Иногда приложение не может иметь доступ на запись в файловой системе. Рассмотрим сценарий, где приложение выполняется виртуальной учетной записью службы (например, удостоверение пула приложений w3wp.exe). В таких случаях администратор может подготовить раздел реестра, соответствующий ACLed для учетной записи удостоверения службы. Вызовите [PersistKeysToRegistry](https://github.com/aspnet/DataProtection/blob/rel/1.1.0/src/Microsoft.AspNetCore.DataProtection/DataProtectionBuilderExtensions.cs) подпрограммы конфигурации, как показано ниже. Укажите `RegistryKey` указывает место хранения криптографических ключей и значений.

```csharp
   sc.AddDataProtection()
       // persist keys to a specific location in the system registry
       .PersistKeysToRegistry(Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Sample\keys"));
   ```

При использовании системного реестра как механизм сохраняемости, рассмотрите возможность использования [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest) для шифрования ключей при хранении.

## <a name="custom-key-repository"></a>Пользовательские хранилища ключей

Если встроенные механизмы не подходят, разработчик может указать собственный механизм сохраняемости ключа, предоставляя пользовательский `IXmlRepository`.
