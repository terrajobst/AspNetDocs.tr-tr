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
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810771"
---
# <a name="adding-a-controller"></a>Denetleyici Ekleme

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

[!INCLUDE [Tutorial Note](sample/code-location.md)]

MVC, *Model-View-Controller*için temsil eder. MVC, iyi şekilde tasarlanmış ve bakımı kolay olan uygulamalar geliştirmeye yönelik bir modeldir. MVC tabanlı uygulamalar şunları içerir:

- **A** odels: Uygulamanın verilerini temsil eden ve bu veriler için iş kurallarını zorlamak üzere doğrulama mantığını kullanan sınıflar.
- **V** ıews: Uygulamanızın, dinamik olarak HTML yanıtları oluşturmak için kullandığı şablon dosyaları.
- **C** ontrolleyiciler: Gelen tarayıcı isteklerini işleyen sınıflar, model verilerini alır ve tarayıcıya yanıt döndüren şablonları görüntüle seçeneğini belirtir.

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

Denetleyici yöntemleri bir örnek olarak HTML dizesi döndürür. Denetleyici adlandırılır `HelloWorldController` ve ilk yöntem adlandırılır `Index`. Bir tarayıcıdan çağıralım. Uygulamayı çalıştırın (F5 tuşuna basın veya CTRL + F5 tuşlarına basın). Tarayıcıda, adres çubuğundaki yola &quot;HelloWorld&quot; ekleyin. (Örneğin, aşağıdaki çizimde olduğu `http://localhost:1234/HelloWorld.`gibi), tarayıcıdaki sayfa aşağıdaki ekran görüntüsüne benzer şekilde görünür. Yukarıdaki yöntemde kod doğrudan bir dize döndürdü. Sisteme yalnızca birkaç HTML döndürdüyordu ve!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan URL yönlendirme mantığı, çağrılacak kodu belirlemek için aşağıdaki gibi bir biçim kullanır:

`/[Controller]/[ActionName]/[Parameters]`

*Uygulama\_başlangıç/routeconfig. cs* dosyasında yönlendirme biçimini ayarlarsınız.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

Uygulamayı çalıştırdığınızda ve herhangi bir URL kesimini sağlamadığınızda, varsayılan olarak "giriş" denetleyicisi ve Yukarıdaki kodun varsayılanlar bölümünde belirtilen "Dizin" eylem yöntemi olur.

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle */HelloWorld* `HelloWorldController` sınıfla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle */HelloWorld/Index* `Index` `HelloWorldController` sınıfın yönteminin yürütülmesine neden olur. Yalnızca */HelloWorld* öğesine göz atabildiğimiz ve `Index` yöntemin varsayılan olarak kullanıldığı konusunda dikkat edin. Bunun nedeni, bir yöntemi `Index` açıkça belirtilmediyse bir denetleyicide çağrılacak olan varsayılan yöntemdir. URL segmentinin ( `Parameters`) üçüncü bölümü rota verileri içindir. Bu öğreticide daha sonra rota verilerini inceleyeceğiz.

konumuna gözatın `http://localhost:xxxx/HelloWorld/Welcome`. Yöntemi çalışır ve bu karşılama eylemi yöntemi &quot;olan dizeyi döndürür... `Welcome` &quot;. Varsayılan MVC eşlemesi `/[Controller]/[ActionName]/[Parameters]`. Bu URL için denetleyici `HelloWorld` , ve `Welcome` eylem yöntemidir. URL 'nin bir `[Parameters]` bölümünü henüz kullanmadınız.

![](adding-a-controller/_static/image6.png)

URL 'den denetleyiciye bazı parametre bilgilerini geçirebilmeniz için örneği biraz daha değiştirelim (örneğin, */HelloWorld/Welcome? ad = Scott&amp;numtimes = 4*). `Welcome` Yönteminizi aşağıda gösterildiği gibi iki parametre içerecek şekilde değiştirin. Bu parametre için hiçbir değer geçirilmemişse, C# `numTimes` kodun varsayılan olarak 1 ' e sahip olacağını belirtmek için isteğe bağlı parametre özelliğini kullandığını unutmayın.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> Güvenlik Notno: Yukarıdaki kod, uygulamayı kötü amaçlı girişten korumak için [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) kullanır (yani JavaScript). Daha fazla bilgi için [nasıl yapılır: Dizelere](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)HTML kodlaması uygulayarak bir Web uygulamasındaki betiklere karşı koruma sağlar.

 Uygulamanızı çalıştırın ve örnek URL 'ye (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) gidin. URL 'de ve `name` `numtimes` için farklı değerler deneyebilirsiniz. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler.

![](adding-a-controller/_static/image7.png)

Yukarıdaki örnekte, `Parameters`URL segmenti () kullanılmaz `name` , ve `numTimes` parametreleri [sorgu dizeleri](http://en.wikipedia.org/wiki/Query_string)olarak geçirilir. İçin? (soru işareti) Yukarıdaki URL 'de bir ayırıcıdır ve sorgu dizeleri aşağıdaki gibi olur. &amp; Karakter Sorgu dizelerini ayırır.

Welcome metodunu aşağıdaki kodla değiştirin:

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

Uygulamayı çalıştırın ve aşağıdaki URL 'YI girin:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

Bu kez, üçüncü URL `ID.` segmenti, `RegisterRoutes` yöntemi içindeki URL belirtimiyle `Welcome` eşleşen bir parametreyi (`ID`) içeren yol parametresiyle eşleştirildiği zaman.

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

ASP.NET MVC uygulamalarında, parametreleri sorgu dizeleri olarak geçirmeden, parametreleri yönlendirme verileri (yukarıda ID ile yaptığımız gibi) olarak geçirmek daha tipik bir yoldur. Ayrıca, `name` `numtimes` URL 'ye yönlendirme verileri olarak hem hem de parametrelerini geçirmek için bir yol ekleyebilirsiniz. *App\_start\routeconfig.cs* dosyasına "Merhaba" yolunu ekleyin:

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

Uygulamayı çalıştırın ve konumuna gidin `/localhost:XXX/HelloWorld/Welcome/Scott/3`.

![](adding-a-controller/_static/image9.png)

Birçok MVC uygulaması için, varsayılan yol sorunsuz şekilde çalışıyor. Bu öğreticide daha sonra model cildi kullanarak veri geçireceğini öğrenirsiniz ve bunun için varsayılan yolu değiştirmeniz gerekmez.

Bu örneklerde, denetleyici MVC 'nin &quot;VC&quot; bölümünü yapıyor — yani, görünüm ve denetleyici çalışır. Denetleyici HTML 'i doğrudan döndürüyor. Normalde, kod için çok daha fazla hale geldiği için denetleyicilerin doğrudan HTML döndürmesini istemezsiniz. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Şimdi bunu nasıl yapadığımızda bakalım.

> [!div class="step-by-step"]
> [Önceki](getting-started.md)İleri
> [](adding-a-view.md)
