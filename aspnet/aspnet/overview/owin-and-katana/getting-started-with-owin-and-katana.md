---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWıN ve Katana ile çalışmaya başlama | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584674"
---
# <a name="getting-started-with-owin-and-katana"></a>OWIN ve Katana ile Çalışmaya Başlama

, [Mike te son](https://github.com/MikeWasson)

[.Net Için açık Web arabirimi (OWıN)](http://owin.org/) , .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web sunucusunu uygulamadan ayırarak .NET Web geliştirme için ara yazılım oluşturmayı kolaylaştırır. Ayrıca, OWIN, Web uygulamalarının diğer konaklara&#8212;, örneğin bir Windows hizmetinde veya başka bir işlemde kendi kendine barındırılmasına yönelik bağlantı noktasını daha kolay hale getirir.

OWIN, bir uygulama değil, topluluğa ait bir belirtimdir. Katana proje, Microsoft tarafından geliştirilen açık kaynaklı bir OWIN bileşenleri kümesidir. Hem OWIN hem de Katana 'ya genel bir bakış için bkz. [Proje Katana 'Ya genel bakış](an-overview-of-project-katana.md). Bu makalede, başlamak için hemen koda atlayacağım.

Bu öğretici [Visual Studio 2013 Sürüm adayını](https://go.microsoft.com/fwlink/?LinkId=306566)kullanır, ancak Visual Studio 2012 ' i de kullanabilirsiniz. Visual Studio 2012 ' de birkaç adım daha farklı olduğundan, aşağıda notlıyorum.

## <a name="host-owin-in-iis"></a>IIS 'de OWIN Konağı

Bu bölümde, IIS 'de OWıN barındırılırsınız. Bu seçenek, bir OWIN işlem hattının esneklik ve bir şekilde bir arada olmasını, IIS 'nin yetişkinlere yönelik özellik kümesiyle birlikte sağlar. Bu seçeneği kullanarak OWIN uygulaması ASP.NET istek ardışık düzeninde çalışır.

İlk olarak, yeni bir ASP.NET Web uygulaması projesi oluşturun. (Visual Studio 2012 ' de ASP.NET boş Web uygulaması proje türünü kullanın.)

![](getting-started-with-owin-and-katana/_static/image1.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin.

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>NuGet paketleri Ekle

Ardından, gerekli NuGet paketlerini ekleyin. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>Başlangıç sınıfı ekleme

Ardından, bir OWıN başlangıç sınıfı ekleyin. Çözüm Gezgini, projeye sağ tıklayın ve **Ekle**' yi ve ardından **Yeni öğe**' yi seçin. **Yeni öğe Ekle** Iletişim kutusunda **owın başlangıç sınıfı**' nı seçin. Başlangıç sınıfını yapılandırma hakkında daha fazla bilgi için, bkz. [Owın başlangıç sınıfı algılama](owin-startup-class-detection.md).

![](getting-started-with-owin-and-katana/_static/image4.png)

`Startup1.Configuration` yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

Bu kod, OWıN ardışık düzenine bir **Microsoft. Owin. ıowincontext** örneği alan bir işlev olarak uygulanan basit bir ara yazılım parçası ekler. Sunucu bir HTTP isteği aldığında, OWıN işlem hattı ara yazılımı çağırır. Ara yazılım, yanıt için içerik türünü ayarlar ve yanıt gövdesini yazar.

> [!NOTE]
> OWıN başlangıç sınıfı şablonu Visual Studio 2013 kullanılabilir. Visual Studio 2012 kullanıyorsanız, yalnızca `Startup1`adlı yeni bir boş sınıf ekleyin ve aşağıdaki kodu yapıştırın:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>Uygulamayı çalıştırma

Hata ayıklamaya başlamak için F5 'e basın. Visual Studio, `http://localhost:*port*/`için bir tarayıcı penceresi açar. Sayfa aşağıdaki gibi görünmelidir:

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>Konsol uygulamasındaki Self-Host OWIN

Bu uygulamayı IIS barındırmanın özel bir işlemde kendi kendine barındırılmasına dönüştürmek çok kolay. IIS barındırma ile IIS, hem HTTP sunucusu hem de hizmeti barındıran işlem olarak davranır. Kendi kendine barındırma ile, uygulamanız süreci oluşturur ve HTTP sunucusu olarak **HttpListener** sınıfını kullanır.

Visual Studio 'da yeni bir konsol uygulaması oluşturun. Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:

`Install-Package Microsoft.Owin.SelfHost -Pre`

Bu öğreticinin 1. bölümünde projeye `Startup1` bir sınıf ekleyin. Bu sınıfı değiştirmenize gerek yok.

Uygulamanın `Main` yöntemini aşağıdaki şekilde uygulayın.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

Konsol uygulamasını çalıştırdığınızda, sunucu `http://localhost:9000`dinlemeye başlar. Bu adrese bir Web tarayıcısında gittiğinizde, "Merhaba Dünya" sayfasını görürsünüz.

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>OWıN tanılamayı ekleme

Microsoft. Owin. Diagnostics paketi işlenmemiş özel durumları yakalayan ve hata ayrıntıları içeren bir HTML sayfası görüntüleyen ara yazılım içerir. Bu sayfa, bazen "[sarı ekran](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)hatası" (Ysod) olarak adlandırılan ASP.NET hata sayfasına benzer şekilde çalışır. YSOD gibi, Katana hata sayfası geliştirme sırasında faydalıdır, ancak üretim modunda devre dışı bırakmak iyi bir uygulamadır.

Tanılama paketini projenize yüklemek için, Paket Yöneticisi konsol penceresine aşağıdaki komutu yazın:

`install-package Microsoft.Owin.Diagnostics –Pre`

`Startup1.Configuration` yöntemdeki kodu aşağıdaki gibi değiştirin:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

Şimdi, Visual Studio 'Nun özel durum üzerinde kesintiye uğramaması için, uygulamayı hata ayıklamadan çalıştırmak için CTRL + F5 kullanın. Uygulama, `http://localhost/fail`' a gitene kadar, uygulamanın özel durumu oluşturulduğu noktada, önceki ile aynı şekilde davranır. Hata sayfası ara yazılımı, özel durumu yakalar ve hata hakkında bilgi içeren bir HTML sayfası görüntüler. Yığın, sorgu dizesi, tanımlama bilgileri, istek üst bilgisi ve OWıN ortam değişkenlerini görmek için sekmelere tıklayabilirsiniz.

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>Sonraki Adımlar

- [OWIN Başlangıç Sınıfı Algılama](owin-startup-class-detection.md)
- [OWıN kullanarak Self-Host ASP.NET Web API 'SI](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [OWIN 'ı kullanarak kendi kendini barındırın SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
