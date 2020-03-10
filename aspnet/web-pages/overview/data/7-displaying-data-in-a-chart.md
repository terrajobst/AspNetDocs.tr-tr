---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: ASP.NET Web Pages (Razor) ile bir grafikteki verileri görüntüleme | Microsoft Docs
author: microsoft
description: Bu bölümde verilerin bir grafikte nasıl görüntüleneceği açıklanmaktadır. Önceki bölümlerde, verileri el ile ve bir kılavuzda görüntülemeyi öğrendiniz. Bu bölümde açıklanmaktadır...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 6dad67d4e3d38d57a761c567d937d714a3184ea9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627493"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>ASP.NET Web Pages (Razor) ile bir grafikteki verileri görüntüleme

[Microsoft](https://github.com/microsoft) tarafından

> Bu makalede, `Chart` Yardımcısını kullanarak bir ASP.NET Web Pages (Razor) Web sitesinde verileri görüntülemek için bir grafiğin nasıl kullanılacağı açıklanmaktadır.
> 
> Şunları **öğreneceksiniz**:
> 
> - Verileri bir grafikte görüntüleme.
> - Yerleşik Temalar kullanılarak grafikleri stil oluşturma.
> - Grafikleri kaydetme ve daha iyi performans için önbelleğe alma.
> 
> Makalesinde sunulan ASP.NET programlama özellikleri şunlardır:
> 
> - `Chart` Yardımcısı.
> 
> > [!NOTE]
> > Bu makaledeki bilgiler, ASP.NET Web sayfaları 1,0 ve Web sayfaları 2 için geçerlidir.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Grafik Yardımcısı

Verilerinizi grafik biçiminde göstermek istediğinizde `Chart` yardımcısını kullanabilirsiniz. `Chart` Yardımcısı, verileri çeşitli grafik türlerinde görüntüleyen bir görüntüyü işleyebilir. Biçimlendirme ve etiketleme için birçok seçeneği destekler. `Chart` Yardımcısı, Microsoft Excel veya diğer araç &#8212; alanı grafikleri, çubuk grafikler, sütun grafikleri, çizgi grafikleri ve pasta grafiklerinden tanıdık olabileceğiniz grafiklerin yanı sıra hisse senedi grafikleri gibi daha özelleştirilmiş grafiklerle birlikte 30 ' dan fazla grafik türünü işleyebilir.

| **Alan grafiği** ![açıklaması: alan grafik türünün resmi](7-displaying-data-in-a-chart/_static/image1.jpg) | **Çubuk grafik** ![açıklaması: çubuk grafik türünün resmi](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Sütun grafik** ![Açıklama: sütun grafik türünün resmi](7-displaying-data-in-a-chart/_static/image3.jpg) | **Çizgi grafik** ![açıklaması: çizgi grafik türünün resmi](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Pasta grafik** ![açıklaması: pasta grafik türünün resmi](7-displaying-data-in-a-chart/_static/image5.jpg) | **Hisse senedi grafik** ![açıklaması: hisse senedi grafik türünün resmi](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Grafik Öğeleri

Grafikler, verileri ve göstergeler, eksenler, seriler gibi ek öğeleri gösterir. Aşağıdaki resimde, `Chart` yardımcısını kullanırken özelleştirebileceğiniz grafik öğelerinin birçoğu gösterilmektedir. Bu makalede, bu öğelerin bazılarının (hepsini değil) nasıl ayarlanacağı gösterilmektedir.

![Açıklama: grafik öğelerini gösteren resim](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Verilerden grafik oluşturma

Bir grafikte görüntülenen veriler bir diziden, veritabanından döndürülen sonuçlardan veya bir XML dosyasındaki verilerden olabilir.

### <a name="using-an-array"></a>Dizi kullanma

[Razor söz dizimini kullanarak ASP.NET Web sayfaları programlamasına giriş](https://go.microsoft.com/fwlink/?LinkId=202890)bölümünde açıklandığı gibi, bir dizi benzer öğelerin koleksiyonunu tek bir değişkende depolamanıza olanak sağlar. Şeilerinize eklemek istediğiniz verileri içeren dizileri kullanabilirsiniz.

Bu yordamda, varsayılan grafik türünü kullanarak dizilerdeki verilerden nasıl bir grafik oluşturabileceğiniz gösterilmektedir. Ayrıca, grafiğin sayfa içinde nasıl görüntüleneceğini gösterir.

1. *Chartarraybasic. cshtml*adlı yeni bir dosya oluşturun.
2. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Kod ilk olarak yeni bir grafik oluşturur ve genişliğini ve yüksekliğini ayarlar. `AddTitle` yöntemini kullanarak grafik başlığını belirtirsiniz. Veri eklemek için `AddSeries` yöntemini kullanırsınız. Bu örnekte, `name` yönteminin `xValue`, `yValues` ve `AddSeries` parametrelerini kullanırsınız. `name` parametresi grafik açıklamasında görüntülenir. `xValue` parametresi, grafiğin yatay ekseni üzerinde görüntülenen bir veri dizisi içerir. `yValues` parametresi, grafiğin dikey noktalarını çizmek için kullanılan bir veri dizisi içerir.

    `Write` yöntemi, grafiği gerçekten işler. Bu durumda, bir grafik türü belirtmediğiniz için `Chart` Yardımcısı, bir sütun grafiği olan varsayılan grafiğini işler.
3. Sayfayı tarayıcıda çalıştırın. Tarayıcıda grafik görüntülenir. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Grafik verileri için veritabanı sorgusu kullanma

Grafik oluşturmak istediğiniz bilgiler bir veritabanında ise, bir veritabanı sorgusu çalıştırabilir ve sonra grafiği oluşturmak için sonuçlardan verileri kullanabilirsiniz. Bu yordamda, [ASP.NET Web sayfaları sitelerinde bir veritabanıyla çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=202893)makalesinde oluşturulan veritabanından verileri okuma ve görüntüleme işlemi gösterilmektedir.

1. Klasör zaten yoksa Web sitesinin köküne bir *App\_Data* klasörü ekleyin.
2. *App\_veri* klasöründe, [ASP.NET Web sayfaları sitelerinde bir veritabanıyla çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=202893)bölümünde açıklanan *smallbakaralan. sdf* adlı veritabanı dosyasını ekleyin.
3. *Chartdataquery. cshtml*adlı yeni bir dosya oluşturun.
4. Var olan içeriği aşağıdaki ile değiştirin:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Kod ilk olarak Smallbakarate veritabanını açar ve `db`adlı bir değişkene atar. Bu değişken, veritabanını okumak ve veritabanına yazmak için kullanılabilecek bir `Database` nesnesini temsil eder. Daha sonra kod, her bir ürünün adını ve fiyatını almak için bir SQL sorgusu çalıştırır. Kod, yeni bir grafik oluşturur ve grafiğin `DataBindTable` yöntemini çağırarak veritabanı sorgusunu buna geçirir. Bu yöntem iki parametre alır: `dataSource` parametresi sorgudaki verilere yöneliktir ve `xField` parametresi, grafiğin x ekseni için hangi veri sütununun kullanılacağını ayarlamanıza olanak sağlar.

    `DataBindTable` yönteminin kullanılmasına alternatif olarak `Chart` yardımcı 'nın `AddSeries` yöntemini kullanabilirsiniz. `AddSeries` yöntemi `xValue` ve `yValues` parametrelerini ayarlamanıza olanak tanır. Örneğin, bunun gibi `DataBindTable` yöntemini kullanmak yerine:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    `AddSeries` yöntemini şöyle kullanabilirsiniz:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Her ikisi de aynı sonuçları işler. Grafik türünü ve verileri daha açık bir şekilde belirtebileceğiniz için `AddSeries` yöntemi daha esnektir, ancak ek esneklik gerekmiyorsa `DataBindTable` yöntemi daha kolay kullanılır.
5. Sayfayı bir tarayıcıda çalıştırın. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>XML verileri kullanma

Grafik için üçüncü seçenek, grafik için veri olarak bir XML dosyası kullanmaktır. Bu, XML dosyasının XML yapısını açıklayan bir şema dosyasına ( *. xsd* dosyası) sahip olmasını gerektirir. Bu yordamda, bir XML dosyasındaki verilerin nasıl okunacağı gösterilmektedir.

1. *App\_veri* klasöründe *Data. xml*adlı yeni bir XML dosyası oluşturun.
2. Mevcut XML 'i, kurgusal bir şirketteki çalışanlar hakkında bazı XML verileri olan aşağıdaki ile değiştirin. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. *App\_veri* klasöründe *Data. xsd*adlı yeni bir XML dosyası oluşturun. (Bu süre uzantısının *. xsd*olduğunu unutmayın.)
4. Var olan XML 'i aşağıdaki kodla değiştirin: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. Web sitesinin kökünde, *Chartdataxml. cshtml*adlı yeni bir dosya oluşturun.
6. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Kod ilk olarak bir `DataSet` nesnesi oluşturur. Bu nesne, XML dosyasından okunan verileri yönetmek ve şema dosyasındaki bilgilere göre düzenlemek için kullanılır. (Kodun en üstüne `using SystemData`deyimin dahil olduğuna dikkat edin. `DataSet` nesnesiyle çalışabilmeniz için bu gereklidir. Daha fazla bilgi için, bu makalenin ilerleyen kısımlarında [&quot; deyimlerini ve tam adları kullanarak&quot;](#SB_UsingStatements) bakın.)

    Daha sonra kod, veri kümesini temel alan bir `DataView` nesnesi oluşturur. Veri görünümü, grafiğin, okuma ve çizim için &#8212; bağlanacağı bir nesne sağlar. Grafik, `xValue` ve `yValues` parametrelerinin `DataView` nesnesine ayarlandığı durumlar dışında, daha önce dizi verilerini grafik oluştururken gördüğünüz `AddSeries` yöntemi kullanılarak verilere bağlanır.

    Bu örnek ayrıca, belirli bir grafik türünü nasıl belirtkullanabileceğinizi gösterir. Veriler `AddSeries` yöntemine eklendiğinde, `chartType` parametresi de bir pasta grafiği görüntüleyecek şekilde ayarlanır.
7. Sayfayı bir tarayıcıda çalıştırın. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" deyimleri ve tam nitelikli adlar
> 
> Razor söz dizimi içeren Web sayfalarının .NET Framework, binlerce bileşenden (sınıflar) oluşur. BT 'nin tüm bu sınıflarla çalışmasını sağlamak için, kitaplıklar gibi, *ad alanları*halinde düzenlenirler. Örneğin, `System.Web` ad alanı tarayıcı/sunucu iletişimini destekleyen sınıflar içeriyorsa, `System.Xml` ad alanı XML dosyalarını oluşturmak ve okumak için kullanılan sınıfları içerir ve `System.Data` ad alanı, verilerle çalışmanıza izin veren sınıflar içerir.
> 
> .NET Framework belirli bir sınıfa erişmek için, kodun yalnızca sınıf adını değil, ayrıca sınıfın içinde bulunduğu ad alanını bilmesi gerekir. Örneğin, `Chart` Yardımcısını kullanmak için kodun, ad alanını (`System.Web.Helpers`) sınıf adıyla (`Chart`) birleştiren `System.Web.Helpers.Chart` sınıfını bulması gerekir. Bu, sınıfın *tamamen* tam adı &#8212; olarak bilinir ve bu, .NET Framework yüksek bir konum içinde tam bir konum değildir. Kodda, bu, aşağıdaki gibi görünür:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Ancak, bir sınıfa veya yardımcıya her başvurmak istediğinizde, bu uzun ve tam adları kullanmak için çok daha fazla (ve hataya açıktır). Bu nedenle, sınıf adlarının kullanılmasını kolaylaştırmak için, ilgilendiğiniz ad alanlarını *içeri aktarabilirsiniz* . Bu, genellikle .NET Framework çok sayıda ad alanı arasından tek bir yoldur. Bir ad alanını içeri aktardıysanız, tam adı (`System.Web.Helpers.Chart`) yerine yalnızca bir sınıf adı (`Chart`) kullanabilirsiniz. Kodunuz çalıştırıldığında ve bir sınıf adı ile karşılaştığında, bu sınıfı bulmak için yalnızca içeri aktardığınız ad alanlarını arayabilir.
> 
> Web sayfaları oluşturmak için Razor söz dizimi ile ASP.NET Web sayfaları kullandığınızda, genellikle `WebPage` sınıfı, çeşitli yardımcılar ve benzeri gibi her seferinde aynı sınıf kümesini kullanırsınız. Bir Web sitesi oluşturduğunuzda ilgili ad alanlarını içeri aktarma işi için, ASP.NET yapılandırılır, böylece her Web sitesi için bir dizi çekirdek ad alanını otomatik olarak aktarır. Bu nedenle, ad alanlarını ilgilenmenize veya şu anda içeri aktarmadığınıza göre üzerinde çalıştığınız tüm sınıflar, sizin için zaten içeri aktarılmış olan ad boşluklarlardır.
> 
> Ancak, bazen sizin için otomatik olarak içeri aktarılan bir ad alanında olmayan bir sınıfla çalışmanız gerekir. Bu durumda, bu sınıfın tam adını kullanabilir ya da sınıfını içeren ad alanını el ile içeri aktarabilirsiniz. Bir ad alanını içeri aktarmak için, makalenin önceki kısımlarında gördüğünüz gibi `using` ifadesini (`import` Visual Basic) kullanırsınız.
> 
> Örneğin, `DataSet` sınıfı `System.Data` ad alanıdır. `System.Data` ad alanı ASP.NET Razor sayfaları için otomatik olarak kullanılamaz. Bu nedenle, tam adı kullanarak `DataSet` sınıfla çalışmak için aşağıdaki gibi bir kod kullanabilirsiniz:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> `DataSet` sınıfını tekrar tekrar kullanmanız gerekiyorsa, bunun gibi bir ad alanını içeri aktarabilir ve ardından kodda yalnızca sınıf adını kullanabilirsiniz:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Başvurmak istediğiniz diğer tüm .NET Framework ad alanları için `using` deyimlerini ekleyebilirsiniz. Bununla birlikte, birlikte çalışacağımız sınıfların çoğu, ASP.NET tarafından *. cshtml* ve *. vbhtml* sayfalarında kullanılmak üzere otomatik olarak içeri aktarılan ad alanlarında olduğundan, bu durum genellikle yapmanız gerekmez.

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Grafikleri bir Web sayfası Içinde görüntüleme

Şimdiye kadar gördüğünüz örneklerde bir grafik oluşturun ve ardından grafik doğrudan tarayıcıya bir grafik olarak işlenir. Birçok durumda, ancak tarayıcıda yalnızca kendi başına değil, bir sayfanın parçası olarak bir grafik görüntülenmesini istersiniz. Bunu yapmak için iki adımlı bir işlem gerekir. İlk adım, zaten gördüğünüz gibi grafiği oluşturan bir sayfa oluşturmaktır.

İkinci adım, sonuçta elde edilen görüntüyü başka bir sayfada görüntülemektir. Görüntüyü göstermek için, bir HTML `<img>` öğesini herhangi bir görüntüyü görüntülerken kullandığınız şekilde kullanırsınız. Ancak, bir *. jpg* veya *. png* dosyasına başvurmak yerine `<img>` öğesi, grafiği oluşturan `Chart` Yardımcısını içeren *. cshtml* dosyasına başvurur. Görüntü sayfası çalıştırıldığında, `<img>` öğesi `Chart` Yardımcısı çıktısını alır ve grafiği işler.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. *Showchart. cshtml*adlı bir dosya oluşturun.
2. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Kod, daha önce *Chartarraybasic. cshtml* dosyasında oluşturduğunuz grafiği göstermek için `<img>` öğesini kullanır.
3. Web sayfasını bir tarayıcıda çalıştırın. *Showchart. cshtml* dosyası, *Chartarraybasic. cshtml* dosyasında bulunan koda göre grafik görüntüsünü görüntüler.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Grafik Stillendirme

`Chart` Yardımcısı, grafiğin görünümünü özelleştirmenize olanak sağlayan çok sayıda seçeneği destekler. Renkleri, yazı tiplerini, kenarlıkları ve benzerlerini ayarlayabilirsiniz. Bir grafiğin görünümünü özelleştirmenin kolay bir yolu bir *Tema*kullanmaktır. Temalar, bir grafiğin yazıtipleri, renkler, etiketler, paletler, sınırlar ve etkiler kullanılarak nasıl oluşturulacağını belirten bilgi topluluklarıdır. (Bir grafik stilinin grafik türünü göstermediğini unutmayın.)

Aşağıdaki tabloda yerleşik temalar listelenmektedir.

| Tema | Açıklama |
| --- | --- |
| `Vanilla` | Beyaz bir arka planda kırmızı sütunları görüntüler. |
| `Blue` | Mavi bir gradyan arka planında mavi sütunları görüntüler. |
| `Green` | Yeşil gradyan arka planında mavi sütunları görüntüler. |
| `Yellow` | Turuncu sütunları sarı bir gradyan arka planında görüntüler. |
| `Vanilla3D` | Beyaz bir arka planda 3-b kırmızı sütunları görüntüler. |

Yeni bir grafik oluştururken kullanılacak temayı belirtebilirsiniz.

1. *Chartstylegreen. cshtml*adlı yeni bir dosya oluşturun.
2. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Bu kod, veri veritabanını kullanan önceki örnekle aynıdır, ancak `Chart` nesnesini oluşturduğunda `theme` parametresi ekler. Değiştirilen kodu aşağıda gösterilmektedir:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Sayfayı bir tarayıcıda çalıştırın. Önceki verilerle aynı verileri görürsünüz, ancak grafik daha parlak görünür: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Grafik kaydetme

Bu makalede şimdiye kadar gördüğünüz `Chart` Yardımcısı 'nı kullandığınızda, yardımcı her çağrıldığında grafiği sıfırdan yeniden oluşturur. Gerekirse, grafiğe yönelik kod ayrıca veritabanını yeniden sorgular veya verileri almak için XML dosyasını yeniden okur. Bazı durumlarda, sorgulama yaptığınız veritabanı büyükse veya XML dosyası çok miktarda veri içeriyorsa, bunun yapılması karmaşık bir işlem olabilir. Grafik çok fazla veri içermiyorsa bile, bir görüntüyü dinamik olarak oluşturma işlemi sunucu kaynaklarını kaplar ve çok sayıda kişi, grafiği görüntüleyen sayfayı veya sayfaları talep etse, Web sitenizin performansı üzerinde bir etkisi olabilir.

Grafik oluşturmanın olası performans etkisini azaltmaya yardımcı olmak için, ilk kez ihtiyacınız olduğunda bir grafik oluşturabilir ve ardından kaydedebilirsiniz. Grafik gerektiğinde yeniden oluşturmak yerine, kaydedilen sürümü getirip işleyebilir.

Bir grafiği şu yollarla kaydedebilirsiniz:

- Grafiği bilgisayar belleğinde (sunucusunda) önbelleğe alır.
- Grafiği bir resim dosyası olarak kaydedin.
- Grafiği bir XML dosyası olarak kaydedin. Bu seçenek, kaydetmeden önce grafiği değiştirmenize olanak sağlar.

### <a name="caching-a-chart"></a>Bir grafiği önbelleğe alma

Bir grafik oluşturduktan sonra, bunu önbelleğe alabilirsiniz. Bir grafiği önbelleğe almak, yeniden görüntülenmesi gerekiyorsa, yeniden oluşturulması gerekmediği anlamına gelir. Bir grafiği önbellekte kaydettiğinizde, bu grafiğe benzersiz olması gereken bir anahtar verirsiniz.

Sunucu belleği azalmışsa, önbelleğe kaydedilen grafikler kaldırılabilir. Ayrıca, uygulamanız herhangi bir nedenle yeniden başlatılırsa önbellek temizlenir. Bu nedenle, önbelleğe alınmış bir grafik ile çalışmanın standart yolu, ilk olarak önbellekte kullanılabilir olup olmadığını kontrol etmek ve yoksa yeniden oluşturmak veya yeniden oluşturmak için kullanılır.

1. Web sitenizin kökünde *Showcachedchart. cshtml*adlı bir dosya oluşturun.
2. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` etiketi, *Chartsavetocache. cshtml* dosyasına işaret eden bir `src` özniteliği içerir ve bir anahtarı bir sorgu dizesi olarak sayfaya geçirir. Anahtar, myChartKey&quot;&quot;değerini içerir. *Chartsavetocache. cshtml* dosyası grafiği oluşturan `Chart` yardımcısını içerir. Bu sayfayı bir süre içinde oluşturacaksınız.

    Sayfanın sonunda, *ClearCache. cshtml*adlı bir sayfanın bağlantısı vardır. Bu, kısa süre içinde de oluşturacağınız bir sayfasıdır. Bu örnek için yalnızca önbellek önbelleği için *ClearCache. cshtml* gereklidir; bu, önbelleğe alınmış grafiklerle çalışırken normalde dahil edeceğiniz bir bağlantı veya sayfa değildir.
3. Web sitenizin kökünde, *Chartsavetocache. cshtml*adlı yeni bir dosya oluşturun.
4. Var olan içeriği aşağıdaki ile değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Kod ilk olarak sorgu dizesinde anahtar değer olarak herhangi bir şeyin geçtiğini denetler. Bu durumda, kod `GetFromCache` yöntemini çağırarak ve anahtarı geçirerek bir grafiği önbellekten okumaya çalışır. Bu anahtar altında önbellekte hiçbir şey olmadığını (grafik istendiğinde ilk kez gerçekleşecektir) önyüklerseniz, kod grafiği her zamanki gibi oluşturur. Grafik tamamlandığında, kod `SaveToCache`çağırarak önbelleğe kaydeder. Bu yöntem bir anahtar gerektirir (Bu nedenle grafik daha sonra istenebilir) ve grafiğin önbellekte kaydedilmesi gereken süre miktarı. (Bir grafiği tam olarak önbelleğe alacağınız zaman, temsil ettiği verilerin ne sıklıkta değişeceğinize göre değişir.) `SaveToCache` yöntemi, true olarak ayarlanırsa bir `slidingExpiration` &#8212; parametresi gerektirir, grafiğe her erişildiğinde zaman aşımı sayacı sıfırlanır. Bu durumda, etkin olması, grafiğin önbellek girişinin, bir kişinin grafiğe son kez eriştiği zamandan sonraki 2 dakika sona erdiği anlamına gelir. (Kayan süre sonu için alternatif, mutlak süre sonu, yani önbellek girişinin önbelleğe alındıktan sonra, ne sıklıkta erişildiğine bakılmaksızın tam olarak 2 dakika dolacağını belirtir.)

    Son olarak, kod `WriteFromCache` yöntemi kullanarak grafiği alıp önbellekten işleyebilir. Bu yöntemin önbelleği denetleyen `if` bloğunun dışında olduğunu unutmayın, çünkü grafiğin, bir veya oluşturulması ve önbellekte kaydedilmesi gerekiyordu. bu durum, grafiği önbellekten alacak veya bu durumda kaydedilecek şekilde.

    Örnekte, `AddTitle` yönteminin bir zaman damgası içerdiğine dikkat edin. (Geçerli tarih ve saat &#8212; `DateTime.Now` &#8212; başlığına ekler.)
5. *ClearCache. cshtml* adlı yeni bir sayfa oluşturun ve içeriğini aşağıdakiler ile değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Bu sayfa, *Chartsavetocache. cshtml*içinde önbelleğe alınan grafiği kaldırmak için `WebCache` yardımcısını kullanır. Daha önce belirtildiği gibi, normalde bunun gibi bir sayfanız olması gerekmez. Burada yalnızca önbelleğe alma sınamasını kolaylaştırmak için oluşturuluyor olursunuz.
6. *Showcachedchart. cshtml* Web sayfasını bir tarayıcıda çalıştırın. Sayfa, *Chartsavetocache. cshtml* dosyasında bulunan koda göre grafik görüntüsünü görüntüler. Grafik başlığında zaman damgasının ne olduğuna ilişkin bir göz atın. 

    ![Açıklama: Grafik başlığında zaman damgasıyla temel grafiğin resmi](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Tarayıcıyı kapatın.
8. *Showcachedchart. cshtml* dosyasını yeniden çalıştırın. Zaman damgasının daha önce olduğu gibi, grafiğin yeniden üretilmediğini belirten, ancak önbellekten okunduğuna dikkat edin.
9. *Showcachedchart. cshtml*dosyasında **önbelleği temizle** bağlantısına tıklayın. Bu sizi, önbelleğin temizlenmiş olduğunu raporlayan *ClearCache. cshtml*öğesine götürür.
10. **Showcachedchart. cshtml bağlantısına dön** veya WebMatrix 'Ten *showcachedchart. cshtml* öğesini yeniden çalıştırın. Bu zaman damgasının değiştiği ve önbelleğin temizlendiğine dikkat edin. Bu nedenle, kodun grafiği yeniden oluşturması ve önbelleğe geri dönmesi gerekiyordu.

### <a name="saving-a-chart-as-an-image-file"></a>Bir grafiği resim dosyası olarak kaydetme

Ayrıca, bir grafiği bir görüntü dosyası (örneğin, bir *. jpg* dosyası) olarak sunucuya kaydedebilirsiniz. Daha sonra resim dosyasını istediğiniz şekilde kullanabilirsiniz. Bunun avantajı, dosyanın geçici bir önbelleğe kaydedilmesi yerine saklanmasıdır. Yeni bir grafik görüntüsünü farklı zamanlarda (örneğin, her saat) kaydedebilir ve sonra zaman içinde oluşan değişikliklerin kalıcı kaydını tutabilirsiniz. Web uygulamanızın, görüntü dosyasını yerleştirmek istediğiniz sunucuda bulunan klasöre dosya kaydetme izni olduğundan emin olun.

1. Web sitenizin kökünde, zaten yoksa *\_ChartFiles* adlı bir klasör oluşturun.
2. Web sitenizin kökünde, *Chartsave. cshtml*adlı yeni bir dosya oluşturun.
3. Var olan içeriği aşağıdaki ile değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Kod ilk olarak, `File.Exists` yöntemini çağırarak *. jpg* dosyasının mevcut olup olmadığını denetler. Dosya yoksa, kod diziden yeni bir `Chart` oluşturur. Bu kez, kod `Save` yöntemini çağırır ve grafiğin kaydedileceği dosya yolunu ve dosya adını belirtmek için `path` parametresini geçirir. Sayfanın gövdesinde `<img>` öğesi, görüntülenecek *. jpg* dosyasını işaret etmek için yolu kullanır.
4. *Chartsave. cshtml* dosyasını çalıştırın.
5. WebMatrix 'e geri dönün. *Chart01. jpg* adlı bir resim dosyasının *\_chartfiles* klasörüne kaydedildiğini unutmayın.

### <a name="saving-a-chart-as-an-xml-file"></a>Bir grafiği bir XML dosyası olarak kaydetme

Son olarak, bir grafiği sunucuda bir XML dosyası olarak kaydedebilirsiniz. Grafiği önbelleğe alma veya grafiği bir dosyaya kaydetme konusunda bu yöntemi kullanmanın bir avantajı, isterseniz grafiği görüntülemeden önce XML 'yi değiştirebilmektir. Uygulamanızın, görüntü dosyasını yerleştirmek istediğiniz klasör için okuma/yazma izinlerine sahip olması gerekir.

1. Web sitenizin kökünde, *Chartsavexml. cshtml*adlı yeni bir dosya oluşturun.
2. Var olan içeriği aşağıdaki ile değiştirin:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Bu kod, bir XML dosyası kullanması dışında, bir grafiği önbellekte depolamak için daha önce gördüğünüz koda benzer. Kod ilk olarak, `File.Exists` yöntemini çağırarak XML dosyasının mevcut olup olmadığını denetler. Dosya varsa, kod yeni bir `Chart` nesnesi oluşturur ve dosya adını `themePath` parametresi olarak geçirir. Bu, XML dosyasında her şeyi temel alan grafiği oluşturur. XML dosyası zaten yoksa, kod normal gibi bir grafik oluşturur ve sonra kaydetmek için `SaveXml` çağırır. Grafik, daha önce gördüğünüz gibi `Write` yöntemi kullanılarak işlenir.

    Önbelleğe almayı gösteren sayfada olduğu gibi, bu kod grafik başlığında bir zaman damgası içerir.
3. *Chartdisplayxmlchart. cshtml* adlı yeni bir sayfa oluşturun ve buna aşağıdaki biçimlendirmeyi ekleyin: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. *Chartdisplayxmlchart. cshtml* sayfasını çalıştırın. Grafik görüntülenir. Grafiğin başlığındaki zaman damgasını bir yere göz atın.
5. Tarayıcıyı kapatın.
6. WebMatrix 'te, *\_ChartFiles* klasörüne sağ tıklayın, **Yenile**' ye tıklayın ve klasörü açın. Bu klasördeki *Xmlchart. xml* dosyası `Chart` Yardımcısı tarafından oluşturuldu. 

    ![Açıklama: grafik Yardımcısı tarafından oluşturulan XMLChart. xml dosyasını gösteren _ChartFiles klasörü.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. *Chartdisplayxmlchart. cshtml* sayfasını yeniden çalıştırın. Grafik, sayfayı ilk çalıştırışınızda aynı zaman damgasını gösterir. Bunun nedeni, grafiğin daha önce kaydettiğiniz XML 'den üretilmesinden kaynaklanır.
8. WebMatrix 'te, *\_ChartFiles* klasörünü açın ve *xmlchart. xml* dosyasını silin.
9. *Chartdisplayxmlchart. cshtml* sayfasını bir kez daha çalıştırın. Bu kez, `Chart` Yardımcısı XML dosyasını yeniden oluşturmak zorunda olduğundan zaman damgası güncellenir. İsterseniz, *\_ChartFiles* klasörünü denetleyip XML dosyasının geri olduğuna dikkat edin.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.NET Web sayfaları sitelerinde bir veritabanıyla çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Performansı artırmak için ASP.NET Web sayfaları sitelerinde önbelleğe alma kullanma](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Grafik sınıfı](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (MSDN 'de ASP.NET Web Pages API Başvurusu)
