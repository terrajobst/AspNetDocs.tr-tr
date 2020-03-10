---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Denetleyici ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 194a8a7398e163f0c37164a8724f98b16444984b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615810"
---
# <a name="adding-a-controller"></a>Denetleyici Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [Tutorial Note](index.md)]

MVC, *Model-View-Controller*için temsil eder. MVC, iyi şekilde tasarlanmış ve bakımı kolay olan uygulamalar geliştirmeye yönelik bir modeldir. MVC tabanlı uygulamalar şunları içerir:

- **K** odels: uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.
- **V** ıews: uygulamanızın HTML yanıtlarını dinamik olarak oluşturmak Için kullandığı şablon dosyaları.
- **C** ontrolleyiciler: gelen tarayıcı isteklerini işleyen, model verilerini alan ve tarayıcıya yanıt döndüren şablonları görüntüleme gibi sınıflar.

Bu öğretici serisinde bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

Bir denetleyici sınıfı oluşturarak başlayalım. **Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.

![](adding-a-controller/_static/image1.png)

**Yapı Iskelesi Ekle** Iletişim kutusunda **MVC 5 denetleyici-boş**' ya tıklayın ve ardından **Ekle**' ye tıklayın.

![](adding-a-controller/_static/image2.png)  

Yeni denetleyicinizi "Merhaba Dünya denetleyicisi" olarak adlandırın ve **Ekle**' ye tıklayın.

![denetleyici Ekle](adding-a-controller/_static/image3.png)

**Çözüm Gezgini** , *HelloWorldController.cs* adlı yeni bir dosya ve *views\helloworld*adlı yeni bir klasör oluşturulduğunu fark edin. Denetleyici IDE 'de açıktır.

![](adding-a-controller/_static/image4.png)

Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Denetleyici yöntemleri bir örnek olarak HTML dizesi döndürür. Denetleyicinin adı `HelloWorldController` ve ilk yöntem `Index`olarak adlandırılmıştır. Bir tarayıcıdan çağıralım. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcıda, adres çubuğundaki yola &quot;HelloWorld&quot; ekleyin. (Örneğin, aşağıdaki çizimde `http://localhost:1234/HelloWorld.`) Tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca birkaç HTML döndürdüyordu ve!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan URL yönlendirme mantığı, çağrılacak kodu belirlemek için aşağıdaki gibi bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

*Uygulama\_start/RouteConfig. cs* dosyasında yönlendirme biçimini ayarlarsınız.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

Uygulamayı çalıştırdığınızda ve herhangi bir URL kesimini sağlamadığınızda, varsayılan olarak "giriş" denetleyicisi ve Yukarıdaki kodun varsayılanlar bölümünde belirtilen "Dizin" eylem yöntemi olur.

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle, */HelloWorld* `HelloWorldController` sınıfıyla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `HelloWorldController` sınıfının `Index` yönteminin yürütülmesine neden olur. Yalnızca */HelloWorld* 'e göz attık ve `Index` yöntemi varsayılan olarak kullanılmış olduğuna dikkat edin. Bunun nedeni, `Index` adlı bir yöntemin, açıkça belirtilmemişse bir denetleyicide çağrılacak olan varsayılan yöntemdir. URL segmentinin (`Parameters`) üçüncü bölümü rota verileri içindir. Bu öğreticide daha sonra rota verilerini inceleyeceğiz.

`http://localhost:xxxx/HelloWorld/Welcome` adresine gidin. `Welcome` yöntemi çalışır ve &quot;dizeyi döndürür. Bu yöntem,...&quot;hoş geldiniz eylemi yöntemidir. Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`. Bu URL için, denetleyici `HelloWorld` ve `Welcome` Action yöntemidir. URL 'nin `[Parameters]` parçasını henüz kullanmadınız.

![](adding-a-controller/_static/image6.png)

URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*). `Welcome` yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Kodun, bu parametre için hiçbir C# değer geçirilmemişse, `numTimes` parametresinin varsayılan olarak 1 ' e olacağını belirtmek için isteğe bağlı parametre özelliğini kullandığını unutmayın.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> Güvenlik notumu: Yukarıdaki kod, uygulamayı kötü amaçlı girişten korumak için [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) kullanır (yani JavaScript). Daha fazla bilgi için bkz. [nasıl yapılır: DIZELERE HTML kodlaması uygulayarak bir Web uygulamasındaki betiklere karşı koruma](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).

 Uygulamanızı çalıştırın ve örnek URL 'ye (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) gidin. URL 'de `name` ve `numtimes` için farklı değerler deneyebilirsiniz. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image7.png)

Yukarıdaki örnekte, URL segmenti (`Parameters`) kullanılmaz, `name` ve `numTimes` parametreleri [sorgu dizeleri](http://en.wikipedia.org/wiki/Query_string)olarak geçirilir. ? işareti (soru işareti) Yukarıdaki URL 'de bir ayırıcıdır ve sorgu dizeleri aşağıdaki gibi olur. &amp; karakter Sorgu dizelerini ayırır.

Welcome metodunu aşağıdaki kodla değiştirin:

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

Uygulamayı çalıştırın ve şu URL 'YI girin: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

Bu kez, üçüncü URL segmenti yol parametresiyle eşleştirildiği `ID.` `Welcome` Action yöntemi `RegisterRoutes` yöntemindeki URL belirtimiyle eşleşen bir parametre (`ID`) içerir.

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC uygulamalarında, parametreleri sorgu dizeleri olarak geçirmeden, parametreleri yönlendirme verileri (yukarıda ID ile yaptığımız gibi) olarak geçirmek daha tipik bir yoldur. Ayrıca, URL 'de yönlendirme verileri olarak `name` ve `numtimes` parametreleri içine geçirmek üzere bir yol ekleyebilirsiniz. *App\_Start\RouteConfig.cs* dosyasına "Merhaba" yolunu ekleyin:

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

Uygulamayı çalıştırın ve `/localhost:XXX/HelloWorld/Welcome/Scott/3`gidin.

![](adding-a-controller/_static/image9.png)

Birçok MVC uygulaması için, varsayılan yol sorunsuz şekilde çalışıyor. Bu öğreticide daha sonra model cildi kullanarak veri geçireceğini öğrenirsiniz ve bunun için varsayılan yolu değiştirmeniz gerekmez.

Bu örneklerde denetleyici, MVC 'nin &quot;VC&quot; bölümünü (yani, görünüm ve denetleyici) yapıyor. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Şimdi bunu nasıl yapadığımızda bakalım.

> [!div class="step-by-step"]
> [Önceki](getting-started.md)
> [İleri](adding-a-view.md)
