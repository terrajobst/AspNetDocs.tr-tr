---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Birim testi SignalR uygulamaları | Microsoft Docs
author: bradygaster
description: Bu makalede, SignalR 2,0 'nin birim testi özelliklerinin nasıl kullanılacağı açıklanır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578675"
---
# <a name="unit-testing-signalr-applications"></a>SignalR Uygulamalarına Birim Testi Yapma

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu makalede, SignalR 2 ' nin birim testi özelliklerini kullanma açıklanmaktadır.
>
> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>Birim testi SignalR uygulamaları

SignalR uygulamanız için birim testleri oluşturmak için SignalR 2 ' deki birim testi özelliklerini kullanabilirsiniz. SignalR 2, test için hub yöntemlerinizi taklit etmek üzere bir sahte nesne oluşturmak için kullanılabilecek olan [IHV Ubcallerconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) arabirimini içerir.

Bu bölümde, [XUnit.net](https://github.com/xunit/xunit) ve [moq](https://github.com/Moq/moq4)kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için birim testleri ekleyeceksiniz.

XUnit.net, testi denetlemek için kullanılacaktır; MOQ, test için bir [sahte](http://en.wikipedia.org/wiki/Mock_object) nesne oluşturmak üzere kullanılacaktır. İsterseniz, diğer sahte işlem çerçeveleri kullanılabilir; [Ndeğiştirme](http://nsubstitute.github.io/) de iyi bir seçimdir. Bu öğreticide, bir arabirim kullanılarak, bir `dynamic` nesnesi (.NET Framework 4 ' te tanıtılan) ve ikincisi kullanarak, sahte nesnenin nasıl ayarlanacağı gösterilmektedir.

### <a name="contents"></a>İçindekiler

Bu öğretici aşağıdaki bölümleri içerir.

- [Dinamik ile birim testi](#dynamic)
- [Türe göre birim testi](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>Dinamik ile birim testi

Bu bölümde, dinamik bir nesne kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için bir birim testi ekleyeceksiniz.

1. Visual Studio 2013 için [xUnit Çalıştırıcısı uzantısını](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) yükler.
2. [Kullanmaya başlama öğreticisini](../getting-started/tutorial-getting-started-with-signalr.md)ya da tamamlanmış uygulamayı [MSDN kod galerisinden](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)indirin.
3. Başlarken uygulamasının indirme sürümünü kullanıyorsanız, **Paket Yöneticisi konsolu 'nu** açın ve **geri yükle** ' ye tıklayarak SignalR paketini projeye ekleyin.

    ![Paketleri geri yükle](unit-testing-signalr-applications/_static/image1.png)
4. Birim testi için çözüme bir proje ekleyin. **Çözüm Gezgini** çözümünüzde çözümünüze sağ tıklayın ve **Ekle**, **Yeni proje..** . öğesini seçin. **C#** Düğüm altında **Windows** düğümünü seçin. **Sınıf kitaplığı**' nı seçin. Yeni projeyi **Testlibrary** olarak adlandırın ve **Tamam**' a tıklayın.

    ![Test kitaplığı oluştur](unit-testing-signalr-applications/_static/image2.png)
5. Test kitaplığı projesine SignalRChat projesine bir başvuru ekleyin. **Testlibrary** projesine sağ tıklayın ve **Ekle**, **başvuru..** . seçeneğini belirleyin. **Çözüm** düğümü altındaki **Projeler** düğümünü seçin ve **signalrchat**' i kontrol edin. **Tamam**’a tıklayın.

    ![Proje başvurusu Ekle](unit-testing-signalr-applications/_static/image3.png)
6. SignalR, moq ve XUnit paketlerini **Testlibrary** projesine ekleyin. **Paket Yöneticisi konsolunda**, **varsayılan proje** açılan menüsünü **testlibrary**olarak ayarlayın. Konsol penceresinde aşağıdaki komutları çalıştırın:

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Paketleri yükler](unit-testing-signalr-applications/_static/image4.png)
7. Test dosyasını oluşturun. **Testlibrary** projesine sağ tıklayın ve **Ekle...** **' ye tıklayın.** Yeni sınıfı **Tests.cs**olarak adlandırın.
8. Tests.cs içeriğini aşağıdaki kodla değiştirin.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    Yukarıdaki kodda, bir test istemcisi, IQ kitaplığı 'ndan (SignalR 2,1 ' [de tür parametresi](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) için `dynamic` atayın), [moq](https://github.com/Moq/moq4) kitaplığındaki `Mock` nesnesi kullanılarak oluşturulur. `IHubCallerConnectionContext` arabirimi, istemcisinde yöntemleri çağırmada kullandığınız ara sunucu nesnesidir. `broadcastMessage` işlevi daha sonra, `ChatHub` sınıfı tarafından çağrılabilmesi için, sahte istemci için tanımlanmıştır. Test motoru daha sonra `ChatHub` sınıfının `Send` yöntemini çağırır ve bu da moclenmiş `broadcastMessage` işlevini çağırır.
9. **F6**tuşuna basarak çözümü oluşturun.
10. Birim testini çalıştırın. Visual Studio 'da **Test**, **Windows**, **Test Gezgini**' ni seçin. Test Gezgini penceresinde, **Hubsaremockableviadynamıc** öğesine sağ tıklayın ve **Seçili Testleri Çalıştır**' ı seçin.

    ![Test Gezgini](unit-testing-signalr-applications/_static/image5.png)
11. Testin test Gezgini penceresindeki alt bölmeyi denetleyerek geçtiğini doğrulayın. Pencerede testin geçtiğini gösterir.

    ![Test geçildi](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>Türe göre birim testi

Bu bölümde, test edilecek yöntemi içeren bir arabirimi kullanarak başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulama için bir test ekleyeceksiniz.

1. Yukarıdaki [dinamik öğreticiyle birim testinde](#dynamic) 1-7 arasındaki adımları uygulayın.
2. Tests.cs içeriğini aşağıdaki kodla değiştirin.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    Yukarıdaki kodda, test altyapısının bir sahte istemci oluşturması için `broadcastMessage` yönteminin imzasını tanımlayan bir arabirim oluşturulur. Daha sonra bir sahte istemci, [ıubcallerconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) türünde `Mock` nesnesi kullanılarak oluşturulur (signalr 2,1 ' de tür parametresi için `dynamic` atayın.) `IHubCallerConnectionContext` arabirimi, istemcisinde yöntemleri çağırmada kullandığınız ara sunucu nesnesidir.

    Test daha sonra bir `ChatHub`örneği oluşturur ve sonra `broadcastMessage` yönteminin bir sahte sürümünü oluşturur ve bu da hub üzerinde `Send` yöntemi çağırarak çağrılır.
3. **F6**tuşuna basarak çözümü oluşturun.
4. Birim testini çalıştırın. Visual Studio 'da **Test**, **Windows**, **Test Gezgini**' ni seçin. Test Gezgini penceresinde, **Hubsaremockableviadynamıc** öğesine sağ tıklayın ve **Seçili Testleri Çalıştır**' ı seçin.

    ![Test Gezgini](unit-testing-signalr-applications/_static/image7.png)
5. Testin test Gezgini penceresindeki alt bölmeyi denetleyerek geçtiğini doğrulayın. Pencerede testin geçtiğini gösterir.

    ![Test geçildi](unit-testing-signalr-applications/_static/image8.png)
