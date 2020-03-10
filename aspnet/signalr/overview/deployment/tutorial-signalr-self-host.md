---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'Öğretici: SignalR Self-Host | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, şirket içinde barındırılan bir SignalR 2 sunucusu oluşturma ve bir JavaScript istemcisiyle buna bağlanma işlemlerinin nasıl yapılacağı gösterilmektedir. Eğitim V 'de kullanılan yazılım sürümleri...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558683"
---
# <a name="tutorial-signalr-self-host"></a>Öğretici: Şirket İçinde SignalR Barındırma

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> Bu öğreticide, şirket içinde barındırılan bir SignalR 2 sunucusu oluşturma ve bir JavaScript istemcisiyle buna bağlanma işlemlerinin nasıl yapılacağı gösterilmektedir.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>Visual Studio 2012 'yi bu öğreticiyle kullanma
>
>
> Visual Studio 2012 'yi bu öğreticiyle kullanmak için şunları yapın:
>
> - [Paket yöneticinize](http://docs.nuget.org/docs/start-here/installing-nuget) en son sürüme güncelleştirin.
> - [Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)'ni yükleme.
> - Web platformu yükleyicisinde, **Visual Studio 2012 için ASP.NET and Web Tools 2013,1**' i arayın ve yükleme yapın. Bu, **Merkez**gibi SignalR sınıfları Için Visual Studio şablonlarını yükler.
> - Bazı şablonlar ( **Owın başlangıç sınıfı**gibi) kullanılamayacak; Bunlar için bunun yerine bir sınıf dosyası kullanın.
>
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

## <a name="overview"></a>Genel bakış

Bir SignalR sunucusu, genellikle IIS 'deki bir ASP.NET uygulamasında barındırılır, ancak Self-Host kitaplığını kullanarak kendiliğinden barındırılabilen (bir konsol uygulaması veya Windows hizmeti gibi). Bu kitaplık, SignalR 2 ' nin tümü gibi, OWıN üzerinde oluşturulmuştur ([.net Için açık Web arabirimi](http://owin.org)). OWIN, .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web uygulamasını sunucusundan ayırır, bu da bir Web uygulamasını kendi işleminizde IIS dışında bir Web uygulaması barındırmak için ideal hale getirir.

IIS 'de barındırılamayan nedenler şunlardır:

- IIS olmadan var olan bir sunucu grubu gibi IIS 'nin kullanılamadığı veya istenmediğinde ortamlar.
- IIS 'nin performans ek yükünün önlenebilir olması gerekir.
- SignalR işlevselliği, bir Windows hizmeti, Azure Worker rolü veya başka bir işlemde çalışan mevcut bir uygulamaya eklenir.

Bir çözüm, performans nedenleriyle kendi kendine ana bilgisayar olarak geliştiriliyorsa, performans avantajını belirleyebilmek için IIS 'de barındırılan uygulamayı da sınamanız önerilir.

Bu öğretici aşağıdaki bölümleri içerir:

- [Sunucu oluşturuluyor](#server)
- [Bir JavaScript istemcisiyle sunucuya erişme](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>Sunucu oluşturuluyor

Bu öğreticide, bir konsol uygulamasında barındırılan bir sunucu oluşturacaksınız, ancak sunucu, Windows hizmeti veya Azure çalışan rolü gibi herhangi bir işlem sıralaması içinde barındırılabilir. Bir Windows hizmetinde bir SignalR sunucusunu barındırmak için örnek kod için, bkz. [bir Windows hizmetinde kendi kendine barındırma SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).

1. Yönetici ayrıcalıklarıyla Visual Studio 2013 açın. **Dosya**, **Yeni proje**' yi seçin. **Şablonlar** bölmesindeki **görsel C#**  düğümü altında **Windows** ' u seçin ve **konsol uygulaması** şablonunu seçin. "SignalRSelfHost" adlı yeni projeyi adlandırın ve **Tamam**' a tıklayın.

    ![](tutorial-signalr-self-host/_static/image1.png)
2. **Araçlar** > **nuget** Paket Yöneticisi > **Paket Yöneticisi konsolu**' nu seçerek NuGet Paket Yöneticisi konsolunu açın.
3. Paket Yöneticisi konsolunda aşağıdaki komutu girin:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    Bu komut, SignalR 2 Self-Host kitaplıklarını projeye ekler.
4. Paket Yöneticisi konsolunda aşağıdaki komutu girin:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    Bu komut, Microsoft. Owin. CORS kitaplığını projeye ekler. Bu kitaplık, SignalR barındıran uygulamalar ve farklı etki alanlarında bir Web sayfası istemcisi için gerekli olan etki alanları arası destek için kullanılacaktır. SignalR sunucusunu ve Web istemcisini farklı bağlantı noktalarında barındırabileceksiniz, bu, bu bileşenler arasındaki iletişim için etki alanları arası iletişim için etkinleştirilmesi gerektiği anlamına gelir.
5. Program.cs içeriğini aşağıdaki kodla değiştirin.

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    Yukarıdaki kod üç sınıf içerir:

    - **Program**, yürütmenin birincil yolunu tanımlayan **Main** yöntemi de dahil. Bu yöntemde, **Başlangıç** türü bir Web UYGULAMASı belirtilen URL 'de başlatılır (`http://localhost:8080`). Uç noktada güvenlik gerekliyse, SSL uygulanabilir. Daha fazla bilgi için bkz. [nasıl yapılır: SSL sertifikası Ile bağlantı noktası yapılandırma](https://msdn.microsoft.com/library/ms733791.aspx) .
    - **Başlangıç**, SignalR Server için yapılandırmayı içeren sınıf (Bu öğreticinin kullandığı tek yapılandırma `UseCors`) ve `MapSignalR`çağrısı, projedeki tüm Hub nesneleri için yollar oluşturur.
    - Uygulamanın istemcilere sağlayacağız SignalR hub sınıfı olan **Myhub**. Bu sınıf tek bir yönteme **sahiptir ve istemcileri, diğer**tüm bağlı istemcilere bir ileti yayınlamak için çağıracaktır.
6. Uygulamayı derleyin ve çalıştırın. Sunucunun çalıştırıldığı adresin bir konsol penceresinde gösterilmesi gerekir.

    ![](tutorial-signalr-self-host/_static/image2.png)
7. Yürütme `System.Reflection.TargetInvocationException was unhandled`özel durumla başarısız olursa, Visual Studio 'Yu yönetici ayrıcalıklarıyla yeniden başlatmanız gerekir.
8. Sonraki bölüme geçmeden önce uygulamayı durdurun.

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>Bir JavaScript istemcisiyle sunucuya erişme

Bu bölümde, Başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md)aynı JavaScript istemcisini kullanacaksınız. İstemcide yalnızca bir değişiklik yapacağız. Bu, hub URL 'sini açıkça tanımlamak için kullanılır. Şirket içinde barındırılan bir uygulamayla, sunucu bağlantı URL 'siyle aynı adreste olmayabilir (ters proxy 'ler ve yük dengeleyiciler nedeniyle), URL 'nin açıkça tanımlanması gerekir.

1. **Çözüm Gezgini**, çözüme sağ tıklayın ve **Ekle**, **Yeni proje**' yi seçin. **Web** düğümünü seçin ve **ASP.NET Web uygulaması** şablonunu seçin. Projeyi "JavascriptClient" olarak adlandırın ve **Tamam**' a tıklayın.

    ![](tutorial-signalr-self-host/_static/image3.png)
2. **Boş** şablonu seçin ve kalan seçenekleri seçilmemiş olarak bırakın. **Proje oluştur**' u seçin.

    ![](tutorial-signalr-self-host/_static/image4.png)
3. Paket Yöneticisi konsolunda, **varsayılan proje** açılır penceresinde "JavascriptClient" projesini seçin ve aşağıdaki komutu yürütün:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    Bu komut, istemcisinde ihtiyacınız olan SignalR ve JQuery kitaplıklarını yükleme.
4. Projenize sağ tıklayın ve **Ekle**, **Yeni öğe**' yi seçin. **Web** düğümünü SEÇIN ve HTML sayfası ' nı seçin. Sayfayı **default. html**olarak adlandırın.

    ![](tutorial-signalr-self-host/_static/image5.png)
5. Yeni HTML sayfasının içeriğini aşağıdaki kodla değiştirin. Buradaki betik başvurularının, projenin betikler klasöründeki betiklerin eşleştiğini doğrulayın.

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    Aşağıdaki kod (Yukarıdaki kod örneğinde vurgulanan), başlangıç öğreticisinde (kodu SignalR sürüm 2 Beta 'ya yükseltmenin yanı sıra) kullanılan istemciye yaptığınız bir ektir. Bu kod satırı, sunucuda SignalR için temel bağlantı URL 'sini açık olarak ayarlar.

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. Çözüme sağ tıklayın ve **Başlangıç projelerini ayarla...** seçeneğini belirleyin. **Birden çok başlangıç projesi** radyo düğmesini seçin ve her Iki projenin **eylemini** **Başlat**olarak ayarlayın.

    ![](tutorial-signalr-self-host/_static/image6.png)
7. "Default. html" öğesine sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.
8. Uygulamayı çalıştırın. Sunucu ve sayfa başlatılır. Sayfa sunucu başlatılmadan önce yüklenirse Web sayfasını yeniden yüklemeniz gerekebilir (veya hata ayıklayıcıda **devam et** ' i seçin).
9. Tarayıcıda, sorulduğunda bir Kullanıcı adı girin. Sayfanın URL 'sini başka bir tarayıcı sekmesine veya pencereye kopyalayın ve farklı bir Kullanıcı adı belirtin. Başlangıç öğreticisinde olduğu gibi, bir tarayıcı bölmesinden diğerine ileti gönderebileceksiniz.
