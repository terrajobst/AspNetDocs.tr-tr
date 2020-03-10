---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC yürütme Işlemini anlama | Microsoft Docs
author: microsoft
description: ASP.NET MVC çerçevesinin bir tarayıcı isteği adım adım nasıl işlem kullandığını öğrenin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541519"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC Yürütme İşlemini Anlama

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET MVC çerçevesinin bir tarayıcı isteği adım adım nasıl işlem kullandığını öğrenin.

ASP.NET MVC tabanlı bir Web uygulamasına yönelik istekler, ilk olarak HTTP modülü olan **UrlRoutingModule** nesnesinden geçer. Bu modül, isteği ayrıştırır ve yol seçimini gerçekleştirir. **UrlRoutingModule** nesnesi, geçerli istekle eşleşen ilk yol nesnesini seçer. (Yol nesnesi, **RouteBase**uygulayan bir sınıftır ve genellikle **yol** sınıfının bir örneğidir.) Hiçbir yol eşleşmezse, **UrlRoutingModule** nesnesi hiçbir şey yapmaz ve isteğin normal ASP.NET veya IIS istek işlemeye geri dönmesine izin verir.

Seçili **yol** nesnesinden **UrlRoutingModule** nesnesi, **yol** nesnesiyle ilişkili **IRouteHandler** nesnesini alır. Genellikle, bir MVC uygulamasında bu bir **MvcRouteHandler**örneği olacaktır. **IRouteHandler** örneği bir **IHttpHandler** nesnesi oluşturur ve onu **IHttpContext** nesnesine geçirir. Varsayılan olarak, MVC için **IHttpHandler** örneği **MvcHandler** nesnesidir. **MvcHandler** nesnesi daha sonra isteği işleyecek olan denetleyiciyi seçer.

> [!NOTE]
> ASP.NET MVC web uygulaması IIS 7,0 ' de çalıştığında, MVC projeleri için dosya adı uzantısı gerekli değildir. Ancak, IIS 6,0 ' de, işleyici. Mvc dosya adı uzantısını ASP.NET ISAPI DLL 'SI ile eşlemenizi gerektirir.

Modül ve işleyici, ASP.NET MVC çerçevesinin giriş noktalarıdır. Aşağıdaki eylemleri gerçekleştirir:

- MVC web uygulamasında uygun denetleyiciyi seçin.
- Belirli bir denetleyici örneği edinin.
- Denetleyicinin **Execute** metodunu çağırın.

Aşağıda bir MVC web projesi yürütme aşamaları listelenmektedir:

- Uygulama için ilk isteği al 

    - Global. asax dosyasında, **route** nesneleri **RouteTable** nesnesine eklenir.
- Yönlendirme gerçekleştir 

    - **UrlRoutingModule** modülü, daha sonra bir **RequestContext** (**IHttpContext**) nesnesi oluşturmak için kullanılan **RouteData** nesnesini oluşturmak için **RouteTable** koleksiyonundaki ilk eşleşen **yol** nesnesini kullanır.
- MVC istek işleyicisi oluştur 

    - **MvcRouteHandler** nesnesi, **MvcHandler** sınıfının bir örneğini oluşturur ve onu **RequestContext** örneğine geçirir.
- Denetleyici oluştur 

    - **MvcHandler** nesnesi, ile denetleyici örneğini oluşturmak Için **IControllerFactory** nesnesini (genellikle **DefaultControllerFactory** sınıfının bir örneği) tanımlamak üzere **RequestContext** örneğini kullanır.
- Denetleyiciyi yürütme- **MvcHandler** örneği Controller for **Execute** metodunu çağırır. |
- Eylemi çağır 

    - Çoğu denetleyici **Controller** temel sınıfından devralınır. Bunu yapan denetleyiciler için, denetleyici ile ilişkili olan **ControllerActionInvoker** nesnesi, denetleyici sınıfının hangi eylem yöntemini çağırılacağını belirler ve ardından bu yöntemi çağırır.
- Sonucu Yürüt 

    - Tipik bir eylem yöntemi kullanıcı girişi alabilir, uygun yanıt verilerini hazırlayabilir ve sonuç türünü döndürerek sonucu yürütebilir. Yürütülemeyen yerleşik sonuç türleri şunlardır: **ViewResult** (bir görünüm oluşturur ve en sık kullanılan sonuç türü olan), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**ve **EmptyResult**.
