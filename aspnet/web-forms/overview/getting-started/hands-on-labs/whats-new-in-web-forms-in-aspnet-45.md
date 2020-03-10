---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4,5 ' de Web Forms yenilikler | Microsoft Docs
author: rick-anderson
description: Yeni ASP.NET Web Forms sürümü, verilerle çalışırken kullanıcı deneyimini iyileştirmeye odaklanan birkaç geliştirme sunar. Önceki sürümlerinde...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525734"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>ASP.NET 4.5 Sürümünde Web Forms Yenilikleri

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

> Yeni ASP.NET Web Forms sürümü, verilerle çalışırken kullanıcı deneyimini iyileştirmeye odaklanan birkaç geliştirme sunar.
> 
> Önceki Web Forms sürümlerinde, bir nesne üyesinin değerini göstermek için veri bağlamayı kullanırken, bind () veya eval () veri bağlama ifadeleri kullandınız. Yeni bir ASP.NET sürümünde, yeni bir ItemType özelliği kullanarak bir denetimin ne tür veriye bağlandığını bildirebileceksiniz. Bu özelliğin ayarlanması, Visual Studio geliştirme deneyiminin IntelliSense, üye gezintisi ve derleme zamanı denetimi gibi tüm avantajlarından yararlanmak için türü kesin belirlenmiş bir değişken kullanmanıza imkan sağlar.
> 
> Veri bağlantılı denetimlerle artık, veri seçme, güncelleştirme, silme ve ekleme için kendi özel yöntemlerinizi de belirtebilir ve bu da sayfa denetimleri ile uygulama mantığınızın etkileşimini basitleştirir. Ayrıca, ASP.NET 'e model bağlama özellikleri eklenmiştir, bu da sayfadaki verileri doğrudan yöntem türü parametrelerine eşleyebileceğiniz anlamına gelir.
> 
> Kullanıcı girişinin doğrulanması, Web Forms en son sürümü ile de daha kolay olmalıdır. Artık, **System. ComponentModel. datanot** ad alanındaki doğrulama öznitelikleriyle model sınıflarınıza açıklama ekleyebilir ve tüm site denetimlerinizin bu bilgileri kullanarak Kullanıcı girişini doğrulamasını isteyebilirsiniz. Web Forms içindeki istemci tarafı doğrulaması artık jQuery ile tümleştirilerek, temizleyici istemci tarafı kodu ve engellemeyen JavaScript özellikleri sağlanır.
> 
> İstek doğrulama alanında, uygulamalarınızın belirli bölümleri için istek doğrulamayı seçmeli olarak devre dışı bırakmayı kolaylaştırmak veya geçersiz kılınan istek verilerini okumak daha kolay hale getirmek için geliştirmeler yapılmıştır.
> 
> HTML5 'in yeni özelliklerinden yararlanmak için Web Forms sunucu denetimlerine bazı geliştirmeler yapılmıştır:
> 
> - TextBox denetiminin TextMode özelliği, e-posta, DateTime vb. gibi yeni HTML5 giriş türlerini destekleyecek şekilde güncelleştirilmiştir.
> - FileUpload denetimi artık bu HTML5 özelliğini destekleyen tarayıcılardan birden çok dosya yüklemeyi destekliyor.
> - Doğrulayıcı denetimleri artık HTML5 giriş öğelerinin doğrulanmasını destekliyor.
> - Bir URL 'YI temsil eden öznitelikleri olan yeni HTML5 öğeleri artık runat =&quot;Server&quot;desteklemektedir. Sonuç olarak, uygulama kökünü temsil etmek için ~ işleci gibi URL yollarında ASP.NET kurallarını kullanabilirsiniz (örneğin, &lt;video runat =&quot;Server&quot; src =&quot;~/MyVideo.exe&quot;&gt;&lt;/video&gt;).
> - UpdatePanel denetimi HTML5 giriş alanlarının nakledilmesini destekleyecek şekilde düzeltildi.
> 
> Resmi ASP.NET portalında, ASP.NET WebForms 4,5 ' deki yeni özelliklerin daha fazla örneğini bulabilirsiniz: [ASP.NET 4,5 ve Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385) yenilikleri
> 
> Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Kesin türü belirtilmiş veri bağlama ifadeleri kullanın
- Web Forms yeni model bağlama özelliklerini kullan
- Sayfa verilerini arka plan kod yöntemlerine eşlemek için değer sağlayıcıları kullanın
- Kullanıcı girişi doğrulaması için veri ek açıklamalarını kullanma
- Web Forms içinde jQuery ile obtrusive istemci tarafı doğrulamasından yararlanın
- Ayrıntılı istek doğrulaması Uygula
- Web Forms zaman uyumsuz sayfa işleme Uygula

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

**Kod parçacıklarını yükleme**

Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır. Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Alıştırma 1: ASP.NET Web Forms model bağlama](#Exercise1)
2. [Alıştırma 2: veri doğrulama](#Exercise2)
3. [Alıştırma 3: ASP.NET Web Forms zaman uyumsuz sayfa Işleme](#Exercise3)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>Alıştırma 1: ASP.NET Web Forms model bağlama

Yeni ASP.NET Web Forms sürümü, verilerle çalışırken deneyimin geliştirilmesine odaklanan birkaç geliştirme sunar. Bu alıştırmada, kesin tür belirtilmiş veri denetimleri ve model bağlama hakkında bilgi edineceksiniz.

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>Görev 1-türü kesin belirlenmiş veri bağlamaları kullanma

Bu görevde, ASP.NET 4,5 ' de bulunan, kesin olarak belirlenmiş yeni bağlamaları keşfedeceksiniz.

1. **Kaynak/Ex1-ModelBinding/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Customers. aspx** sayfasını açın. Ana denetime numaralanmış olmayan bir liste yerleştirin ve her müşteriyi listelemek için içine bir yineleyici denetimi ekleyin. Yineleyicisi adını aşağıdaki kodda gösterildiği gibi **Customersrepeater** olarak ayarlayın.

    Web Forms önceki sürümlerinde, veri bağlama yaptığınız bir nesne üzerindeki bir üyenin değerini göstermek için veri bağlamayı kullanırken, bir veri bağlama ifadesi kullanın ve bu, üyenin adını bir dize olarak geçirerek Eval yöntemine bir çağrı ile birlikte kullanılır.

    Çalışma zamanında, bu eval çağrıları, belirtilen ada sahip üyenin değerini okumak için o anda bağlı nesnenin yansımasını kullanır ve sonucu HTML olarak görüntüler. Bu yaklaşım, veri bağlamayı rastgele, düzensiz verilere karşı çok kolay hale getirir.

    Ne yazık ki, Visual Studio 'da üye adları için IntelliSense, gezinti için destek (tanıma git gibi) ve derleme zamanı denetimi gibi harika geliştirme zamanı deneyimi özelliklerinin çoğunu kaybedersiniz.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. **Customers.aspx.cs** dosyasını açın.
4. Aşağıdaki using ifadesini ekleyin.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. **Sayfa\_Load** yönteminde, yineleyicisi 'ni müşteriler listesiyle doldurmak için kod ekleyin.

    (Kod parçacığı- *Web Forms Lab-Ex01-BIND müşterileri veri kaynağı*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    Çözüm, veritabanı oluşturmak ve veritabanına erişmek için EntityFramework 'Ü CodeFirst ile birlikte kullanır. Aşağıdaki kodda, customersRepeater, veritabanındaki tüm müşterileri döndüren gerçekleştirilmiş bir sorguya bağlanır.
6. **F5** tuşuna basarak çözümü çalıştırın ve yineleyicisi 'ni eylemde görmek için **müşteriler** sayfasına gidin. Çözüm Codefırst kullanırken, uygulama çalıştırılırken veritabanı yerel SQL Express Örneğinizde oluşturulur ve doldurulur.

    ![Yineleyici olan müşterileri listeleme](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Yineleyici olan müşterileri listeleme")

    *Yineleyici olan müşterileri listeleme*

    > [!NOTE]
    > Visual Studio 2012 ' de, IIS Express varsayılan Web geliştirme sunucusudur.
7. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.
8. Şimdi, uygulamayı kesin belirlenmiş bağlamaları kullanacak şekilde değiştirin. **Customers. aspx** sayfasını açın ve **Kullanıcı türünü bağlama** türü olarak ayarlamak için Repeater ' da yeni **ItemType** özniteliğini kullanın.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType özelliği, denetimin bağlanacağı veri türünü bildirmenize olanak tanır ve veri bağlama denetimi içinde kesin türü belirtilmiş bağlamayı kullanmanıza olanak sağlar.
9. ItemTemplate içeriğini aşağıdaki kodla değiştirin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    Yukarıdaki yaklaşımlar ile bir aşağı doğru, eval () ve bind () çağrılarının geç bağlı olduğundan ve özellik adlarını temsil etmek için dizeleri geçirdiğiniz anlamına gelir. Bu, üye adları için IntelliSense 'i, kod gezintisi desteğini (tanım 'e git gibi) veya derleme zamanı denetimi desteğini belirtmediğiniz anlamına gelir.

    ItemType özelliğinin ayarlanması, veri bağlama ifadelerinin kapsamında iki yeni tür değişkenin oluşturulmasına neden olur: **Item** ve **BindItem**. Bu kesin türü belirtilmiş değişkenleri veri bağlama ifadelerinde kullanabilir ve Visual Studio geliştirme deneyiminin tüm avantajlarından yararlanabilirsiniz.

    İfadede kullanılan &quot; &quot; **:** güvenlik sorunlarından kaçınmak için (örneğin, siteler arası komut dosyası saldırıları), çıktıyı OTOMATIK olarak HTML olarak kodlayacaktır. Bu gösterim, yanıt yazma işlemi için .NET 4 ' te sunulduğundan, ancak artık veri bağlama ifadelerinde de kullanıma sunulmuştur.

    > [!NOTE]
    > Öğe üyesi tek yönlü bağlama için geçerlidir. İki yönlü bağlama gerçekleştirmek istiyorsanız, **BindItem** üyesini kullanın.

    ![Türü kesin belirlenmiş bağlamada IntelliSense desteği](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "Türü kesin belirlenmiş bağlamada IntelliSense desteği")

    *Türü kesin belirlenmiş bağlamada IntelliSense desteği*
10. Çözümü çalıştırmak için **F5** tuşuna basın ve değişikliklerin beklenen şekilde çalıştığından emin olmak için müşteriler sayfasına gidin.

    ![Müşteri ayrıntılarını listeleme](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Müşteri ayrıntılarını listeleme")

    *Müşteri ayrıntılarını listeleme*
11. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>Görev 2-Web Forms model bağlama ile tanışın

Önceki ASP.NET Web Forms sürümlerinde, iki yönlü veri bağlamayı gerçekleştirmek istediğinizde, verileri almak ve güncellemek istediğinizde, bir veri kaynağı nesnesi kullanmanız gerekir. Bu bir nesne veri kaynağı, bir SQL veri kaynağı, LINQ veri kaynağı vb. olabilir. Ancak senaryonuz verileri işlemek için özel kod gerektiriyorsa, nesne veri kaynağını kullanmanız gerekir ve bu, biraz sakıncayordu. Örneğin, karmaşık türlerden kaçınmak ve doğrulama mantığını yürütürken özel durumları işlemek için ihtiyaç duymanız gerekir.

Yeni Web Forms ASP.NET sürümünde, veri bağlama denetimleri model bağlamayı destekler. Bu, arka plan kod dosyanızdaki veya başka bir sınıftan mantığı çağırmak için doğrudan veri bağlantılı denetimde Select, Update, INSERT ve Delete yöntemleri belirleyebileceðiniz anlamına gelir.

Bunun hakkında bilgi edinmek için, yeni **SelectMethod** özniteliğini kullanarak ürün kategorilerini listelemek üzere bir GridView kullanacaksınız. Bu öznitelik, GridView verilerini almak için bir yöntem belirtmenize olanak sağlar.

1. **Products. aspx** sayfasını açın ve bir **GridView**ekleyin. Kesin türü belirtilmiş bağlamaları kullanmak ve sıralamayı ve Sayfalamayı etkinleştirmek için GridView 'ı aşağıda gösterildiği gibi yapılandırın.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. GridView öğesini, verileri seçmek için bir **GetCategories** yöntemi çağırmak üzere yapılandırmak Için yeni **SelectMethod** özniteliğini kullanın.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. **Products.aspx.cs** arka plan kod dosyasını açın ve aşağıdaki using deyimlerini ekleyin.

    (Kod parçacığı- *Web Forms Lab-Ex01-namespaces*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. **Products** sınıfında bir özel üye ekleyin ve yeni bir **productscontext**örneği atayın. Bu özellik veritabanına bağlanmanızı sağlayan Entity Framework veri bağlamını depolar.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. LINQ kullanarak kategorilerin listesini almak için **GetCategories** yöntemi oluşturun. GridView, **Products** özelliğini içerir, bu nedenle GridView, her kategorinin ürün miktarını gösterebilir. Yöntemin, daha sonra sayfa yaşam döngüsü üzerinde yürütülecek sorguyu temsil eden ham bir IQueryable nesnesi döndürtiğine dikkat edin.

    (Kod parçacığı- *Web Forms Lab-Ex01-GetCategories*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > Önceki ASP.NET Web Forms sürümlerinde, kendi özel kodunuzu yazmak ve gerekli tüm parametreleri almak için gerekli olan bir nesne veri kaynağı bağlamı içindeki kendi depo mantığınızı kullanarak sıralama ve sayfalama olanağı sağlar. Artık veri bağlama yöntemleri IQueryable döndürebilirken ve bu bir sorguyu hala yürütülmesi gerektiğini temsil ettiğinden, ASP.NET doğru sıralama ve sayfalama parametrelerini eklemek için sorguyu değiştirme işlemini gerçekleştirebilir.
6. Sitede hata ayıklamayı başlatmak için **F5** tuşuna basın ve Ürünler sayfasına gidin. GridView 'un GetCategories yöntemi tarafından döndürülen kategorilerle doldurulduğunu görmeniz gerekir.

    ![Model bağlamayı kullanarak GridView doldurma](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Model bağlamayı kullanarak GridView doldurma")

    *Model bağlamayı kullanarak GridView doldurma*
7. **Shıft**+**F5** tuşuna basarak hata ayıklamayı durdurun.

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>Görev 3-model bağlamasında değer sağlayıcıları

Model bağlama, yalnızca veri bağlantılı denetimde verilerinize doğrudan çalışmak için özel yöntemler belirtmenize olanak tanır, ancak aynı zamanda sayfadaki verileri bu yöntemlerin parametrelerine eşlemenizi sağlar. Yöntem parametresinde, değer sağlayıcısı özniteliklerini kullanarak değerin veri kaynağını belirtebilirsiniz. Örneğin:

- Sayfadaki denetimler
- Sorgu dizesi değerleri
- Verileri görüntüleme
- Oturum durumu
- Özgü
- Gönderilen form verileri
- Durumu görüntüle
- Özel değer sağlayıcıları da desteklenir

ASP.NET MVC 4 kullandıysanız model bağlama desteğinin benzer olduğunu fark edeceksiniz. Aslında, bu özellikler ASP.NET MVC 'den alınmıştır ve Web Forms de kullanabilmek için **System. Web** derlemesine taşınmıştır.

Bu görevde, GridView 'u her bir kategorinin ürün miktarına göre filtrelemek için, model bağlaması ile filtre parametresini alacak şekilde güncelleştireceğinizi göreceksiniz.

1. **Products. aspx** sayfasına geri dönün.
2. GridView 'un en üstünde, aşağıda gösterildiği gibi her bir kategorinin ürün sayısını seçmek için bir **etiket** ve **ComboBox** ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. Seçilen sayıda ürüne sahip kategori olmadığında bir ileti göstermek için GridView 'a bir **EmptyDataTemplate** ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. **Products.aspx.cs** arka plan kodunu açın ve aşağıdaki using ifadesini ekleyin.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. **GetCategories** metodunu bir Integer **minproductscount** bağımsız değişkeni alacak şekilde değiştirin ve döndürülen sonuçları filtreleyin. Bunu yapmak için yöntemini aşağıdaki kodla değiştirin.

    (Kod parçacığı- *Web Forms Lab-Ex01-GetCategories 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    **Minproductscount** bağımsız değişkenindeki yeni **[Control]** özniteliği, ASP.net değerinin sayfadaki bir denetim kullanılarak doldurulması gerektiğini bilmesine izin verir. ASP.NET, bağımsız değişkenin adı (minProductsCount) ile eşleşen herhangi bir denetimi arar ve gerekli eşlemeyi ve dönüştürmeyi, parametreyi denetim değeri ile dolduracak şekilde yapar.

    Alternatif olarak, özniteliği değerin nereden alınacağını belirten bir denetim belirtmenize olanak tanıyan aşırı yüklenmiş bir oluşturucu sağlar.

    > [!NOTE]
    > Veri bağlama özelliklerinin bir hedefi, sayfa etkileşimi için yazılması gereken kod miktarını azaltmaktır. [Control] değer sağlayıcısından ayrı olarak, yöntem parametreleriniz içinde diğer model bağlama sağlayıcılarını kullanabilirsiniz. Bunlardan bazıları görev giriş bölümünde listelenmiştir.
6. Sitede hata ayıklamayı başlatmak için **F5** tuşuna basın ve Ürünler sayfasına gidin. Açılan listeden bir dizi ürün seçin ve GridView 'un nasıl güncelleştirildiğini fark edin.

    ![GridView 'un açılan liste değeri ile filtrelenmesi](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "GridView 'un açılan liste değeri ile filtrelenmesi")

    *GridView 'un açılan liste değeri ile filtrelenmesi*
7. Hata ayıklamayı durdurun.

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>Görev 4-filtreleme için model bağlamayı kullanma

Bu görevde, seçili kategoride ürünleri göstermek için ikinci bir alt GridView ekleyeceksiniz.

1. **Products. aspx** sayfasını açın ve Seç düğmesini otomatik oluşturmak için GridView kategorisini güncelleştirin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. En Alta **Productsgrid** adlı Ikinci bir **GridView** ekleyin. **ItemType** öğesini **webformdöşeme. model. Product**, **DataKeyNames** to **ProductID** ve **SelectMethod** to **GetProducts**olarak ayarlayın. **AutoGenerateColumns** **değerini false** olarak ayarlayın ve ProductID, ProductName, Description ve BirimFiyat için sütunları ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. **Products.aspx.cs** arka plan kod dosyasını açın. GridView kategorisinden kategori KIMLIĞINI almak ve ürünleri filtrelemek için **GetProducts** yöntemini uygulayın. Model bağlama, **Categoriesgrid**içindeki seçili satırı kullanarak parametre değerini ayarlar. Bağımsız değişken adı ve denetim adı eşleşmediğinden, denetim değeri sağlayıcısındaki denetimin adını belirtmeniz gerekir.

    (Kod parçacığı- *Web Forms Lab-Ex01-GetProducts*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > Bu yaklaşım, bu yöntemlerin birim sınamasını kolaylaştırır. Web Forms yürütülmemekte olan bir birim testi bağlamında, [Control] özniteliği belirli bir eylemi gerçekleştirmeyecektir.
4. **Products. aspx** sayfasını açın ve GridView ürünlerini bulun. Ürün GridView ' i, seçili ürünü düzenlemeyle ilgili bir bağlantı gösterecek şekilde güncelleştirin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. **ProductDetails. aspx** sayfa kodunu açın ve **selectproduct** metodunu aşağıdaki kodla değiştirin.

    (Kod parçacığı- *Web Forms Lab-Ex01-SelectProduct yöntemi*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > Sorgu dizesindeki bir ProductID parametresinden Yöntem parametresini doldurmaya yönelik **[QueryString]** özniteliğinin kullanıldığını unutmayın.
6. Sitede hata ayıklamayı başlatmak için **F5** tuşuna basın ve Ürünler sayfasına gidin. Kategoriler GridView ' den herhangi bir kategori seçin ve Products GridView ' in güncelleştirildiğinden emin olun.

    ![Seçilen kategorinin ürünleri gösteriliyor](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Seçilen kategorinin ürünleri gösteriliyor")

    *Seçilen kategorinin ürünleri gösteriliyor*
7. Üründetails. aspx sayfasını açmak için ürün üzerindeki **Görünüm** bağlantısına tıklayın.

    Sayfanın, sorgu dizesinden ProductID parametresini kullanarak SelectMethod ile ürünü aldığına dikkat edin.

    ![Ürün ayrıntılarını görüntüleme](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Ürün ayrıntılarını görüntüleme")

    *Ürün ayrıntılarını görüntüleme*

    > [!NOTE]
    > Bir HTML açıklaması yazma özelliği bir sonraki alıştırmada uygulanır.

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>5\. görev-güncelleştirme Işlemleri için model bağlamayı kullanma

Önceki görevde, verileri seçmek için öncelikle model bağlamayı kullandınız, bu görevde güncelleştirme işlemlerinde model bağlamayı kullanmayı öğreneceksiniz.

Kullanıcı tarafından kategori güncelleştirmesine izin vermek için GridView kategorisini güncelleşolursunuz.

1. **Products. aspx** sayfasını açın ve Düzenle düğmesini otomatik olarak oluşturmak için GridView kategorisini güncelleştirin ve seçilen öğeyi güncelleştirmek üzere bir **updatecategory** yöntemi belirtmek için yeni **UpdateMethod** özniteliğini kullanın.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView 'daki DataKeyNames özniteliği, model bağlantılı nesneyi benzersiz bir şekilde tanımlayan üyeler ve bu nedenle, Update yönteminin en az Receive olması gereken parametrelerdir.
2. **Products.aspx.cs** arka plan kod dosyasını açın ve **updatecategory** yöntemini uygulayın. Yöntem, geçerli kategoriyi yüklemek için kategori KIMLIĞINI almalıdır, verileri GridView 'dan doldurur ve sonra kategoriyi güncelleştirir.

    (Kod parçacığı- *Web Forms Lab-Ex01-UpdateCategory*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    Page sınıfındaki yeni **TryUpdateModel** yöntemi, sayfadaki denetimlerden değerler kullanılarak model nesnesini doldurmaktan sorumludur. Bu durumda, güncelleştirilmiş değerleri, düzenlenmekte olan geçerli GridView satırına **Kategori** nesnesi olarak değiştirir.

    > [!NOTE]
    > Sonraki alıştırma, ModelState 'in kullanımını açıklayacak. nesne düzenlenirken Kullanıcı tarafından girilen verileri doğrulamak için geçerli.
3. Siteyi çalıştırın ve Ürünler sayfasına gidin. Bir kategoriyi düzenleyin. Yeni bir ad yazın ve sonra değişiklikleri kalıcı hale getirmek için **Güncelleştir** ' e tıklayın.

    ![Kategorileri Düzenle](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Kategorileri Düzenle")

    *Kategorileri Düzenle*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>Alıştırma 2: veri doğrulama

Bu alıştırmada, ASP.NET 4,5 ' deki yeni veri doğrulama özellikleri hakkında bilgi edineceksiniz. Web Forms yeni bir obtrusive doğrulama özelliği kullanıma sunulacaktır. Kullanıcı girişi doğrulaması için uygulama modeli sınıflarında bulunan veri ek açıklamalarını kullanacaksınız ve son olarak, bir sayfadaki tek tek denetimlere istek doğrulamayı açma veya kapatma hakkında bilgi edineceksiniz.

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>Görev 1-Obtrusive doğrulaması

Doğrulayıcılar dahil karmaşık verileri olan formlar sayfada çok fazla JavaScript kodu oluşturur ve bu da kodun %60 ' larını temsil edebilir. Unobtrusive doğrulaması etkinken, HTML kodunuz temizleyici ve tidier görünür.

Bu bölümde, her iki yapılandırma tarafından oluşturulan HTML kodunu karşılaştırmak için ASP.NET ' deki obtrusive doğrulamasını etkinleştirecektir.

1. **Visual Studio 2012** ' i açın ve bu laboratuvarın **Source\ex2-validation\begin** klasöründe bulunan **BEGIN** Solution ' i açın. Alternatif olarak, önceki alýþtýrmadaki mevcut çözümünüz üzerinde çalışmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için, Çözüm Gezgini, **Webformdöşeme** projesi **NuGet Paketlerini Yönet**' e tıklayın.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Web uygulamasını başlatmak için **F5** tuşuna basın. Müşteriler sayfasına gidin ve **yeni müşteri Ekle** bağlantısına tıklayın.
3. Tarayıcı sayfasına sağ tıklayın ve uygulama tarafından oluşturulan HTML kodunu açmak için **kaynağı görüntüle** seçeneğini belirleyin.

    ![Sayfa HTML kodunu gösterme](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Sayfa HTML kodunu gösterme")

    *Sayfa HTML kodunu gösterme*
4. Sayfa kaynak kodunda ilerleyin ve ASP.NET ' nin, doğrulamaları gerçekleştirmek ve hata listesini göstermek için sayfada JavaScript kodu ve veri Doğrulayıcıları içerdiğine dikkat edin.

    ![CustomerDetails sayfasında doğrulama JavaScript kodu](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails sayfasında doğrulama JavaScript kodu")

    *CustomerDetails sayfasında doğrulama JavaScript kodu*
5. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.
6. Şimdi, engellemeyen doğrulamayı etkinleştirecektir. **Web. config** dosyasını açın ve **appSettings** bölümünde **ValidationSettings: UnobtrusiveValidationMode** anahtarını bulun **.** Anahtar değerini **WebForms**olarak ayarlayın.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > Bu özelliği, &quot;sayfasında bu özelliği, yalnızca bazı sayfalar için Kaldıruntrusive doğrulamayı etkinleştirmek istiyorsanız **\_** &quot; olayında da ayarlayabilirsiniz.
7. **CustomerDetails. aspx** ' i açın ve Web uygulamasını başlatmak için **F5** 'e basın.
8. IE geliştirici araçları 'nı açmak için F12 tuşuna basın. Geliştirici araçları açıldıktan sonra komut dosyası sekmesini seçin. menüden **CustomerDetails. aspx** ' i seçin ve sayfada jQuery çalıştırmak için gereken betiklerin yerel siteden tarayıcıya yüklendiğini unutmayın.

    ![JQuery JavaScript dosyalarını doğrudan yerel IIS sunucusundan yükleme](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "JQuery JavaScript dosyalarını doğrudan yerel IIS sunucusundan yükleme")

    *JQuery JavaScript dosyalarını doğrudan yerel IIS sunucusundan yükleme*
9. Visual Studio 'ya dönmek için tarayıcıyı kapatın. **Site. Master** dosyasını yeniden açın ve **ScriptManager**'ı bulun. **EnableCdn** özelliği özniteliğini **true**değerine ekleyin. Bu, jQuery 'in yerel sitenin URL 'sinden değil, çevrimiçi URL 'den yüklenmesine zorlanır.
10. Visual Studio 'da **CustomerDetails. aspx** ' i açın. Siteyi çalıştırmak için F5 tuşuna basın. Internet Explorer açıldıktan sonra, geliştirici araçlarını açmak için F12 tuşuna basın. **Betik** sekmesini seçin ve ardından açılan listeye göz atın. Bu şekilde, jQuery JavaScript dosyaları artık yerel siteden yüklenmiyor, ancak çevrimiçi jQuery CDN 'den değil.

    ![CDN 'den jQuery JavaScript dosyalarını yükleme](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN 'den jQuery JavaScript dosyalarını yükleme")

    *CDN 'den jQuery JavaScript dosyalarını yükleme*
11. Tarayıcıdaki kaynağı görüntüle seçeneğini kullanarak HTML sayfası kaynak kodunu yeniden açın. Unobtrusive doğrulama ASP.NET ' i etkinleştirerek eklenen JavaScript kodunun Data-\*öznitelikleriyle değiştirildiğini unutmayın.

    ![Engellemeyen doğrulama kodu](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Engellemeyen doğrulama kodu")

    *Engellemeyen doğrulama kodu*

    > [!NOTE]
    > Bu örnekte, veri ek açıklamalarına sahip bir doğrulama özetinin yalnızca birkaç HTML ve JavaScript satırı ile basitleştirilmesi gerektiğini gördünüz. Daha önce, obtrusive doğrulaması olmadan, eklediğiniz daha fazla doğrulama denetimi, JavaScript doğrulama kodunuzun daha büyük olduğu kadar artar.

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>Görev 2-modeli veri ek açıklamalarıyla doğrulama

ASP.NET 4,5 Web Forms için veri açıklamaları doğrulaması sağlar. Her girişte doğrulama denetimi yapmak yerine, artık model sınıflarınızda kısıtlamalar tanımlayabilir ve bunları tüm Web uygulamanızda kullanabilirsiniz. Bu bölümde, yeni/düzenleme müşteri formunu doğrulamak için veri ek açıklamalarını nasıl kullanacağınızı öğreneceksiniz.

1. **Customerdetail. aspx** sayfasını açın. **EditItemTemplate** ve **InsertItemTemplate** bölümlerindeki müşterinin adı ve ikinci adının bir RequiredFieldValidator denetimleri kullanılarak doğrulanacağını unutmayın. Her Doğrulayıcı belirli bir koşulla ilişkilendirilir, bu yüzden denetlenecek koşul olarak çok sayıda Doğrulayıcıları dahil etmeniz gerekir.
2. Müşteri modeli sınıfını doğrulamak için veri ek açıklamaları ekleyin. Model klasöründe **Customer.cs** sınıfını açın ve veri ek açıklaması özniteliklerini kullanarak her bir özelliği **süsleyin** .

    (Kod parçacığı- *Web Forms laboratuvar-Ex02-veri ek açıklamaları*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4,5, var olan veri ek açıklaması koleksiyonunu genişletti. Kullanabileceğiniz bazı veri ek açıklamalarından bazıları şunlardır: [CreditCard], [Phone], [Emadresi], [Range], [Compare], [URL], [FileExtensions], [gerekli], [Key], [cevap içerisinde RegularExpression].
    > 
    > Bazı kullanım örnekleri:
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > Ayrıca, her bir öznitelik içinde kendi hata iletilerinizi de tanımlayabilirsiniz.
3. **CustomerDetails. aspx** ' i açın ve FormView denetiminin edıtıtemtemplate ve InsertItemTemplate bölümlerindeki First ve Last Name alanları Için tüm RequiredFieldValidators ' i kaldırın.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > Veri ek açıklamalarını kullanmanın bir avantajı, uygulama sayfalarınızda doğrulama mantığının çoğaltılmamasının bir avantajlarından biridir. Model içinde bir kez tanımlayabilir ve verileri işleyen tüm uygulama sayfalarında kullanırsınız.
4. **CustomerDetails. aspx** arka plan kodunu açın ve SaveCustomer yöntemini bulun. Bu yöntem, yeni bir müşteri eklenirken ve müşteri parametresi FormView denetim değerlerinden alındığında çağrılır. Sayfa denetimleri ve Parameter nesnesi arasındaki eşleme gerçekleştiğinde, ASP.NET tüm veri ek açıklaması özniteliklerine göre model doğrulamasını yürütür ve varsa ModelState sözlüğünü karşılaşılan hatalarla doldurur.

    ModelState. IsValid yalnızca, doğrulama gerçekleştirildikten sonra modelinizdeki tüm alanlar geçerliyse true değerini döndürür.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. Model hatalarının listesini göstermek için CustomerDetails sayfasının sonuna bir **ValidationSummary** denetimi ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **ShowModelStateErrors** , **doğru**olarak ayarlandığında, denetimin hataları ModelState sözlüğünden göstermesini sağlayacak olan ValidationSummary denetimindeki yeni bir özelliktir. Bu hatalar, veri ek açıklamaları doğrulamasından gelir.
6. Web uygulamasını çalıştırmak için **F5** tuşuna basın. Formu, bazı hatalı değerlerle doldurun ve doğrulamayı yürütmek için **Kaydet** ' e tıklayın. Alttaki hata özetine dikkat edin.

    ![Veri ek açıklamalarıyla doğrulama](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Veri ek açıklamalarıyla doğrulama")

    *Veri ek açıklamalarıyla doğrulama*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>Görev 3-ModelState ile özel veritabanı hatalarını Işleme

Önceki Web Forms sürümünde, çok uzun bir dize veya benzersiz bir anahtar ihlali gibi veritabanı hatalarının işlenmesi, depo kodunuzda özel durumlar üretilmesini ve sonra hata göstermek için arka plan kodunuzda özel durumları işlemeyi gerektirebilir. Oldukça basit bir işlem yapmak için büyük miktarda kod gereklidir.

Web Forms 4,5 ' de ModelState nesnesi, sayfadaki hataları, modelinizde veya veritabanından tutarlı bir şekilde göstermek için kullanılabilir.

Bu görevde, veritabanı özel durumlarını doğru bir şekilde işlemek ve ModelState nesnesini kullanarak kullanıcıya uygun iletiyi göstermek için kod ekleyeceksiniz.

1. Uygulama çalışmaya devam ederken, yinelenen bir değer kullanarak bir kategorinin adını güncelleştirmeyi deneyin.

    ![Yinelenen bir ada sahip bir kategoriyi güncelleştirme](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Yinelenen bir ada sahip bir kategoriyi güncelleştirme")

    *Yinelenen bir ada sahip bir kategoriyi güncelleştirme*

    **CategoryName** sütununun &quot;benzersiz&quot; kısıtlaması nedeniyle bir özel durum oluşturulduğuna dikkat edin.

    ![Yinelenen kategori adları için özel durum](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Yinelenen kategori adları için özel durum")

    *Yinelenen kategori adları için özel durum*
2. Hata ayıklamayı durdurun. **Products.aspx.cs** arka plan kod dosyasında, veritabanı tarafından oluşturulan özel durumları Işlemek Için **updatecategory** metodunu güncelleştirin. SaveChanges () yöntemi çağrısı yapın ve **ModelState** nesnesine bir hata ekleyin.

    Yeni **TryUpdateModel** yöntemi, veritabanından alınan kategori nesnesini Kullanıcı tarafından sunulan form verilerini kullanarak güncelleştirir.

    (Kod parçacığı- *Web Forms Lab-Ex02-UpdateCategory tanıtıcı hataları*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > İdeal olarak, DbUpdateException nedenini belirlemeniz ve kök nedenin benzersiz bir anahtar kısıtlamasının ihlal olup olmadığını kontrol etmeniz gerekir.
3. **Products. aspx** ' i açın ve model hatalarının listesini göstermek için GridView kategorisinin altına bir **ValidationSummary** denetimi ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. Siteyi çalıştırın ve Ürünler sayfasına gidin. Yinelenen bir değer kullanarak bir kategorinin adını güncelleştirmeyi deneyin.

    Özel durumun işlendiğine ve hata iletisinin **ValidationSummary** denetiminde göründüğünü unutmayın.

    ![Yinelenen kategori hatası](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Yinelenen kategori hatası")

    *Yinelenen kategori hatası*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>Görev 4-ASP.NET Web Forms 4,5 içinde Istek doğrulaması

ASP.NET ' deki istek doğrulama özelliği, siteler arası komut dosyası (XSS) saldırılarına karşı belirli bir varsayılan koruma düzeyi sağlar. Önceki ASP.NET sürümlerinde, istek doğrulaması varsayılan olarak etkinleştirilmiştir ve yalnızca bir sayfanın tamamı için devre dışı bırakılabilir. Yeni ASP.NET sürümü Web Forms, artık tek bir denetim için istek doğrulamayı devre dışı bırakabilir, yavaş istek doğrulaması gerçekleştirebilir veya kimliği doğrulanmamış istek verilerine erişebilirsiniz (Bunu yaptığınızda dikkatli olun!).

1. **CTRL + F5** tuşlarına basarak siteyi hata ayıklama olmadan başlatın ve Ürünler sayfasına gidin. Bir kategori seçin ve ardından herhangi bir üründe **düzenleme** bağlantısına tıklayın.
2. HTML etiketleri dahil olmak üzere tehlikeli olabilecek içerik içeren bir açıklama yazın. İstek doğrulaması nedeniyle oluşan özel durum hakkında bir uyarı alın.

    ![Potansiyel olarak tehlikeli içeriğe sahip bir ürünü Düzenle](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Potansiyel olarak tehlikeli içeriğe sahip bir ürünü Düzenle")

    *Potansiyel olarak tehlikeli içeriğe sahip bir ürünü Düzenle*

    ![İstek doğrulaması nedeniyle özel durum oluşturuldu](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "İstek doğrulaması nedeniyle özel durum oluşturuldu")

    *İstek doğrulaması nedeniyle özel durum oluşturuldu*
3. Sayfayı kapatın ve Visual Studio 'da hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.
4. **ProductDetails. aspx** sayfasını açın ve **Açıklama** metin kutusunu bulun.
5. TextBox 'a yeni **ValidateRequestMode** özelliğini ekleyin ve değerini **devre dışı**olarak ayarlayın.

    Yeni **ValidateRequestMode** özniteliği her denetimde istek doğrulamasını devre dışı bırakmanızı sağlar. Bu, HTML kodu alabilen bir girişi kullanmak istediğinizde, ancak doğrulamanın sayfanın geri kalanı için çalışmasını sağlamak istediğinizde yararlıdır.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. Web uygulamasını çalıştırmak için **F5** tuşuna basın. Ürün Düzenle sayfasını yeniden açın ve HTML etiketleri dahil bir ürün açıklaması doldurun. Artık açıklamaya HTML içeriği ekleyebildiğinize dikkat edin.

    ![Ürün açıklaması için istek doğrulaması devre dışı](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Ürün açıklaması için istek doğrulaması devre dışı")

    *Ürün açıklaması için istek doğrulaması devre dışı*

    > [!NOTE]
    > Bir üretim uygulamasında, yalnızca güvenli HTML etiketlerinin girildiğinden emin olmak için Kullanıcı tarafından girilen HTML kodunu temizleyin (örneğin, hiçbir &lt;betik&gt; etiketi yoktur). Bunu yapmak için [Microsoft Web koruması kitaplığı](https://www.nuget.org/packages/AntiXSS)'nı kullanabilirsiniz.
7. Ürünü yeniden düzenleyin. Ad alanına HTML kodu yazın ve **Kaydet**' e tıklayın. Istek doğrulamanın yalnızca açıklama alanı için devre dışı bırakıldığını ve kalan alanların geri kalanı, potansiyel olarak tehlikeli içerikte hala doğrulandığını unutmayın.

    ![İstek doğrulaması, alanların geri kalanında etkinleştirildi](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "İstek doğrulaması, alanların geri kalanında etkinleştirildi")

    *İstek doğrulaması, alanların geri kalanında etkinleştirildi*

    ASP.NET Web Forms 4,5, istek doğrulaması geç gerçekleştirmek için yeni bir istek doğrulama modu içerir. İstek doğrulama modu **4,5**olarak ayarlandığında, bir kod parçası *Request. form [&quot;Key&quot;]* , ASP.NET 4.5 'in istek doğrulaması yalnızca form koleksiyonundaki bu belirli öğe için istek doğrulamasını tetikler.

    Ayrıca, ASP.NET 4,5 artık Microsoft anti-XSS kitaplığı v 4.0 'ın temel kodlama yordamlarını içerir. XSS önleme kodlama yordamları, yeni **System. Web. Security. AntiXss** ad alanında bulunan yeni *AntiXssEncoder* türü tarafından uygulanır. *AntiXssEncoder*kullanacak şekilde yapılandırılmış **EncoderType** parametresi ile, ASP.NET içindeki tüm çıkış kodlaması otomatik olarak yeni kodlama yordamlarını kullanır.
8. ASP.NET 4,5 istek doğrulaması, istek verilerine yönelik doğrulanmamış erişimi de destekler. ASP.NET 4,5, **HttpRequest** nesnesine **doğrulanmamış**adlı yeni bir koleksiyon özelliği ekler. **HttpRequest** içine gittiğinizde, form, Querystrings, tanımlama bilgileri, URL 'ler ve benzeri tüm ortak istek verileri parçalarından erişebilirsiniz.

    ![Request. Undoðrulanmış nesne](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request. Undoðrulanmış nesne")

    *Request. Undoðrulanmış nesne*

    > [!NOTE]
    > **Lütfen HttpRequest. Undoğrulanabilen özelliğini dikkatli kullanın!** Tehlikeli metnin, şüphelenilmez müşterilere doğru bir şekilde dönerek geri işlenip işlenmeyeceğini güvence altına almak için ham istek verilerinde dikkatle özel doğrulama gerçekleştirdiğinizden emin olun!

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>Alıştırma 3: ASP.NET Web Forms zaman uyumsuz sayfa Işleme

Bu alıştırmada, ASP.NET Web Forms yeni zaman uyumsuz sayfa işleme özelliklerine tanıtıma sunulacaktır.

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>Görev 1-görüntüleri karşıya yüklemek ve göstermek için ürün ayrıntıları sayfasını güncelleştirme

Bu görevde, kullanıcının ürün için bir görüntü URL 'SI belirtmesini ve salt okunurdur görünümünde görüntülemesini sağlamak için ürün ayrıntıları sayfasını güncelleşolursunuz. Zaman uyumlu olarak indirerek, belirtilen görüntünün yerel bir kopyasını oluşturacaksınız. Bir sonraki görevde, zaman uyumsuz olarak çalışmasını sağlamak için bu uygulamayı güncelleşolursunuz.

1. **Visual Studio 2012** ' i açın ve bu laboratuvar klasöründen **Source\ex3-async\begin** ' de bulunan **Başlangıç** çözümünü yükleyin. Alternatif olarak, önceki alýþtýrmalardan mevcut çözümünüz üzerinde çalışmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için, Çözüm Gezgini, **Webformblok** projesine tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **ProductDetails. aspx** sayfa kaynağını açın ve ürün görüntüsünü göstermek için FormView 'un ItemTemplate 'e bir alan ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. FormView 'un EditTemplate içindeki görüntü URL 'sini belirtmek için bir alan ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. **ProductDetails.aspx.cs** arka plan kod dosyasını açın ve aşağıdaki ad alanı yönergelerini ekleyin.

    (Kod parçacığı- *Web Forms Lab-Ex03-namespaces*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. Yerel **görüntüler** klasöründe uzak görüntüleri depolamak Için bir **Updateproductımage** yöntemi oluşturun ve ürün varlığını yeni görüntü konumu değeriyle güncelleştirin.

    (Kod parçacığı- *Web Forms Lab-Ex03-Updateproductımage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. **Updateproductımage** yöntemini çağırmak Için **UpdateProduct** metodunu güncelleştirin.

    (Kod parçacığı- *Web Forms Lab-Ex03-Updateproductımage çağrısı*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. Uygulamayı çalıştırın ve bir ürünün görüntüsünü karşıya yüklemeyi deneyin. Örneğin, Office Clip sanat 'daki şu görüntü URL 'sini kullanabilirsiniz: [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![Bir ürün için görüntü ayarlama](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Bir ürün için görüntü ayarlama")

    *Bir ürün için görüntü ayarlama*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>Görev 2-ürün ayrıntıları sayfasına zaman uyumsuz Işleme ekleme

Bu görevde, zaman uyumsuz olarak çalışmasını sağlamak için ürün ayrıntıları sayfasını güncelleşolursunuz. ASP.NET 4,5 zaman uyumsuz sayfa işleme kullanılarak, uzun süre çalışan bir görevi geliştirecek.

Web uygulamalarındaki zaman uyumsuz yöntemler ASP.NET iş parçacığı havuzlarının kullanıldığı yöntemi iyileştirmek için kullanılabilir. ASP.NET ' de, isteklere katılan isteklerin iş parçacığı havuzunda sınırlı sayıda iş parçacığı vardır. bu nedenle, tüm iş parçacıkları meşgul olduğunda, yeni istekleri reddedecek şekilde ASP.NET başlar, uygulama hata iletilerini gönderir ve sitenizi kullanılamaz hale getirir.

Web sitenizdeki zaman alan işlemler, atanan iş parçacığını uzun bir süre kapladıklarından zaman uyumsuz programlama için harika adaylardır. Bu, uzun süre çalışan istekler, çok sayıda farklı öğe ve sayfa içeren, örneğin bir veritabanını sorgulayan veya bir dış Web sunucusuna erişen sayfalar içerir. Bunun avantajı, bu işlemler için zaman uyumsuz yöntemler kullanıyorsanız, sayfa işlenirken iş parçacığı serbest bırakılır ve iş parçacığı havuzuna döndürülür ve yeni bir sayfa isteğine katılmak için kullanılabilir. Bu, sayfanın iş parçacığı havuzundan bir iş parçacığında işlemeye başlayacağı ve zaman uyumsuz işlem tamamlandıktan sonra farklı bir iş parçacığında işlemeyi tamamlayabileceği anlamına gelir.

1. **ProductDetails. aspx** sayfasını açın. **Zaman uyumsuz** özniteliğini **Page** öğesine ekleyin ve **true**olarak ayarlayın. Bu öznitelik, ASP.NET 'in IHttpAsyncHandler arabirimini uygulamasını söyler.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. Sayfayı çalıştıran iş parçacıklarının ayrıntılarını göstermek için sayfanın alt kısmına bir etiket ekleyin.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. **ProductDetails.aspx.cs** açın ve aşağıdaki ad alanı yönergelerini ekleyin.

    (Kod parçacığı- *Web Forms Lab-Ex03-namespaces 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. Görüntüyü zaman uyumsuz bir görevle indirmek için **Updateproductımage** metodunu değiştirin. **WebClient** **DownloadFile** yöntemini **DownloadFileTaskAsync** yöntemiyle değiştirecek ve **await** anahtar sözcüğünü kapsayacaktır.

    (Kod parçacığı- *Web Forms Lab-Ex03-Updateproductımage zaman uyumsuz*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask, farklı bir iş parçacığında yürütülecek yeni bir sayfa zaman uyumsuz görevi kaydeder. Yürütülecek görev (t) ile bir lambda ifadesi alır. **DownloadFileTaskAsync** yöntemi içindeki **await** anahtar sözcüğü, geri kalan yöntemi **DownloadFileTaskAsync** yöntemi tamamlandıktan sonra zaman uyumsuz olarak çağrılan bir geri aramaya dönüştürür. ASP.NET, tüm HTTP isteği özgün değerlerini otomatik olarak tutarak metodun yürütülmesini sürdürür. .NET 4,5 ' deki yeni zaman uyumsuz programlama modeli, zaman uyumlu kod gibi görünen zaman uyumsuz kod yazmanızı sağlar ve derleyicinin geri çağırma işlevlerini veya devamlılık kodunu işlemesini sağlar.
    > [!NOTE]
    > RegisterAsyncTask ve PageAsyncTask, .NET 2,0 ' den bu yana zaten kullanılabilir. Await anahtar sözcüğü, .NET 4,5 zaman uyumsuz programlama modelinden yenidir ve .NET WebClient nesnesinden yeni TaskAsync yöntemleriyle birlikte kullanılabilir.
5. Kodun başlatıldığı ve yürütüldüğü iş parçacıklarını göstermek için kod ekleyin. Bunu yapmak için **Updateproductımage** yöntemini aşağıdaki kodla güncelleştirin.

    (Kod parçacığı- *Web Forms Lab-Ex03-iş parçacıklarını göster*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. Web sitesinin **Web. config** dosyasını açın. Aşağıdaki appSetting değişkenini ekleyin.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. **F5** tuşuna basarak uygulamayı çalıştırın ve ürün için bir görüntü yükleyin. Kodun başladığı ve bittiği iş parçacığı KIMLIĞI farklı olabilir. Bunun nedeni, zaman uyumsuz görevlerin ASP.NET iş parçacığı havuzundan ayrı bir iş parçacığında çalıştırılmaktır. Görev tamamlandığında ASP.NET, görevi kuyruğa geri koyar ve kullanılabilir iş parçacıklarını atar.

    ![Bir görüntüyü zaman uyumsuz olarak indirme](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Bir görüntüyü zaman uyumsuz olarak indirme")

    *Bir görüntüyü zaman uyumsuz olarak indirme*

> [!NOTE]
> Ayrıca, bu uygulamayı Azure 'a dağıtmak için [Ek B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama](#AppendixB).

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı laboratuvarda, aşağıdaki kavramlar ele alındı ve gösterilmiştir:

- Kesin türü belirtilmiş veri bağlama ifadeleri kullanın
- Web Forms yeni model bağlama özelliklerini kullan
- Sayfa verilerini arka plan kod yöntemlerine eşlemek için değer sağlayıcıları kullanın
- Kullanıcı girişi doğrulaması için veri ek açıklamalarını kullanma
- Web Forms içinde jQuery ile obtrusive istemci tarafı doğrulamasından yararlanın
- Ayrıntılı istek doğrulaması Uygula
- Web Forms zaman uyumsuz sayfa işleme Uygula

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürün için arama yapabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Azure portalından yeni bir Web sitesi oluşturmayı ve Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı gösterir.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>Görev 1-Azure portalından yeni bir Web sitesi oluşturma

1. [Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure portal oturum açın")

    *Portalda oturum açın*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Azure, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Azure 'a Portal dışından dağıtmanıza izin verir. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , etkin olan her bir yayımlama yöntemi için bir Web uygulamasını Azure 'da yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Azure 'da yayımlamaya yönelik bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerini okumayı destekler.

    ![Web sitesi yayımlama profili indiriliyor](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, Visual Studio 'dan Azure 'da bir Web uygulaması yayınlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *Değişiklikleri Onayla*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın.

     ![Hedef bağlantı dizesi yapılandırılıyor](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Ek C: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
