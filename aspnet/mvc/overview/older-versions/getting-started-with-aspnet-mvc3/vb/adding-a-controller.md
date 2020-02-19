---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: Denetleyici ekleme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457420"
---
# <a name="adding-a-controller-vb"></a>Denetleyici Ekleme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/adding-a-controller.md) geçin.

MVC, *Model-View-Controller*için temsil eder. MVC, her parçanın ayrı bir sorumluluğu olması gibi uygulamalar geliştirmeye yönelik bir modeldir:

- Model: uygulamanızın verileri.
- Görünümler: uygulamanızın, dinamik olarak HTML yanıtları oluşturmak için kullanacağı şablon dosyaları.
- Denetleyiciler: uygulamaya gelen URL isteklerini işleyen sınıflar, model verilerini alır ve ardından istemciye yanıt işleyen şablonları görüntüler.

Bu öğreticide bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

**Çözüm Gezgini** ' de *denetleyiciler* klasörüne sağ tıklayıp **Denetleyici Ekle**' yi seçerek yeni bir denetleyici oluşturun.

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

Yeni denetleyicinizi &quot;Merhaba Worldcontroller&quot; adlandırın ve **Ekle**' ye tıklayın.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

**Çözüm Gezgini** , *HelloWorldController.cs* adlı sizin için yeni bir DOSYANıN oluşturulduğunu ve dosyanın IDE 'de açık olduğunu görürsünüz.

Yeni `public class HelloWorldController` bloğunun içinde, aşağıdaki kod gibi iki yeni yöntem oluşturun. Bir örnek olarak denetleyiciye doğrudan bir HTML dizesi geri döneceğiz.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

Denetleyicinizin adı `HelloWorldController` ve yeni yönteminiz `Index`olarak adlandırılmıştır. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcınız başlatıldıktan sonra, adres çubuğundaki yola &quot;HelloWorld&quot; ekleyin. (Bilgisayarımda `http://localhost:43246/HelloWorld`) Tarayıcınız aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca bazı HTML döndürdük ve!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan eşleme mantığı, hangi kodun çağrılacağını denetlemek için şöyle bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle, */HelloWorld* `HelloWorldController` sınıfıyla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `HelloWorldController` sınıfının `Index` yönteminin yürütülmesine neden olur. Yukarıda yalnızca */HelloWorld* ' i ziyaret ettiğimiz ve `Index` yönteminin varsayılan olarak kullanıldığını fark etmiş olun. Bunun nedeni, `Index` adlı bir yöntemin, açıkça belirtilmemişse bir denetleyicide çağrılacak olan varsayılan yöntemdir.

`http://localhost:xxxx/HelloWorld/Welcome` adresine gidin. `Welcome` yöntemi çalışır ve &quot;dizeyi döndürür. Bu yöntem,...&quot;hoş geldiniz eylemi yöntemidir. Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`. Bu URL için, denetleyici `HelloWorld` ve `Welcome` yöntemidir. URL 'nin `[Parameters]` parçasını henüz kullanmadınız.

![](adding-a-controller/_static/image6.png)

URL 'den denetleyiciye bir miktar parametre bilgisi geçirebilmemiz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*). `Welcome` yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Bu parametre için hiçbir değer geçirilmemişse `numTimes` parametresinin varsayılan olarak 1 ' e olacağını belirtmek için VB isteğe bağlı parametre özelliğini kullandığımızda unutmayın.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

Uygulamanızı çalıştırın ve `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`gidin **.** `name` ve `numtimes`için farklı değerler deneyebilirsiniz. Sistem, adres çubuğundaki sorgu dizinizdeki adlandırılmış parametreleri yöntemdeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image7.png)

Her iki örnekte de denetleyici, bu, görünüm ve denetleyicinin çalıştığı, MVC 'nin VC bölümünü yapıyor. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Bu, bunu nasıl yapabiliriz bakalım.

> [!div class="step-by-step"]
> [Önceki](intro-to-aspnet-mvc-3.md)
> [İleri](adding-a-view.md)
