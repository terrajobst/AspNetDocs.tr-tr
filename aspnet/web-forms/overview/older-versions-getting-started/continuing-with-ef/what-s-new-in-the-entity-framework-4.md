---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4,0 ' deki yenilikler | Microsoft Docs
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642676"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0 Sürümündeki Yenilikler

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, Entity Framework öğretici serisi [Ile çalışmaya](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) . Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.

Önceki öğreticide, Entity Framework kullanan bir Web uygulamasının performansını en üst düzeye çıkarmak için bazı yöntemler gördünüz. Bu öğretici, Entity Framework sürüm 4 ' teki en önemli yeni özelliklerden bazılarını inceler ve tüm yeni özelliklere daha kapsamlı bir giriş sağlayan kaynaklara bağlanır. Bu öğreticide vurgulanan özellikler şunlardır:

- Yabancı anahtar ilişkilendirmeleri.
- Kullanıcı tanımlı SQL komutları yürütülüyor.
- Model ilk geliştirme.
- POCO desteği.

Ayrıca öğretici, Entity Framework sonraki sürümünde gelen bir özellik olan *kod öncelikli geliştirmeyi*kısaca tanıtacaktır.

Öğreticiyi başlatmak için, Visual Studio 'Yu başlatın ve önceki öğreticide birlikte çalıştığınız Contoso University Web uygulamasını açın.

## <a name="foreign-key-associations"></a>Yabancı anahtar Ilişkilendirmeleri

Entity Framework bulunan gezinti özelliklerinin 3,5 sürümü, ancak veri modelinde yabancı anahtar özellikleri içermiyor. Örneğin, `StudentGrade` tablosunun `CourseID` ve `StudentID` sütunları `StudentGrade` varlığından atlanacaktır.

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

Bu yaklaşımın nedeni, tamamen konuşuyor, yabancı anahtarlar fiziksel uygulama ayrıntısımıdır ve kavramsal bir veri modeline ait değildir. Ancak, pratik bir şekilde, yabancı anahtarlara doğrudan erişim sahibi olduğunuzda kodda varlıklarla çalışmak daha kolay olur.

Veri modelindeki yabancı anahtarların kodunuzu nasıl basitleştirebileceğini gösteren bir örnek için, *DepartmentsAdd. aspx* sayfasını bu olmadan nasıl kodlayacağınızı düşünün. `Department` varlığında `Administrator` özelliği, `Person` varlığındaki `PersonID` karşılık gelen bir yabancı anahtardır. Yeni bir departman ve yöneticisi arasındaki ilişkiyi oluşturmak için, tüm yapmanız gerekiyordu, veri bağlama denetiminin `ItemInserting` olay işleyicisinde `Administrator` özelliğinin değerini ayarladı:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

Veri modelinde yabancı anahtarlar olmadan, varlık kümesine eklenmeden önce varlığa bir başvuru almak için veri kaynağı denetiminin `ItemInserting` olayı yerine veri kaynağı denetiminin `Inserting` olayını idare edersiniz. Bu başvuruya sahip olduğunuzda, aşağıdaki örneklerde olduğu gibi kodu kullanarak ilişkilendirmeyi kurarsınız:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

Entity Framework ekibin [blog gönderisini yabancı anahtar İlişkilendirmelerde](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)görebileceğiniz gibi, kod karmaşıklığının farkının çok daha büyük olduğu başka durumlar da vardır. Daha basit kod için kavramsal veri modelinde uygulama ayrıntıları ile canlı olmayı tercih eden kişilerin ihtiyaçlarını karşılamak için Entity Framework artık veri modeline yabancı anahtarlar ekleme seçeneği sunar.

Entity Framework terminoloji ' de, yabancı *anahtar ilişkilendirmelerini*kullandığınız veri modeline yabancı anahtarlar eklerseniz ve yabancı anahtarları dışladığınızda *bağımsız ilişkilendirmeler*kullanıyorsunuz demektir.

## <a name="executing-user-defined-sql-commands"></a>Kullanıcı tanımlı SQL komutları yürütülüyor

Entity Framework önceki sürümlerinde, kendi SQL komutlarınızı hızlı bir şekilde oluşturmak ve çalıştırmak için kolay bir yol yoktu. Sizin için dinamik olarak oluşturulan Entity Framework ya da bir saklı yordam oluşturup bir işlev olarak içeri aktarmanız gerekiyordu. Sürüm 4 ' te, herhangi bir sorguyu doğrudan veritabanına geçirmenize daha kolay hale gelen `ObjectContext` sınıfına `ExecuteStoreQuery` ve `ExecuteStoreCommand` yöntemleri eklenir.

Contoso Üniversitesi yöneticilerinin, saklı bir yordam oluşturma ve veri modeline aktarma sürecini gerçekleştirmeden, veritabanında toplu değişiklikler gerçekleştirebilmesini istediğini varsayalım. İlk istekleri, veritabanındaki tüm kurslar için kredilerin sayısını değiştirmesine izin veren bir sayfa içindir. Web sayfasında, her `Course` satırı `Credits` sütununun değerini çarpmak için kullanılacak bir sayı girebilmek ister.

*Site. Master* ana sayfasını kullanan yeni bir sayfa oluşturun ve bunu *updatekrediler. aspx*olarak adlandırın. Ardından aşağıdaki biçimlendirmeyi `Content2`adlı `Content` denetimine ekleyin:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

Bu biçimlendirme, kullanıcının çarpan değerini girebileceği bir `TextBox` denetimi oluşturur, komutu yürütmek için tıklamayı bir `Button` denetimi ve etkilenen satır sayısını belirten bir `Label` denetimi oluşturur.

*UpdateCredits.aspx.cs*'i açın ve düğmenin `Click` olayı için aşağıdaki `using` ifadesini ve işleyiciyi ekleyin:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

Bu kod, metin kutusundaki değeri kullanarak SQL `Update` komutunu yürütür ve etkilenen satır sayısını göstermek için etiketini kullanır. Sayfayı çalıştırmadan önce, bazı verilerin "önceki" bir resmini almak için *Kurslar. aspx* sayfasını çalıştırın.

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

*Updatekrediler. aspx*' i çalıştırın, çarpan olarak "10" yazın ve ardından **Yürüt**' e tıklayın.

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

Değiştirilen verileri görmek için *Kurslar. aspx* sayfasını yeniden çalıştırın.

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(Kredi sayısını özgün değerlerine geri ayarlamak istiyorsanız, *UpdateCredits.aspx.cs* Değiştir ' de `Credits * {0}` `Credits / {0}` ve sayfayı yeniden çalıştırıp, bölen olarak 10 ' u girerek.)

Kodda tanımladığınız sorguları yürütme hakkında daha fazla bilgi için bkz. [nasıl yapılır: komutları veri kaynağında doğrudan yürütme](https://msdn.microsoft.com/library/ee358769.aspx).

## <a name="model-first-development"></a>Model-Ilk geliştirme

Bu izlenecek yollarda, önce veritabanını oluşturup ardından veritabanı yapısına bağlı olarak veri modelini oluşturmuş olursunuz. Entity Framework 4 ' te, bunun yerine veri modeliyle başlayabilir ve veri modeli yapısına bağlı olarak veritabanı oluşturabilirsiniz. Veritabanının zaten mevcut olmadığı bir uygulama oluşturuyorsanız, model ilk yaklaşım uygulama için kavramsal anlamda anlamlı olan varlıklar ve ilişkiler oluşturmanızı sağlarken fiziksel uygulama ayrıntıları konusunda endişelenmenize olanak sağlar . (Bu, ancak yalnızca geliştirme aşamaları aracılığıyla doğru kalır. Sonuç olarak veritabanı oluşturulur ve burada üretim verilerine sahip olur ve modelden yeniden oluşturmak artık pratik olmayacaktır; Bu noktada, veritabanı ilk yaklaşımına geri dönebilirsiniz.)

Öğreticinin bu bölümünde basit bir veri modeli oluşturacak ve veritabanını bundan oluşturacaksınız.

**Çözüm Gezgini** *dal* klasörüne sağ tıklayın ve **Yeni öğe Ekle**' yi seçin. **Yeni öğe Ekle** iletişim kutusunda, **yüklü şablonlar** altında **veri** ' ı seçin ve ardından **ADO.net varlık veri modeli** şablonunu seçin. Yeni dosyayı *Alumniassociationmodel. edmx* olarak adlandırın ve **Ekle**' ye tıklayın.

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

Bu, Varlık Veri Modeli Sihirbazı 'Nı başlatır. **Model Içeriğini seçin** adımında **boş model** ' i seçin ve ardından **son**' a tıklayın.

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

**Varlık veri modeli Tasarımcısı** boş bir tasarım yüzeyi ile açılır. **Araç kutusundan** bir **varlık** öğesini tasarım yüzeyine sürükleyin.

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

`Entity1` varlık adını `Alumnus`olarak değiştirin, `Id` özellik adını `AlumnusId`olarak değiştirin ve `Name`adlı yeni bir skaler özellik ekleyin. Yeni özellikler eklemek için `Id` sütununun adını değiştirdikten sonra ENTER tuşuna basabilir veya varlığa sağ tıklayıp **skalar Özellik Ekle**' yi seçebilirsiniz. Yeni özellikler için varsayılan tür, bu basit gösteride ince `String`, ancak **Özellikler** penceresinde veri türü gibi şeyleri değiştirebilirsiniz.

Aynı şekilde başka bir varlık oluşturun ve `Donation`adlandırın. `Id` özelliğini `DonationId` olarak değiştirip `DateAndAmount`adlı bir skaler özellik ekleyin.

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

Bu iki varlık arasında bir ilişki eklemek için `Alumnus` varlığına sağ tıklayın, **Ekle**' yi seçin ve ardından **ilişkilendirme**' yi seçin.

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

**Ilişki Ekle** iletişim kutusundaki varsayılan değerler, istediğiniz şeydir (bire çok, gezinme özellikleri dahil, yabancı anahtarlar dahil), bu nedenle **Tamam**' a tıklamanız yeterlidir.

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

Tasarımcı bir ilişkilendirme satırı ve yabancı anahtar özelliği ekler.

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

Artık veritabanını oluşturmaya hazır olursunuz. Tasarım yüzeyine sağ tıklayın ve **modelden veritabanı oluştur**' u seçin.

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

Bu, veritabanı oluşturma Sihirbazı 'Nı başlatır. (Varlıkların eşlenmediğine işaret eden uyarılar görürseniz, bu süreyi göz ardı edebilirsiniz.)

**Veri bağlantınızı seçin** adımında **Yeni bağlantı**' ya tıklayın.

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

**Bağlantı özellikleri** iletişim kutusunda yerel SQL Server Express örneğini seçin ve veritabanını `AlumniAssociation`adlandırın.

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet** ' e tıklayın. **Veri bağlantınızı seçin** adımı yeniden görüntüleniyorsa, **İleri**' ye tıklayın.

**Özet ve ayarlar** adımında **son**' a tıklayın.

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

Veri tanımlama dili (DDL) komutlarıyla bir *. SQL* dosyası oluşturulur, ancak komutlar henüz çalıştırılmadı.

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

Başlangıç [öğreticisi serisinde ilk öğreticinin](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)`School` veritabanını oluştururken yaptığınız gibi, komut dosyasını çalıştırmak ve tabloları oluşturmak için **SQL Server Management Studio** gibi bir araç kullanın. (Veritabanını indirmediğiniz müddetçe.)

Artık, Web sayfalarınızdaki `AlumniAssociation` veri modelini, `School` modelini kullandığınız şekilde kullanabilirsiniz. Bunu denemek için tablolara bazı veriler ekleyin ve verileri görüntüleyen bir Web sayfası oluşturun.

**Sunucu Gezgini**kullanarak, `Alumnus` ve `Donation` tablolarına aşağıdaki satırları ekleyin.

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

*Site. Master* ana sayfasını kullanan *alumnı. aspx* adlı yeni bir Web sayfası oluşturun. Aşağıdaki biçimlendirmeyi `Content2`adlı `Content` denetimine ekleyin:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

Bu biçimlendirme, iç içe geçmiş `GridView` denetimleri ve alumnı adlarını ve iç birini görüntüleyen bağış tarihleri ve miktarları göstermek için dıştaki bir oluşturur.

*Alumni.aspx.cs*'i açın. Veri erişim katmanı için bir `using` açıklaması ve dış `GridView` denetiminin `RowDataBound` olayına yönelik bir işleyici ekleyin:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

Bu kod, geçerli satırın `Alumnus` varlığının `Donations` gezinti özelliğini kullanarak iç `GridView` denetimini databinds.

Sayfayı çalıştırın.

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(Unutmayın: Bu sayfa indirilebilir projede bulunur, ancak bunu yapmak için yerel SQL Server Express Örneğinizde veritabanını oluşturmanız gerekir; veritabanı *App\_Data* klasörüne bir *. mdf* dosyası olarak dahil değildir.)

Entity Framework model-ilk özelliğini kullanma hakkında daha fazla bilgi için, [Entity Framework 4 ' te model-ilk](https://msdn.microsoft.com/data/ff830362.aspx)' a bakın.

## <a name="poco-support"></a>POCO Desteği

Etki alanı odaklı tasarım yöntemini kullandığınızda, iş etki alanıyla ilgili verileri ve davranışları temsil eden veri sınıfları tasarlayaöneririz. Bu sınıfların verileri depolamak (kalıcı hale getirmek) için kullanılan herhangi bir teknolojiden bağımsız olması gerekir; diğer bir deyişle, *Kalıcılık Ignorant*olmalıdır. Birim testi projesi, test etmek için en uygun Kalıcılık teknolojisini kullanabilmesi için kalıcılık Ignorance Ayrıca bir sınıfı birim testi için daha kolay hale getirir. Entity Framework önceki sürümlerinde, varlık sınıflarının `EntityObject` sınıftan devralması ve bu nedenle Entity Framework özgü işlevlerin harika bir şekilde sunulması gerektiğinden, kalıcılık kalıcılığı için sınırlı destek sunuluyor.

Entity Framework 4 ' te, `EntityObject` sınıfından kalıtımla almayan varlık sınıflarını kullanma özelliği tanıtılmıştır ve bu nedenle Kalıcılık Ignorant olur. Entity Framework bağlamında, bu gibi sınıflar genellikle *düz eskı clr nesneleri* (poco veya Pocos) olarak adlandırılır. POCO sınıflarını el ile yazabilir veya Entity Framework tarafından sunulan metin şablonu dönüştürme araç seti (T4) şablonlarını kullanarak var olan bir veri modeline göre otomatik olarak oluşturabilirsiniz.

Entity Framework POCOs kullanma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [POCO varlıklarıyla çalışma](https://msdn.microsoft.com/library/dd456853.aspx). Bu, daha ayrıntılı bilgiler içeren diğer belgelerin bağlantılarıyla birlikte POCOs 'a genel bakış sağlayan bir MSDN belgesidir.
- [Izlenecek yol: Entity Framework IÇIN POCO şablonu](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) Bu, POCOs hakkındaki diğer blog gönderilerinin bağlantılarıyla birlikte Entity Framework geliştirme ekibinin bir blog gönderisine sahiptir.

## <a name="code-first-development"></a>Kod-Ilk geliştirme

Entity Framework 4 ' teki POCO desteği hâlâ bir veri modeli oluşturmanızı ve varlık sınıflarınızı veri modeline bağlamayı gerektirir. Entity Framework sonraki sürümünde, *kod ilk geliştirme*adlı bir özellik yer alır. Bu özellik, veri modeli Tasarımcısı veya veri modeli XML dosyası kullanmanıza gerek kalmadan kendi POCO sınıflarınızda Entity Framework kullanmanıza olanak sağlar. (Bu nedenle, bu seçenek *yalnızca kod*olarak da bilinir; yalnızca *kod* ve *kod* her ikisi de aynı Entity Framework özelliğine başvurur.)

Geliştirme için ilk kod yaklaşımı kullanma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Entity Framework 4 Ile kod Ilk geliştirme](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx). Bu, Scott Guthrie tarafından kod ilk geliştirmeyi tanıtan bir blog gönderisine sahiptir.
- [Entity Framework geliştirme ekibi blogu-yalnızca etiketlendirilmiş kod gönderme](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework geliştirme ekibi blogu-etiketli Code First postalar](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC müzik deposu öğreticisi-4. Bölüm: modeller ve veri erişimi](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [MVC 3 ile çalışmaya başlama-4. Bölüm: Entity Framework kodu-Ilk geliştirme](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

Buna ek olarak, Contoso University uygulamasına benzer bir uygulama oluşturan yeni bir MVC kod-Ilk öğretici, [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md) adresindeki 2011 baharında yayımlanacak.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu, Entity Framework yeniliklere genel bakış işlemini tamamlar ve bu işlem Entity Framework öğretici serisine devam eder. Burada kapsanmayan Entity Framework 4 ' teki yeni özellikler hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ADO.net 'deki](https://msdn.microsoft.com/library/ex6y04yf.aspx) yenilikler Entity Framework sürüm 4 ' teki yeni özellikler hakkında MSDN konusu.
- [Entity Framework 4 sürümü duyuruluyor](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) Entity Framework geliştirme ekibinin Web günlüğü, sürüm 4 ' teki yeni özelliklerle ilgili olarak göndermektedir.

> [!div class="step-by-step"]
> [Öncekini](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
