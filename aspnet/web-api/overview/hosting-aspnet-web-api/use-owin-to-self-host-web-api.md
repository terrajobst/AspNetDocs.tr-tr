---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWıN kullanarak Self-Host ASP.NET Web API-ASP.NET 4. x
author: rick-anderson
description: Konsol uygulamasında ASP.NET Web API 'sinin nasıl barındıralınacağını gösteren kod ile öğretici.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556541"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>OWıN kullanarak Self-Host ASP.NET Web API 'SI 

> Bu öğreticide, Web API çerçevesini Self barındırmak için OWIN kullanarak bir konsol uygulamasında ASP.NET Web API 'sinin nasıl barındıralınacağını gösterilmektedir.
>
> [.Net Için açık Web arabirimi](http://owin.org) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web uygulamasını sunucusundan ayırır, bu da bir Web uygulamasını kendi işleminizde IIS dışında bir Web uygulaması barındırmak için ideal hale getirir.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Web API 5.2.7

> [!NOTE]
> Bu öğreticinin tüm kaynak kodunu [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)adresinden bulabilirsiniz.

## <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' yi seçin. **Yüklü**, **Visual C#** altında, **Windows Masaüstü** ' nü seçin ve **konsol uygulaması (.NET Framework)** öğesini seçin. Projeyi "Owınselfhostsample" olarak adlandırın ve **Tamam**' ı seçin.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 'sini ve OWIN paketlerini ekleyin

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

Bu işlem, WebAPI OWıN Selfhost paketini ve tüm gerekli OWIN paketlerini yükler.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>Self-Host için Web API 'YI yapılandırma

Çözüm Gezgini, projeye sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin. `Startup`sınıfı adlandırın.

![](use-owin-to-self-host-web-api/_static/image5.png)

Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Web API denetleyicisi ekleme

Sonra, bir Web API denetleyici sınıfı ekleyin. Çözüm Gezgini, projeye sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin. `ValuesController`sınıfı adlandırın.

Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>OWıN konağını başlatın ve HttpClient ile bir istek yapın

Program.cs dosyasındaki tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>Uygulamayı çalıştırma

Uygulamayı çalıştırmak için, Visual Studio 'da F5 tuşuna basın. Çıktı aşağıdaki gibi görünmelidir:

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>Ek kaynaklar

[Project Katana’ya Genel Bakış](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure çalışan rolünde konak ASP.NET Web API 'SI](host-aspnet-web-api-in-an-azure-worker-role.md)
