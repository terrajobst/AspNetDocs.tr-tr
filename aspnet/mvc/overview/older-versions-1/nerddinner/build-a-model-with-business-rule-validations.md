---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Iş kuralı doğrulamaları ile model oluşturma | Microsoft Docs
author: microsoft
description: 3\. adım, Nerdakşam yemeği uygulamamız için veritabanını sorgulamak ve güncelleştirmek üzere kullandığımız bir modelin nasıl oluşturulacağını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541666"
---
# <a name="build-a-model-with-business-rule-validations"></a>İş Kuralı Doğrulamaları ile Model Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 3. adımından oluşur.
> 
> 3\. adım, Nerdakşam yemeği uygulamamız için veritabanını sorgulamak ve güncelleştirmek üzere kullandığımız bir modelin nasıl oluşturulacağını gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-3-building-the-model"></a>Nerdakşam yemeği 3. Adım: model oluşturma

Model-View-Controller çerçevesinde, "model" terimi, uygulamanın verilerinin yanı sıra doğrulama ve iş kurallarını uygulamayla tümleştiren karşılık gelen etki alanı mantığını temsil eden nesneleri ifade eder. Model, MVC tabanlı bir uygulamanın "kalp" ve daha sonra temel olarak davranmasından daha sonra görüyoruz.

ASP.NET MVC çerçevesi herhangi bir veri erişim teknolojisini kullanmayı destekler ve geliştiriciler, LINQ to Entities, LINQ to SQL, Nhazırda beklet, LLBLGen Pro, SubSonic, Solsonorm veya yalnızca ham ADO gibi modellerini uygulamak için çeşitli zengin .NET veri seçenekleri arasından seçim yapabilir. NET DataReaders veya veri kümeleri.

Nerdakşam yemeği uygulamamız için, veritabanı tasarımlarımıza oldukça yakından karşılık gelen basit bir model oluşturmak üzere LINQ to SQL kullanacağız ve bazı özel doğrulama mantığı ve iş kuralları ekler. Daha sonra, veri Kalıcılık uygulamasını uygulamanın geri kalanından soyutlamanıza yardımcı olan bir depo sınıfı uygulayacağız ve kolayca birim test etmemizi sağlar.

### <a name="linq-to-sql"></a>LINQ - SQL

LINQ to SQL, .NET 3,5 'nin bir parçası olarak gönderilen bir ORM (nesne ilişkisel Eşleyici).

LINQ to SQL, veritabanı tablolarını, kodladığı .NET sınıflarıyla eşleştirmek için kolay bir yol sağlar. Nerdakşam yemeği uygulamamız için, veritabanımızda bulunan Dinetleri ve RSVP tablolarını akşam yemeği ve RSVP sınıflarıyla eşlemek üzere bu uygulamayı kullanacağız. Dinde ve RSVP tablolarının sütunları, akşam yemeği ve RSVP sınıflarının özelliklerine karşılık gelir. Her akşam yemeği ve RSVP nesnesi, veritabanındaki dinde veya RSVP tablolarında ayrı bir satırı temsil eder.

LINQ to SQL, veritabanı verileriyle akşam yemeği ve RSVP nesnelerini almak ve güncelleştirmek için el ile SQL deyimlerini oluşturma zorunluluğunu ortadan kaldırmanıza olanak tanır. Bunun yerine, akşam yemeği ve RSVP sınıflarını, veritabanlarının veritabanına/üzerinden nasıl eşlendiğini ve aralarındaki ilişkileri tanımlayacağız. LINQ to SQL, etkileşim kurarken ve kullanırken çalışma zamanında kullanmak üzere uygun SQL yürütme mantığını oluşturma işlemini gerçekleştirir.

VB 'de LINQ dil desteğini kullanabilir ve C# veritabanından akşam YEMEĞI ve RSVP nesnelerini alan ifade sorguları yazabilirsiniz. Bu, yazmamız gereken veri kodu miktarını en aza indirir ve gerçekten temiz uygulamalar oluşturmamızı sağlar.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>LINQ to SQL sınıfları projemizi ekleme

Projemizdeki "modeller" klasörüne sağ tıklayıp ardından **&gt;yeni öğe Ekle** menü komutunu seçerek başlayacağız:

![](build-a-model-with-business-rule-validations/_static/image1.png)

Bu, "yeni öğe Ekle" iletişim kutusunu getirir. "Veri" kategorisine göre filtreleyecek ve içindeki "LINQ to SQL sınıfları" şablonunu seçeceğiz:

![](build-a-model-with-business-rule-validations/_static/image2.png)

"Nerdakşam yemeği" öğesini adlandırın ve "Ekle" düğmesine tıklayın. Visual Studio, \Modeller dizinimizin altına bir Nerdakşam yemeği. dbml dosyası ekleyecek ve ardından LINQ to SQL nesne ilişkisel tasarımcısını açacaktır:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ to SQL ile veri modeli sınıfları oluşturma

LINQ to SQL, mevcut veritabanı şemasından hızlı bir şekilde veri modeli sınıfları oluşturmamızı sağlar. Bunu yapmak için, Sunucu Gezgini Nerdakşam yemeği veritabanını açacak ve içinde modelleme yaptığımız tabloları seçeceğiz:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Daha sonra tabloları LINQ to SQL tasarımcı yüzeyine sürükleyebiliriz. Bunu yaptığımız LINQ to SQL, tabloların şemasını kullanarak otomatik olarak akşam yemeği ve RSVP sınıfları oluşturur (veritabanı tablosu sütunlarıyla eşlenen sınıf özellikleriyle birlikte):

![](build-a-model-with-business-rule-validations/_static/image5.png)

Varsayılan olarak, bir veritabanı şemasını temel alan sınıflar oluşturduğunda, LINQ to SQL tasarımcı, tablo ve sütun adlarını otomatik olarak "pluralleştirir". Örneğin: Yukarıdaki örneğimizdeki "dinlenebilir" tablosu, "akşam yemeği" sınıfı ile sonuçlandı. Bu sınıf adlandırması, modellerimizin .NET adlandırma kurallarıyla tutarlı olmasına yardımcı olur ve genellikle Tasarımcı 'nın bu çözümü (özellikle de çok sayıda tablo eklerken) düzeltmesine sahip olduğunu buldum. Tasarımcının oluşturduğu bir sınıfın veya özelliğin adını beğenmezseniz, her zaman geçersiz kılabilir ve istediğiniz adla değiştirebilirsiniz. Bunu, tasarımcı içinde varlık/özellik adını düzenleyerek ya da Özellik Kılavuzu aracılığıyla değiştirerek yapabilirsiniz.

Varsayılan olarak LINQ to SQL tasarımcı, tabloların birincil anahtar/yabancı anahtar ilişkilerini de inceler ve bunlara dayalı olarak, oluşturduğu farklı model sınıfları arasında varsayılan "ilişki ilişkilendirmelerini" otomatik olarak oluşturur. Örneğin, dinetleri ve RSVP tablolarını LINQ to SQL tasarımcı 'ya sürükleytiğimiz zaman, RSVP tablosunun dinlenebilir tabloya yabancı anahtar sahip olduğu olgusuna göre çıkarsandı. (Bu, içindeki okla belirtilir Tasarımcı):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Yukarıdaki ilişki, LINQ to SQL, geliştiricilerin belirli bir RSVP ile ilişkili olan akşam yemeği 'ya erişmek için kullanabileceği RSVP sınıfına kesin olarak yazılmış bir "akşam yemeği" özelliği eklemesine neden olur. Ayrıca, akşam yemeği sınıfının, geliştiricilerin belirli bir akşam yemeği ile ilişkili RSVP nesnelerini almasını ve güncelleştirmesini sağlayan bir "RSVPs" koleksiyon özelliğine sahip olmasına neden olur.

Aşağıda, Visual Studio 'da yeni bir RSVP nesnesi oluşturduğumuz ve bunu akşam yemeği 'nin RSVPs koleksiyonuna ekleyen bir IntelliSense örneği görebilirsiniz. LINQ to SQL akşam yemeği nesnesine otomatik olarak bir "RSVPs" koleksiyonu ekleme hakkında dikkat edin:

![](build-a-model-with-business-rule-validations/_static/image7.png)

Akşam yemeği 'nin RSVPs koleksiyonuna RSVP nesnesini ekleyerek, veritabanımızda akşam yemeği ve RSVP satırı arasında yabancı anahtar ilişki ilişkilendirmesi LINQ to SQL söyliyoruz:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Tasarımcının bir tablo ilişkilendirmesini modellenmiş veya adlandırılmış olarak beğenmezseniz, bunu geçersiz kılabilirsiniz. Tasarımcı içindeki ilişki okuna tıkladıktan sonra, özellik Kılavuzu aracılığıyla yeniden adlandırmak, silmek veya değiştirmek için özelliklerine erişmeniz yeterlidir. Nerdakşam yemeği uygulamamız için, varsayılan ilişkilendirme kuralları oluşturmakta olduğumuz veri modeli sınıfları için iyi çalışır ve yalnızca varsayılan davranışı kullanabiliriz.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext sınıfı

Visual Studio, LINQ to SQL Tasarımcısı kullanılarak tanımlanan modelleri ve veritabanı ilişkilerini temsil eden .NET sınıfları otomatik olarak oluşturur. Çözüme eklenen her bir LINQ to SQL tasarımcı dosyası için LINQ to SQL DataContext Sınıfı da oluşturulur. "Nerdakşam yemeği" adlı LINQ to SQL sınıf öğesini adlandırdığımız için, oluşturulan DataContext Sınıfı "NerdDinnerDataContext" olarak adlandırılacaktır. Bu NerdDinnerDataContext sınıfı, veritabanıyla etkileşime gitireceğiz birincil yoldur.

NerdDinnerDataContext sınıfımızda, veritabanı içinde modellendiğimiz iki tabloyu temsil eden iki Özellik ("dinlenebilir" ve "RSVPs") kullanıma sunar. Veritabanından akşam yemeği C# ve RSVP nesnelerini sorgulamak ve almak için bu ÖZELLIKLERE karşı LINQ sorguları yazmak üzere kullanabiliriz.

Aşağıdaki kod, bir NerdDinnerDataContext nesnesinin örneğini oluşturmayı ve gelecekte meydana gelen bir sıra elde etmek için bir LINQ sorgusu gerçekleştirmeyi gösterir. Visual Studio LINQ sorgusu yazarken tam IntelliSense sağlar ve bundan döndürülen nesneler kesin bir şekilde türdedir ve IntelliSense de desteklenir:

![](build-a-model-with-business-rule-validations/_static/image9.png)

NerdDinnerDataContext, akşam yemeği ve RSVP nesneleri için sorgulamanızı sağlayan ek olarak, bundan sonra geri aldığımız akşam yemeği ve RSVP nesnelerinde yaptığımız tüm değişiklikleri de otomatik olarak izler. Açık SQL update kodu yazmak zorunda kalmadan değişiklikleri veritabanına geri yüklemek için bu işlevi kullanabiliriz.

Örneğin, aşağıdaki kod, bir LINQ sorgusunun veritabanından tek bir akşam yemeği nesnesini almak, akşam yemeği özelliklerinden ikisini güncelleştirmek ve değişiklikleri veritabanına geri kaydetmek için nasıl kullanılacağını gösterir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Yukarıdaki koddaki NerdDinnerDataContext nesnesi, bundan sonra gelen akşam yemeği nesnesinde yapılan özellik değişikliklerini otomatik olarak izlendi. "SubmitChanges ()" yöntemini çağırdığımız zaman, güncelleştirilmiş değerlerin yeniden kalıcı hale getirilmesi için veritabanında uygun bir SQL "UPDATE" ifadesini yürütür.

### <a name="creating-a-dinnerrepository-class"></a>DinnerRepository sınıfı oluşturma

Küçük uygulamalar için, denetleyicilerin doğrudan bir LINQ to SQL DataContext sınıfına karşı çalışması ve denetleyicilere LINQ sorguları eklemesi çok iyi bir çalışmadır. Uygulamalar daha büyük olsa da, bu yaklaşım bakım ve test için çok daha fazla hale gelir. Aynı LINQ sorgularını birden fazla yerde çoğaltmamıza de yol açabilir.

Uygulamaları sürdürme ve test etme işlemlerini daha kolay hale getirmek için bir yaklaşım, "depo" deseninin kullanılması. Bir depo sınıfı, veri sorgulama ve kalıcılık mantığını kapsüllemeye yardımcı olur ve veri kalıcılığının uygulama ayrıntılarını uygulamadan soyutlar. Uygulama kodu temizleyici yapmanın yanı sıra, bir depo deseninin kullanılması gelecekte veri depolama uygulamalarının değiştirilmesini kolaylaştırabilir ve gerçek bir veritabanı gerekmeden bir uygulamanın birim testini kolaylaştırmaya yardımcı olabilir.

Nerdakşam yemeği uygulamamız için aşağıdaki imzaya sahip bir DinnerRepository sınıfı tanımlayacağız:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Note: Bu bölümde daha sonra bu sınıftan bir IDinnerRepository arabirimini ayıklayıp Denetleyicilerimizden bu sınıftan bağımlılık ekleme işlemini etkinleştireceğiz. Bununla birlikte başlamak için, basit bir başlangıç yapın ve doğrudan DinnerRepository sınıfıyla çalışmaya devam ediyoruz.*

Bu sınıfı uygulamak için "modeller" klasörünüze sağ tıklayıp **&gt;yeni öğe Ekle** menü komutunu seçin. "Yeni öğe Ekle" iletişim kutusunda "sınıf" şablonunu seçeceğiz ve "DinnerRepository.cs" dosyasını adı vereceğiz:

![](build-a-model-with-business-rule-validations/_static/image10.png)

Daha sonra DinnerRepository sınıfınızı aşağıdaki kodu kullanarak uygulayabiliriz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>DinnerRepository sınıfını kullanarak alma, güncelleştirme, ekleme ve silme

DinnerRepository sınıfınızı oluşturduğumuza göre, bununla birlikte yapabilmemiz için sık kullanılan görevleri gösteren birkaç kod örneğini inceleyelim:

#### <a name="querying-examples"></a>Örnek sorgulama

Aşağıdaki kod DinnerID değerini kullanarak tek bir akşam yemeği alır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Aşağıdaki kod, tüm yaklaşan geri layıcılar ve bunlara yönelik döngüleri alır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>INSERT ve Update örnekleri

Aşağıdaki kod, iki yeni dinde eklemeyi gösterir. Depoya yapılan eklemeler/değişiklikler, "Save ()" yöntemi çağrılana kadar veritabanına yürütülmedi. LINQ to SQL, bir veritabanı işleminde tüm değişiklikleri otomatik olarak kaydırır. bu nedenle, depomız kaydettiğinde tüm değişiklikler gerçekleşir veya hiçbirini kullanmaz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Aşağıdaki kod, var olan bir akşam yemeği nesnesini alır ve üzerinde iki özelliği değiştirir. Depomızda "Save ()" yöntemi çağrıldığında değişiklikler veritabanına geri kaydedilir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Aşağıdaki kod bir akşam yemeği alır ve buna bir RSVP ekler. Bunu, RSVPs için oluşturulan akşam yemeği LINQ to SQL nesnesindeki koleksiyonunu kullanarak yapar (veritabanında ikisi arasında birincil anahtar/yabancı anahtar ilişkisi olduğundan). Bu değişiklik, depoda "Save ()" yöntemi çağrıldığında yeni bir RSVP tablo satırı olarak veritabanına geri kaydedilir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Örneği Sil

Aşağıdaki kod, var olan bir akşam yemeği nesnesini alır ve sonra silinecek şekilde işaretler. Depoda "Save ()" yöntemi çağrıldığında, silme işlemi veritabanına geri alınacaktır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Doğrulama ve Iş kuralı mantığını model sınıflarıyla tümleştirme

Doğrulama ve iş kuralı mantığını tümleştirmek, verilerle birlikte çalışarak herhangi bir uygulamanın önemli bir parçasıdır.

#### <a name="schema-validation"></a>Şema doğrulama

Model sınıfları LINQ to SQL Tasarımcısı kullanılarak tanımlandığında, veri modeli sınıflarında özelliklerin veri türleri veritabanı tablosunun veri türlerine karşılık gelir. Örneğin: dinlenebilir tablosundaki "EventDate" sütunu bir "TarihSaat" ise, LINQ to SQL tarafından oluşturulan veri modeli sınıfı "DateTime" (yerleşik bir .NET veri türü) türünde olacaktır. Bu, koddan bir tamsayı veya Boole değeri atamayı denerseniz derleme hataları alacağınız anlamına gelir ve bu, geçerli olmayan bir dize türünü çalışma zamanında buna örtük olarak dönüştürmeye çalışırsanız bir hata otomatik olarak yükseltir.

LINQ to SQL, dizeleri kullanırken kaçış SQL değerlerini otomatik olarak işler; bu da, kullanırken SQL ekleme saldırılarına karşı korunmanıza yardımcı olur.

#### <a name="validation-and-business-rule-logic"></a>Doğrulama ve Iş kuralı mantığı

Şema doğrulaması ilk adım olarak faydalıdır, ancak nadiren yeterlidir. Birçok gerçek dünyada senaryo, birden çok özelliğe yayılabilen daha zengin doğrulama mantığı belirtme, kod yürütme ve genellikle bir modelin durumunu tanıma (örneğin: veya "arşivlenmiş" gibi bir etki alanına özgü durum içinde). Model sınıflarına doğrulama kuralları tanımlamak ve uygulamak için kullanılabilecek çeşitli farklı desenler ve çerçeveler vardır ve bu konuda yardımcı olmak için kullanılabilecek çeşitli .NET tabanlı çerçeveler vardır. ASP.NET MVC uygulamalarında neredeyse her türlü uygulamayı kullanabilirsiniz.

Nerdakşam yemeği uygulamanızın amaçları doğrultusunda, akşam yemeği model nesnemiz üzerinde IsValid özelliği ve Getruleihlalleri () yöntemi sergilediğimiz görece basit ve düz ileri bir model kullanacağız. IsValid özelliği, doğrulamanın ve iş kurallarının tümünün geçerli olup olmadığına bağlı olarak true veya false değerini döndürür. Getruleihlalleri () yöntemi herhangi bir kural hatalarının listesini döndürür.

Projenize bir "partial class" ekleyerek akşam yemeği modelimiz için IsValid ve Getruleihlalleri () uygulayacağız. Kısmi sınıflar, bir VS Designer tarafından tutulan sınıflara Yöntemler/Özellikler/olaylar eklemek için kullanılabilir (LINQ to SQL tasarımcı tarafından oluşturulan akşam yemeği sınıfı gibi) ve araç kodumuza ulaşmaktan kaçınmaya yardımcı olur. \Modeller klasörüne sağ tıklayıp "yeni öğe Ekle" menü komutunu seçerek projemizi yeni bir kısmi sınıf ekleyebiliriz. Daha sonra "yeni öğe Ekle" iletişim kutusunda "sınıf" şablonunu seçebilir ve Dinner.cs adını verebilirsiniz.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"Ekle" düğmesine tıkladığınızda projemizi bir Dinner.cs dosyası ekleyecek ve IDE içinde açacaktır. Daha sonra aşağıdaki kodu kullanarak temel bir kural/doğrulama zorlama çerçevesi uygulayabiliriz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Yukarıdaki kodla ilgili birkaç Not:

- Akşam yemeği sınıfı bir "partial" anahtar sözcüğüyle önceden geliyor. Bu, içinde yer alan kodun, LINQ to SQL tasarımcı tarafından oluşturulan/tutulan ve tek bir sınıfta derlenen sınıfla birleştirileceği anlamına gelir.
- Ruleihlalin sınıfı, bir kural ihlali hakkında daha fazla ayrıntı sağlayabilmemiz için projeye ekleyeceğiniz bir yardımcı sınıftır.
- Akşam yemeği. Getruleihlalleri () yöntemi doğrulama ve iş kurallarımızın değerlendirilmesine neden olur (bunları kısa süre içinde uygulayacağız). Daha sonra herhangi bir kural hatası hakkında daha fazla ayrıntı sağlayan Ruleihlal nesnelerinin bir dizisini geri döndürür.
- Akşam yemeği. IsValid özelliği, akşam yemeği nesnesinde etkin Ruleihlal olup olmadığını gösteren kullanışlı bir yardımcı özellik sağlar. Her zaman akşam yemeği nesnesi kullanılarak bir geliştirici tarafından proaktif olarak denetlenebilir (ve bir özel durum oluşturmaz).
- Akşam yemeği. OnValidate () kısmi yöntemi, akşam yemeği nesnesinin veritabanı içinde kalıcı hale geçmek üzere olduğu her zaman bildirim almamızı sağlayan bir kanca LINQ to SQL. Yukarıdaki OnValidate () uygulamamız, akşam yemeği 'nin kaydedilmeden önce Ruleihlal olmamasını sağlar. Geçersiz bir durumdaysa, LINQ to SQL işlemi iptal etmek için bir özel durum oluşturur.

Bu yaklaşım, doğrulama ve iş kurallarını ' de tümleştirebilmemiz için basit bir çerçeve sağlar. Şimdilik, Getruleihlalleri () yöntemine aşağıdaki kuralları ekleyelim:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Kural Ihlallerinin bir dizisini döndürmek C# için "yield return" özelliğini kullanıyoruz. Yukarıdaki ilk altı kural denetimi yalnızca akşam yemeği 'daki dize özelliklerinin null ya da boş olamaz. Son kural biraz daha ilgi çekici olduğundan, ContactPhone sayı biçiminin akşam yemeği ülkesinden eşleştiğini doğrulamak üzere projemizi ekleyebilmemiz için bir PhoneValidator. ısvalidnumber () yardımcı yöntemi çağırır.

' İ kullanabilirsiniz. Bu telefon doğrulama desteğini uygulamak için NET 'in normal ifade desteği. Aşağıda ülkeye özgü Regex desenli denetimleri ekleyebilmemiz için projemizi ekleyebileceğimiz basit bir PhoneValidator uygulamasıdır:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Doğrulama ve Iş mantığı Ihlallerini işleme

Yukarıdaki doğrulama ve iş kuralı kodunu ekledik, şimdi de bir akşam yemeği oluşturmayı veya güncelleştirmeyi denediğimiz her seferinde doğrulama mantığı kuralları değerlendirilir ve zorlanır.

Geliştiriciler, bir akşam yemeği nesnesinin geçerli olup olmadığını önceden belirleme ve özel durum oluşturmadan tüm ihlallerin bir listesini alma için aşağıda gibi kod yazabilir:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Bir akşam yemeği 'yi geçersiz bir durumda kaydetmeye çalışdığımızda, DinnerRepository üzerinde Save () yöntemini çağırdığınızda bir özel durum oluşur. Bunun LINQ to SQL nedeni, akşam yemeği. OnValidate () kısmi yöntemimizi Dinner Now 'ın değişikliklerini kaydetmeden önce otomatik olarak çağırdığı ve akşam yemeği. OnValidate () öğesine kod ekledik. Bu özel durumu yakalayabilir ve düzeltilmesi için ihlallerin bir listesini yeniden etkin bir şekilde alabilirsiniz:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Doğrulama ve iş kurallarımız, Kullanıcı arabirimi katmanında değil, model katmanımız içinde uygulandığından ve uygulamamız içindeki tüm senaryolarda kullanılacak ve bu kurallar kullanılacaktır. Daha sonra iş kurallarını değiştirebilir veya ekleyebiliriz ve akşam yemeği nesnelerimiz ile birlikte çalışarak tüm kodların bunları kabul eteceğiz.

Uygulama ve Kullanıcı arabirimi mantığı genelinde bu değişikliklere gerek kalmadan, iş kurallarını tek bir yerde değiştirme esnekliğine sahip olmak, iyi yazılmış bir uygulamanın bir işareti ve MVC çerçevesinin teşvik etmesine yardımcı olan bir avantajdır.

### <a name="next-step"></a>Sonraki adım

Şimdi, veritabanımızı sorgulamak ve güncelleştirmek için kullanabilmemiz gereken bir model sunuyoruz.

Şimdi de, bir HTML Kullanıcı arabirimi deneyimi oluşturmak için kullanabilmemiz için projeye bazı denetleyiciler ve görünümler ekleyelim.

> [!div class="step-by-step"]
> [Önceki](create-a-database.md)
> [İleri](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
