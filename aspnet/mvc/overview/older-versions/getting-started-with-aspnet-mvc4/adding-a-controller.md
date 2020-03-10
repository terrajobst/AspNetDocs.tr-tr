---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: Denetleyici ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599843"
---
# <a name="adding-a-controller"></a>Denetleyici Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

MVC, *Model-View-Controller*için temsil eder. MVC, iyi şekilde tasarlanmış ve bakımı kolay olan uygulamalar geliştirmeye yönelik bir modeldir. MVC tabanlı uygulamalar şunları içerir:

- **K** odels: uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.
- **V** ıews: uygulamanızın HTML yanıtlarını dinamik olarak oluşturmak Için kullandığı şablon dosyaları.
- **C** ontrolleyiciler: gelen tarayıcı isteklerini işleyen, model verilerini alan ve tarayıcıya yanıt döndüren şablonları görüntüleme gibi sınıflar.

Bu öğretici serisinde bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

Bir denetleyici sınıfı oluşturarak başlayalım. **Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Denetleyici Ekle**' yi seçin.

![](adding-a-controller/_static/image1.png)

Yeni denetleyicinizi HelloWorldController&quot;&quot;adlandırın. Varsayılan şablonu **boş MVC denetleyicisi** olarak bırakın ve **Ekle**' ye tıklayın.

![denetleyici Ekle](adding-a-controller/_static/image2.png)

**Çözüm Gezgini** , *HelloWorldController.cs*adlı yeni bir dosyanın oluşturulduğunu fark edin. Dosya IDE 'de açıktır.

![](adding-a-controller/_static/image3.png)

Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Denetleyici yöntemleri bir örnek olarak HTML dizesi döndürür. Denetleyicinin adı `HelloWorldController` ve yukarıdaki ilk yöntem `Index`olarak adlandırılmıştır. Bir tarayıcıdan çağıralım. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcıda, adres çubuğundaki yola &quot;HelloWorld&quot; ekleyin. (Örneğin, aşağıdaki çizimde `http://localhost:1234/HelloWorld.`) Tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca birkaç HTML döndürdüyordu ve!

![](adding-a-controller/_static/image4.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan URL yönlendirme mantığı, çağrılacak kodu belirlemek için aşağıdaki gibi bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle, */HelloWorld* `HelloWorldController` sınıfıyla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `HelloWorldController` sınıfının `Index` yönteminin yürütülmesine neden olur. Yalnızca */HelloWorld* 'e göz attık ve `Index` yöntemi varsayılan olarak kullanılmış olduğuna dikkat edin. Bunun nedeni, `Index` adlı bir yöntemin, açıkça belirtilmemişse bir denetleyicide çağrılacak olan varsayılan yöntemdir.

`http://localhost:xxxx/HelloWorld/Welcome` adresine gidin. `Welcome` yöntemi çalışır ve &quot;dizeyi döndürür. Bu yöntem,...&quot;hoş geldiniz eylemi yöntemidir. Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`. Bu URL için, denetleyici `HelloWorld` ve `Welcome` Action yöntemidir. URL 'nin `[Parameters]` parçasını henüz kullanmadınız.

![](adding-a-controller/_static/image5.png)

URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*). `Welcome` yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Kodun, bu parametre için hiçbir C# değer geçirilmemişse, `numTimes` parametresinin varsayılan olarak 1 ' e olacağını belirtmek için isteğe bağlı parametre özelliğini kullandığını unutmayın.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

Uygulamanızı çalıştırın ve örnek URL 'ye (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`gidin. URL 'de `name` ve `numtimes` için farklı değerler deneyebilirsiniz. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image6.png)

Bu örneklerde, denetleyici MVC 'nin &quot;VC&quot; bölümünü (yani, görünüm ve denetleyici) yapıyor. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Şimdi bunu nasıl yapadığımızda bakalım.

> [!div class="step-by-step"]
> [Önceki](intro-to-aspnet-mvc-4.md)
> [İleri](adding-a-view.md)
