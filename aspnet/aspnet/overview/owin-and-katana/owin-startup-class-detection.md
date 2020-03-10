---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWıN başlangıç sınıfı algılama | Microsoft Docs
author: Praburaj
description: Bu öğreticide, hangi OWıN başlangıç sınıfının yüklendiğini nasıl yapılandıracağınız gösterilmektedir. OWıN hakkında daha fazla bilgi için bkz. proje Katana 'Ya genel bakış. Bu öğretici...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617049"
---
# <a name="owin-startup-class-detection"></a>OWIN Başlangıç Sınıfı Algılama

> Bu öğreticide, hangi OWıN başlangıç sınıfının yüklendiğini nasıl yapılandıracağınız gösterilmektedir. OWıN hakkında daha fazla bilgi için bkz. [Proje Katana 'Ya genel bakış](an-overview-of-project-katana.md). Bu öğretici, Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan ve Howard dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) tarafından yazılmıştır.
>
> ## <a name="prerequisites"></a>Önkoşullar
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>OWIN Başlangıç Sınıfı Algılama

 Her OWıN uygulamasının, uygulama ardışık düzeni için bileşenleri belirttiğiniz bir başlangıç sınıfı vardır. Seçtiğiniz barındırma modeline (OwinHost, IIS ve IIS-Express) bağlı olarak, başlangıç sınıfınızı çalışma zamanına bağlamak için kullanabileceğiniz farklı yollar vardır. Bu öğreticide gösterilen başlangıç sınıfı, her barındırma uygulamasında kullanılabilir. Aşağıdaki yaklaşımlardan birini kullanarak başlangıç sınıfını barındırma çalışma zamanına bağlayabilirsiniz:

1. **Adlandırma kuralı**: Katana, derleme adı veya genel ad alanıyla eşleşen ad alanında `Startup` adlı bir sınıfı arar.
2. **Owinstartup özniteliği**: Bu, çoğu geliştiricilerin başlangıç sınıfını belirtmek için gereken yaklaşımdır. Aşağıdaki öznitelik, başlangıç sınıfını `StartupDemo` ad alanındaki `TestStartup` sınıfına ayarlar.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` öznitelik, adlandırma kuralını geçersiz kılar. Ayrıca, Bu öznitelikle kolay bir ad belirtebilirsiniz, ancak kolay bir ad kullanmak için yapılandırma dosyasında `appSetting` öğesini de kullanmanız gerekir.
3. **Yapılandırma dosyasındaki appSetting öğesi**: `appSetting` öğesi `OwinStartup` özniteliğini ve adlandırma kuralını geçersiz kılar. Birden çok başlangıç sınıfına sahip olabilirsiniz (her biri bir `OwinStartup` özniteliği kullanarak) ve aşağıdakine benzer bir biçimlendirme kullanarak bir yapılandırma dosyasına hangi başlangıç sınıfının yükleneceğini yapılandırabilirsiniz:

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   Başlangıç sınıfını ve derlemeyi açıkça belirten aşağıdaki anahtar de kullanılabilir:

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   Yapılandırma dosyasındaki aşağıdaki XML `ProductionConfiguration`kolay bir başlangıç sınıfı adı belirtir.

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   Yukarıdaki biçimlendirme, kolay bir ad belirten ve `ProductionStartup2` sınıfının çalışmasına neden olan aşağıdaki `OwinStartup` özniteliğiyle kullanılmalıdır.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. OWıN başlangıç bulmayı devre dışı bırakmak için, Web. config dosyasında `"false"` bir değeri ile `appSetting owin:AutomaticAppStartup` ekleyin.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>OWıN başlangıcını kullanarak bir ASP.NET Web uygulaması oluşturma

1. Boş bir Asp.Net Web uygulaması oluşturun ve bunu **Startupdemo**olarak adlandırın. -NuGet Paket Yöneticisi 'ni kullanarak `Microsoft.Owin.Host.SystemWeb` 'i yükler. **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Aşağıdaki komutu girin:

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. Bir OWıN başlangıç sınıfı ekleyin. Visual Studio 2017 ' de projeye sağ tıklayın ve **Sınıf Ekle**' yi seçin.- **Yeni öğe Ekle** iletişim kutusunda, arama alanına *owın* girin ve adı Startup.cs olarak değiştirin ve ardından **Ekle**' yi seçin.

     ![](owin-startup-class-detection/_static/image1.png)

   *Owın başlangıç sınıfını*bir dahaki sefer eklemek Istediğinizde, **Ekle** menüsünde kullanılabilir olacaktır.

     ![](owin-startup-class-detection/_static/image2.png)

   Alternatif olarak, projeye sağ tıklayıp **Ekle**' yi ve ardından **Yeni öğe**' yi seçip **owın başlangıç sınıfını**seçebilirsiniz.

     ![](owin-startup-class-detection/_static/image3.png)

- *Startup.cs* dosyasındaki oluşturulan kodu aşağıdaki kodla değiştirin:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` lambda ifadesi, belirtilen ara yazılım bileşenini OWıN ardışık düzenine kaydetmek için kullanılır. Bu durumda, gelen istek yanıtlanmadan önce gelen isteklerin günlüğe kaydedilmesini ayarlarız. `next` parametresi, işlem hattındaki sonraki bileşene yönelik temsilcidir ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;). `app.Run` lambda ifadesi, ardışık düzeni gelen isteklere takar ve yanıt mekanizmasını sağlar.
     > [!NOTE]
     > Yukarıdaki kodda `OwinStartup` özniteliği kullanıma sunuyoruz ve `Startup` adlı sınıfı çalıştırma kuralına ulaştınız.-uygulamayı çalıştırmak için ***F5*** tuşuna basın. Birkaç kez Yenile 'yi ziyaret edin.

    ![](owin-startup-class-detection/_static/image4.png) Not: Bu öğreticideki resimlerde gösterilen sayı gördüğünüz sayıyla eşleşmeyecektir. Milisaniyelik dize, sayfayı yenilediğinizde yeni bir yanıt göstermek için kullanılır.
  İzleme bilgilerini **Çıkış** penceresinde görebilirsiniz.

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>Daha fazla başlangıç sınıfı ekleyin

Bu bölümde, başka bir başlangıç sınıfı ekleyeceğiz. Uygulamanıza birden çok OWıN başlangıç sınıfı ekleyebilirsiniz. Örneğin, geliştirme, test ve üretim için başlangıç sınıfları oluşturmak isteyebilirsiniz.

1. Yeni bir OWıN başlangıç sınıfı oluşturun ve `ProductionStartup`adlandırın.
2. Oluşturulan kodu aşağıdaki kodla değiştirin:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. Uygulamayı çalıştırmak için Control F5 tuşuna basın. `OwinStartup` özniteliği üretim başlangıç sınıfının çalıştırıldığını belirtir.

    ![](owin-startup-class-detection/_static/image6.png)
4. Başka bir OWıN başlangıç sınıfı oluşturun ve `TestStartup`adlandırın.
5. Oluşturulan kodu aşağıdaki kodla değiştirin:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   Yukarıdaki `OwinStartup` özniteliği aşırı yüklemesi başlangıç sınıfının *kolay* adı olarak `TestingConfiguration` belirtir.
6. *Web. config* dosyasını açın ve başlangıç sınıfının kolay adını belirten Owın uygulama başlangıç anahtarını ekleyin:

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. Uygulamayı çalıştırmak için Control F5 tuşuna basın. Uygulama ayarları öğesi bundan sonra, test yapılandırması çalıştırılır.

    ![](owin-startup-class-detection/_static/image7.png)
8. `TestStartup` sınıfındaki `OwinStartup` özniteliğinden *kolay* adı kaldırın.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. *Web. config* dosyasındaki Owın uygulama başlangıç anahtarını aşağıdakiler ile değiştirin:

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. Her sınıftaki `OwinStartup` özniteliğini, Visual Studio tarafından oluşturulan varsayılan öznitelik koduna döndürür:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    Aşağıdaki OWIN uygulama başlangıç anahtarlarının her biri, üretim sınıfının çalışmasına neden olur.

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    Son başlangıç anahtarı başlangıç yapılandırma yöntemini belirtir. Aşağıdaki OWIN uygulama başlangıç anahtarı, yapılandırma sınıfının adını `MyConfiguration` değiştirmenize izin verir.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Owinhost. exe kullanma

1. Web. config dosyasını aşağıdaki biçimlendirme ile değiştirin:

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   Bu durumda `TestStartup`, son anahtar kazanır.
2. PMC 'den Owinhost 'u yükler:

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. Uygulama klasörüne ( *Web. config* dosyasını içeren klasör) gidin ve komut istemine şunu yazın:

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   Komut penceresinde şunları gösterilecektir:

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. URL `http://localhost:5000/`bir tarayıcı başlatın.

    ![](owin-startup-class-detection/_static/image8.png)

   OwinHost, yukarıda listelenen başlangıç kurallarını kabul eden bir.
5. Komut penceresinde, OwinHost programından çıkmak için ENTER tuşuna basın.
6. `ProductionStartup` sınıfında, bir *Üretim yapılandırmasının*kolay adını belirten aşağıdaki Owınstartup özniteliğini ekleyin.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. Komut istemine şunu yazın:

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   Üretim başlangıç sınıfı yüklenir.
    ![](owin-startup-class-detection/_static/image9.png)

   Uygulamamız birden çok başlangıç sınıfına sahiptir ve bu örnekte, çalışma zamanına kadar hangi başlangıç sınıfının yükleneceğini erteliyoruz.
8. Aşağıdaki çalışma zamanı başlatma seçeneklerini sınayın:

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
