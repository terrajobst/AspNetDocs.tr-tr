---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: Denetleyici ekleme (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457849"
---
# <a name="adding-a-controller-c"></a>Denetleyici Ekleme (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.
> 
> 
> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.

MVC, *Model-View-Controller*için temsil eder. MVC, iyi şekilde tasarlanmış ve bakımı kolay uygulamalar geliştirmeye yönelik bir modeldir. MVC tabanlı uygulamalar şunları içerir:

- Denetleyiciler: uygulamaya gelen istekleri işleyen sınıflar, model verilerini alır ve ardından istemciye bir yanıt döndüren şablonları görüntüleme seçeneğini belirtir.
- Modeller: uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.
- Görünümler: uygulamanızın HTML yanıtlarını dinamik olarak oluşturmak için kullandığı şablon dosyaları.

Bu öğretici serisinde bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

Bir denetleyici sınıfı oluşturarak başlayalım. **Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Denetleyici Ekle**' yi seçin.

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

Yeni denetleyicinizi "Merhaba Dünya denetleyicisi" olarak adlandırın. Varsayılan şablonu **boş denetleyici** olarak bırakın ve **Ekle**' ye tıklayın.

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

**Çözüm Gezgini** , *HelloWorldController.cs*adlı yeni bir dosyanın oluşturulduğunu fark edin. Dosya IDE 'de açıktır.

![](adding-a-controller/_static/image5.png)

`public class HelloWorldController` bloğu içinde, aşağıdaki koda benzeyen iki yöntem oluşturun. Denetleyici bir örnek olarak HTML dizesi döndürür.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Denetleyicinizin adı `HelloWorldController` ve yukarıdaki ilk yöntem `Index`olarak adlandırılmıştır. Bir tarayıcıdan çağıralım. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcıda, adres çubuğundaki yola "HelloWorld" ekleyin. (Örneğin, aşağıdaki çizimde `http://localhost:43246/HelloWorld.`) Tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca birkaç HTML döndürdüyordu ve!

![](adding-a-controller/_static/image6.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan eşleme mantığı, hangi kodun çağıracağına belirlemek için şöyle bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle, */HelloWorld* `HelloWorldController` sınıfıyla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `HelloWorldController` sınıfının `Index` yönteminin yürütülmesine neden olur. Yalnızca */HelloWorld* 'e göz attık ve `Index` yöntemi varsayılan olarak kullanılmış olduğuna dikkat edin. Bunun nedeni, `Index` adlı bir yöntemin, açıkça belirtilmemişse bir denetleyicide çağrılacak olan varsayılan yöntemdir.

`http://localhost:xxxx/HelloWorld/Welcome` adresine gidin. `Welcome` yöntemi çalışır ve "Bu hoş geldiniz eylemi yöntemi..." dizesini döndürür. Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`. Bu URL için, denetleyici `HelloWorld` ve `Welcome` Action yöntemidir. URL 'nin `[Parameters]` parçasını henüz kullanmadınız.

![](adding-a-controller/_static/image7.png)

URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*). `Welcome` yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Kodun, bu parametre için hiçbir C# değer geçirilmemişse, `numTimes` parametresinin varsayılan olarak 1 ' e olacağını belirtmek için isteğe bağlı parametre özelliğini kullandığını unutmayın.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

Uygulamanızı çalıştırın ve örnek URL 'ye (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`gidin. URL 'de `name` ve `numtimes` için farklı değerler deneyebilirsiniz. Sistem, adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden, yönteminizin içindeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image8.png)

Bu örneklerde, denetleyici MVC 'nin "VC" bölümünü (yani, görünüm ve denetleyici çalışır) yapıyor. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Şimdi bunu nasıl yapadığımızda bakalım.

> [!div class="step-by-step"]
> [Önceki](intro-to-aspnet-mvc-3.md)
> [İleri](adding-a-view.md)
