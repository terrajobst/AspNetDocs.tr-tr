---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4\. Bölüm: modeller ve veri erişimi | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, modelleri ve veri erişimini içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559677"
---
# <a name="part-4-models-and-data-access"></a>4\. Bölüm: Modeller ve Veri Erişimi

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.
> 
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 4\. bölüm, modelleri ve veri erişimini içerir.

Şimdiye kadar, Denetleyicilerimizden "kukla verileri" görüntüleme şablonlarımızla geçirdik. Şimdi gerçek bir veritabanını yedeklemeye hazırız. Bu öğreticide, veritabanı altyapımız olarak SQL Server Compact sürümünün (genellikle SQL CE olarak adlandırılır) nasıl kullanılacağını ele alacağız. SQL CE, herhangi bir yükleme veya yapılandırma gerektirmeyen ücretsiz, katıştırılmış, dosya tabanlı bir veritabanıdır. Bu, yerel geliştirme için gerçekten uygun hale getirir.

## <a name="database-access-with-entity-framework-code-first"></a>Entity Framework kodla veritabanı erişimi-Ilk

Veritabanını sorgulamak ve güncelleştirmek için ASP.NET MVC 3 projelerine dahil edilen Entity Framework (EF) desteğini kullanacağız. EF, geliştiricilerin bir veritabanında depolanan verileri nesne yönelimli bir şekilde sorgulamasını ve güncelleştirmesini sağlayan esnek bir nesne ilişkisel eşleme (ORM) veri API 'sidir.

Entity Framework sürüm 4, önce kod adlı bir geliştirme paradigmasını destekler. Kod-önce basit sınıflar ("düz eski" CLR nesnelerinden POCO olarak da bilinir) yazarak model nesnesi oluşturmanıza olanak sağlar ve hatta sınıfınızdan anında veritabanı oluşturabilir.

### <a name="changes-to-our-model-classes"></a>Model sınıflarımızda yapılan değişiklikler

Bu öğreticide Entity Framework veritabanı oluşturma özelliğinden yararlanacağız. Bunu yapmadan önce, model sınıflarımızda daha sonra kullanacağımız bazı şeyleri eklemek için birkaç küçük değişiklik yapalim.

#### <a name="adding-the-artist-model-classes"></a>Sanatçı model sınıfları ekleme

Albümlerimiz sanatçılarla ilişkilendirilecektir, bu nedenle bir sanatçının tanımlanabilmesi için basit bir model sınıfı ekleyeceğiz. Aşağıda gösterilen kodu kullanarak Artist.cs adlı modeller klasörüne yeni bir sınıf ekleyin.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>Model Sınıflarımızı güncelleştirme

Albüm sınıfını aşağıda gösterildiği gibi güncelleştirin.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

Sonra, tarz sınıfına aşağıdaki güncelleştirmeleri yapın.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a>Uygulama\_veri klasörü ekleniyor

SQL Server Express veritabanı dosyalarını tutmak için projenize bir uygulama\_veri dizini ekleyeceğiz. Uygulama\_verileri, veritabanı erişimi için zaten doğru güvenlik erişimi izinlerine sahip olan ASP.NET içinde özel bir dizindir. Proje menüsünde ASP.NET klasörü Ekle ' yi ve ardından App\_verileri ' ni seçin.

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>Web. config dosyasında bir bağlantı dizesi oluşturma

Entity Framework Web sitesinin yapılandırma dosyasına birkaç satır ekleyecek ve bu sayede veritabanınıza nasıl bağlanacağını biliyor. Projenin kökünde bulunan Web. config dosyasına çift tıklayın.

![](mvc-music-store-part-4/_static/image2.png)

Bu dosyanın en altına kaydırın ve aşağıda gösterildiği gibi, doğrudan son satırın üzerine bir &lt;connectionStrings&gt; bölümü ekleyin.

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>Bağlam sınıfı ekleme

Modeller klasörüne sağ tıklayın ve MusicStoreEntities.cs adlı yeni bir sınıf ekleyin.

![](mvc-music-store-part-4/_static/image3.png)

Bu sınıf Entity Framework veritabanı bağlamını temsil eder ve bizim için oluşturma, okuma, güncelleştirme ve silme işlemlerini işleymeyecektir. Bu sınıfın kodu aşağıda gösterilmiştir.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

Bu, başka bir yapılandırma, özel arabirimler vb. değildir. DbContext temel sınıfını genişleterek, MusicStoreEntities sınıfımız bizim için veritabanı işlemlerimizi işleyebilir. Şimdi bağlandığımızdan, veritabanımızda bazı ek bilgilerden yararlanmak için model sınıflarımıza birkaç özellik ekleyelim.

### <a name="adding-our-store-catalog-data"></a>Mağaza kataloğu verilerimizi ekleme

Yeni oluşturulan bir veritabanına "tohum" verileri ekleyen Entity Framework özelliğinden yararlanacağız. Bu, mağaza kataloğumuzu bir tarzın, sanatçıların ve albümlerin bir listesi ile önceden dolduracaktır. Bu öğreticide daha önce kullanılan site tasarım dosyalarımı içeren MvcMusicStore-Assets. zip indirmesi-kod adlı bir klasörde bulunan bu çekirdek verilerle bir sınıf dosyasına sahiptir.

Kod/modeller klasörü içinde, SampleData.cs dosyasını bulun ve aşağıda gösterildiği gibi, projemizdeki modeller klasörüne bırakın.

![](mvc-music-store-part-4/_static/image4.png)

Şimdi bu SampleData sınıfı hakkında Entity Framework söylemek için bir kod satırı eklememiz gerekiyor. Projenin kökündeki Global. asax dosyasına çift tıklayarak açın ve aşağıdaki satırı uygulama\_başlangıç yöntemine ekleyin.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

Bu noktada, projemiz için Entity Framework yapılandırmak üzere gereken işi tamamladık.

## <a name="querying-the-database"></a>Veritabanını Sorgulama

Şimdi StoreController 'ı, bunun yerine "kukla verileri" kullanmak yerine, tüm bilgilerini sorgulamak için veritabanımıza çağrı yapalım. StoreDB adlı bir MusicStoreEntities sınıfının örneğini tutmak için **Storecontroller** üzerinde bir alan bildirerek başlayacağız:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>Veritabanını sorgulamak için mağaza dizinini güncelleştirme

MusicStoreEntities sınıfı Entity Framework tarafından korunur ve veritabanımızda her tablo için bir koleksiyon özelliği sunar. Veritabanımızda tüm tarzları almak için StoreController 'ın Dizin eylemini güncelleştirelim. Daha önce bunu, dize verilerini sabit kodlayarak yaptık. Artık bunun yerine yalnızca Entity Framework Context Generes koleksiyonunu kullanabiliriz:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

Daha önce döndürtiğimiz Storeındexviewmodel 'i hala döndürtiğimiz için görünüm şablonumuza hiçbir değişiklik oluşmaması gerekmez; Şimdi veritabanımızdan canlı verileri döndürdük.

Projeyi yeniden çalıştırıp "/Store" URL 'sini ziyaret ettiğimiz zaman, veritabanımızda bulunan tüm tarzlar için bir liste görürsünüz:

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>Canlı verileri kullanmak için mağaza gözden geçirme ve ayrıntılarını güncelleştirme

/Store/gözatmaya? tarzı = *[bazı-tarz]* eylem yöntemiyle, bir tarz adına göre arıyoruz. Yalnızca bir sonuç beklediğimiz için, her zaman aynı tarz adı için iki girişi olmaması gerektiğinden, kullanabiliriz. LINQ to içinde uygun tarz nesnesini sorgulamak için tek () uzantısı, buna benzer (henüz bu türü kullanmayın):

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

Tek bir yöntem, bir lambda ifadesini parametre olarak alır, bu, adı tanımladığımız değerle eşleşen tek bir tarz nesne istiyoruz. Yukarıdaki örnekte, disco ile eşleşen bir ad değeriyle tek bir tarz nesnesi yüklüyorsunuz.

Bir Entity Framework özelliğinden yararlanarak, daha önce, yüklemek istediğimiz diğer ilgili varlıkları ve tarz nesnesi alındığında belirtmemizi sağlar. Bu özelliğe sorgu sonucu şekillendirme adı verilir ve ihtiyaç duyduğumuz tüm bilgileri almak için veritabanına erişmek için gereken sürelerin sayısını azaltmamızı sağlar. Aldığımız tarz için albümleri önceden getirmek istiyoruz. bu nedenle, ilgili Albümler 'in de isteyeceğini göstermek için sorgumuzu, tarzımızı ("Albümler") içerecek şekilde güncelleştireceğiz. Bu, hem tarz hem de albüm verilerimizi tek bir veritabanı isteğinde alacak olduğundan daha etkilidir.

Açıklamalar sayesinde, güncelleştirilmiş tarama denetleyicisi eylemizin şu şekilde görünür:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

Artık her bir tarz için kullanılabilir olan albümleri görüntülemek için mağaza Tarama görünümünü güncelleştirebiliriz. Görünüm şablonunu açın (/Views/Store/Browse.cshtml içinde bulunur) ve aşağıda gösterildiği gibi bir albüm listesi ekleyin.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

Uygulamamızı çalıştırmak ve/Store/gözatmaya? tarzı = Caat 'e gözatmak, sonuçlarımızın Şu anda veritabanından çekilmekte olduğunu gösteriyor ve seçili tarzımızda tüm albümleri görüntülüyor.

![](mvc-music-store-part-4/_static/image2.jpg)

/Store/Ayrıntılar/[ID] URL 'imizde aynı değişikliği yapacağız ve kukla verilerimizden KIMLIĞI parametre değeriyle eşleşen bir albüm yükleyen bir veritabanı sorgusuyla değiştiririz.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

Uygulamamızı çalıştırmak ve/Store/Details/1 adresine gözatımız, sonuçlarımızın artık veritabanından çekilmekte olduğunu gösterir.

![](mvc-music-store-part-4/_static/image5.png)

Şimdi mağaza ayrıntıları sayfamız, albüm KIMLIĞI tarafından bir albümü görüntüleyecek şekilde ayarlandığına göre, Ayrıntılar görünümünü bağlamak için **tarama** görünümünü güncelleştirelim. Önceki bölümde yer alacak şekilde mağaza dizininden Store 'a bağlantı yaptığımız gibi HTML. ActionLink kullanacağız. Aşağıda, tarama görünümünün tüm kaynağı görüntülenir.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

Artık mağaza sayfamıza, kullanılabilir albümleri listeleyen bir tarz sayfasına gözatabiliriz ve bu albümün ayrıntılarını görüntüleyebilmemiz için bir albüme tıklanıyoruz.

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-3.md)
> [İleri](mvc-music-store-part-5.md)
