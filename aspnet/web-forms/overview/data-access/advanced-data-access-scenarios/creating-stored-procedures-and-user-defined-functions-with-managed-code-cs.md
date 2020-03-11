---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: Yönetilen kodla saklı yordamlar ve Kullanıcı tanımlı Işlevler oluşturma (C#) | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005, geliştiricilerin yönetilen kod aracılığıyla veritabanı nesneleri oluşturmalarına olanak tanımak için .NET ortak dil çalışma zamanına tümleştirilir. Bu öğretici...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: c6aec9ca70fe3ab568b3d17fea6bfd56671edc03
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533539"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>Yönetilen Kod ile Saklı Yordamlar ve Kullanıcı Tanımlı İşlevler Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) veya [PDF 'yi indirin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005, geliştiricilerin yönetilen kod aracılığıyla veritabanı nesneleri oluşturmalarına olanak tanımak için .NET ortak dil çalışma zamanına tümleştirilir. Bu öğreticide, Visual Basic veya C# kodunuzla yönetilen saklı yordamların ve yönetilen Kullanıcı tanımlı işlevlerin nasıl oluşturulacağı gösterilmektedir. Ayrıca, Visual Studio 'nun bu sürümlerinin bu tür yönetilen veritabanı nesnelerinin hatalarını ayıklamanıza nasıl izin veririz.

## <a name="introduction"></a>Giriş

Microsoft s SQL Server 2005 gibi veritabanları veri ekleme, değiştirme ve alma için [Transact-yapılandırılmış sorgu dili (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) kullanır. Çoğu veritabanı sisteminde, daha sonra tek, yeniden kullanılabilir bir birim olarak yürütülebilecek bir dizi SQL deyimini gruplandırmak için yapılar bulunur. Saklı yordamlar bir örnektir. Diğer bir deyişle, adım 9 ' da daha ayrıntılı olarak inceleyeceği bir yapı olan *Kullanıcı tanımlı işlevler*(UDF 'ler).

SQL, temel olarak veri kümeleriyle çalışmak üzere tasarlanmıştır. `SELECT`, `UPDATE`ve `DELETE` deyimleri, karşılık gelen tablodaki tüm kayıtlar için geçerlidir ve yalnızca `WHERE` yan tümceleriyle sınırlandırılır. Ancak, tek seferde bir kayıt ile çalışmak ve skaler verileri değiştirmek için tasarlanan birçok dil özelliği vardır. [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) bir kayıt kümesinin tek seferde bir arada döngüye eklenmesine izin verir. `LEFT`, `CHARINDEX`ve `PATINDEX` gibi dize işleme işlevleri skaler verilerle çalışır. SQL Ayrıca `IF` ve `WHILE`gibi denetim akışı deyimlerini içerir.

Microsoft SQL Server 2005 ' den önce, saklı yordamlar ve UDF 'ler yalnızca bir T-SQL deyimleri koleksiyonu olarak tanımlanabilir. Ancak, SQL Server 2005, tüm .NET derlemeleri tarafından kullanılan çalışma zamanı olan [ortak dil çalışma zamanı (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)ile tümleştirme sağlamak üzere tasarlanmıştır. Sonuç olarak, bir SQL Server 2005 veritabanındaki saklı yordamlar ve UDF 'ler, yönetilen kod kullanılarak oluşturulabilir. Diğer bir deyişle, bir C# sınıfında Yöntem olarak bir saklı yordam veya UDF oluşturabilirsiniz. Bu, bu saklı yordamların ve UDF 'ların .NET Framework ve kendi özel sınıflarınızda işlevselliği kullanmasına olanak sağlar.

Bu öğreticide, yönetilen saklı yordamlar ve Kullanıcı tanımlı Işlevler oluşturmayı ve bunları Northwind veritabanımızla nasıl tümleştirileceğini inceleyeceğiz. Haydi başlayın!

> [!NOTE]
> Yönetilen veritabanı nesneleri, SQL karşılıkları üzerinde bazı avantajlar sunar. Dil zenginliği ve açıklık ve mevcut kodu ve mantığı yeniden kullanma olanağı ana avantajlardır. Ancak, yönetilen veritabanı nesnelerinin çok yordamsal mantığı içermeyen veri kümeleriyle çalışırken daha az verimli olması olasıdır. Yönetilen kod kullanmanın avantajları hakkında daha kapsamlı bir tartışma için, [veritabanı nesneleri oluşturmak üzere yönetilen kod kullanmanın avantajlarını](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)inceleyin.

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>1\. Adım: Northwind veritabanını`App_Data` dışına taşıma

Tüm öğreticilerimiz, Web uygulaması s `App_Data` klasöründe bir Microsoft SQL Server 2005 Express Edition veritabanı dosyası kullandık. Veritabanını basit bir biçimde dağıtmak `App_Data` ve bu öğreticilerin çalıştırılması, tüm dosyalar bir dizinde bulunduğundan ve öğreticiyi test etmek için başka bir yapılandırma adımı gerekmediği için.

Bununla birlikte, bu öğreticide, s Northwind veritabanını `App_Data` dışına taşıyıp SQL Server 2005 Express Sürüm veritabanı örneğine açıkça kaydetlim. Bu öğreticide, `App_Data` klasöründeki veritabanıyla ilgili adımları gerçekleştirebilmemiz de, veritabanını SQL Server 2005 Express Sürüm veritabanı örneğiyle açıkça kaydederek birçok adım daha kolay hale getirilir.

Bu öğreticinin indirileceği iki veritabanı dosyası vardır `NORTHWND.MDF` ve `NORTHWND_log.LDF`, `DataFiles`adlı bir klasöre yerleştirilir. Kendi öğreticilerinin uygulanmasıyla birlikte takip ediyorsanız, Visual Studio 'Yu kapatın ve `NORTHWND.MDF` ve `NORTHWND_log.LDF` dosyalarını web sitesi s `App_Data` klasöründen Web sitesinin dışındaki bir klasöre taşıyın. Veritabanı dosyaları başka bir klasöre taşındıktan sonra Northwind veritabanını SQL Server 2005 Express Sürüm veritabanı örneğiyle kaydetmeniz gerekir. Bu, SQL Server Management Studio yapılabilir. Bilgisayarınızda SQL Server 2005 ' nin Express olmayan bir sürümüne sahipseniz, büyük olasılıkla Management Studio zaten yüklü. Bilgisayarınızda yalnızca SQL Server 2005 Express Sürüm varsa [Microsoft SQL Server Management Studio Express 'i](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)indirip yüklemek için biraz zaman ayırın.

SQL Server Management Studio başlatın. Şekil 1 ' de gösterildiği gibi, Management Studio sunucuya hangi sunucudan bağlanılacağını sorar. Sunucu adı için localhost\SQLExpress girin, kimlik doğrulaması açılır listesinden Windows kimlik doğrulaması ' nı seçin ve Bağlan ' a tıklayın.

![Uygun veritabanı örneğine bağlanma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**Şekil 1**: uygun veritabanı örneğine bağlanma

Bağlandıktan sonra, Nesne Gezgini penceresinde veritabanları, güvenlik bilgileri, yönetim seçenekleri gibi SQL Server 2005 Express Sürüm veritabanı örneğiyle ilgili bilgiler listelenir.

Northwind veritabanını `DataFiles` klasöre iliştirmemiz gerekir (veya dosyayı taşımış olabilirsiniz) SQL Server 2005 Express Sürüm veritabanı örneğine eklemektir. Veritabanları klasörüne sağ tıklayın ve bağlam menüsünden Ekle seçeneğini belirleyin. Bu işlem veritabanlarını Ekle iletişim kutusunu getirir. Ekle düğmesine tıklayın, uygun `NORTHWND.MDF` dosyasına gidin ve Tamam ' a tıklayın. Bu noktada, ekranınızda Şekil 2 ' ye benzer görünmelidir.

[![uygun veritabanı örneğine bağlanın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**Şekil 2**: uygun veritabanı örneğine bağlanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))

> [!NOTE]
> SQL Server 2005 Express Sürüm Management Studio örneğine bağlanırken veritabanları Iliştirme iletişim kutusu, Belgelerim gibi Kullanıcı profili dizinlerinde ayrıntıya geçmenize izin vermez. Bu nedenle, `NORTHWND.MDF` ve `NORTHWND_log.LDF` dosyalarını Kullanıcı profili olmayan bir dizine yerleştirdiğinizden emin olun.

Veritabanını eklemek için Tamam düğmesine tıklayın. Veritabanları Iliştir iletişim kutusu kapanır ve Nesne Gezgini artık tam olarak eklenmiş veritabanını listelemelidir. Northwind veritabanının `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`gibi bir adı vardır. Veritabanına sağ tıklayıp Yeniden Adlandır ' ı seçerek veritabanını Northwind olarak yeniden adlandırın.

![Veritabanını Northwind olarak yeniden adlandırma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**Şekil 3**: veritabanını Northwind olarak yeniden adlandırma

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>2\. Adım: Visual Studio 'da yeni bir çözüm ve SQL Server projesi oluşturma

SQL Server 2005 ' de yönetilen saklı yordamlar veya UDF 'ler oluşturmak için, saklı yordamı ve UDF mantığını bir sınıfta C# kod olarak yazacak. Kod yazıldıktan sonra, bu sınıfı bir derlemede derlemenize (bir `.dll` dosyası), derlemeyi SQL Server veritabanıyla kaydetmeniz ve sonra veritabanında karşılık gelen yönteme işaret eden bir saklı yordam ya da UDF nesnesi oluşturmanız gerekecektir. Bu adımların tümü el ile gerçekleştirilebilir. Kodu herhangi bir metin düzenleyicisinde oluşturabilir, C# derleyici kullanarak komut satırından derleyebiliriz ([`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx)), [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) komutunu veya Management Studio kullanarak veritabanına kaydedebilir ve benzer yollarla saklı yordamı veya UDF nesnesini ekleyebilirsiniz. Neyse ki, Visual Studio 'nun profesyonel ve Team Systems sürümleri, bu görevleri otomatikleştiren SQL Server bir proje türü içerir. Bu öğreticide, yönetilen bir saklı yordam ve UDF oluşturmak için SQL Server proje türünü kullanarak izlenecek yol göstereceğiz.

> [!NOTE]
> Visual Web Developer veya Visual Studio Standard Edition kullanıyorsanız, bunun yerine el ile yaklaşımı kullanmanız gerekir. 13. adım, bu adımları el ile gerçekleştirmeye yönelik ayrıntılı yönergeler sağlar. Bu adımlar, kullanmakta olduğunuz Visual Studio sürümü ne olursa olsun, uygulanması gereken önemli SQL Server yapılandırma yönergelerini içerdiğinden, adım 13 ' i okumadan önce 2 ile 12 arasındaki adımları okumanızı öneririz.

Visual Studio 'Yu açarak başlayın. Yeni proje iletişim kutusunu görüntülemek için Dosya menüsünden Yeni proje ' yi seçin (bkz. Şekil 4). Veritabanı projesi türünün detayına gidin ve sağ tarafta listelenen şablonlardan yeni bir SQL Server projesi oluşturmayı seçin. Bu proje `ManagedDatabaseConstructs` adı ve `Tutorial75`adlı bir çözüme yerleştirdim.

[Yeni bir SQL Server projesi oluşturma ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**Şekil 4**: yeni bir SQL Server projesi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))

Çözüm ve SQL Server proje oluşturmak için yeni proje iletişim kutusundaki Tamam düğmesine tıklayın.

Bir SQL Server projesi belirli bir veritabanına bağlıdır. Sonuç olarak, yeni SQL Server projesi oluşturduktan sonra bu bilgileri hemen belirtmemiz istenir. Şekil 5 ' te, 1. adımda SQL Server 2005 Express Sürüm veritabanı örneğine Kaydolduğumuz Northwind veritabanına işaret etmek üzere doldurulmuş yeni veritabanı başvurusu iletişim kutusu gösterilir.

![SQL Server projesini Northwind veritabanıyla ilişkilendir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**Şekil 5**: SQL Server projesini Northwind veritabanıyla ilişkilendirme

Bu proje içinde oluşturduğumuz yönetilen saklı yordamları ve UDF 'Leri hata ayıklaması yapmak için, bağlantı için SQL/CLR hata ayıklama desteğini etkinleştirmemiz gerekiyor. Bir SQL Server projesini yeni bir veritabanıyla ilişkilendirirken (Şekil 5 ' te yaptığımız gibi), Visual Studio, bağlantıda SQL/CLR hata ayıklamayı etkinleştirmek isteyip istemediğinizi sorar (bkz. Şekil 6). Evet’e tıklayın.

![SQL/CLR hata ayıklamayı etkinleştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**Şekil 6**: SQL/CLR hata ayıklamayı etkinleştir

Bu noktada yeni SQL Server projesi çözüme eklenmiştir. Projede oluşturulan yönetilen veritabanı nesnelerinde hata ayıklamak için kullanılan `Test.sql`adlı bir dosya ile `Test Scripts` adlı bir klasör içerir. Adım 12 ' de hata ayıklamaya bakacağız.

Artık bu projeye yeni yönetilen saklı yordamlar ve UDF 'ler ekleyebiliriz, ancak ilk olarak çözümde mevcut Web uygulamamıza izin vermeden önce Dosya menüsünden Ekle seçeneğini belirleyin ve mevcut Web sitesi ' ni seçin. Uygun Web sitesi klasörüne gidin ve Tamam ' a tıklayın. Şekil 7 ' de gösterildiği gibi bu, çözümü iki proje içerecek şekilde güncelleştirecektir: Web sitesi ve `ManagedDatabaseConstructs` SQL Server projesi.

![Çözüm Gezgini artık Iki proje Içeriyor](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**Şekil 7**: Çözüm Gezgini Şu anda Iki proje içeriyor

`Web.config` `NORTHWNDConnectionString` değeri şu anda `App_Data` klasöründeki `NORTHWND.MDF` dosyasına başvurmuş. Bu veritabanını `App_Data` sunucudan kaldırdık ve SQL Server 2005 Express Sürüm veritabanı örneğine açık olarak kaydettiniz, `NORTHWNDConnectionString` değerini buna karşılık olarak güncelleştirmeniz gerekir. Web sitesindeki `Web.config` dosyasını açın ve `NORTHWNDConnectionString` değerini bağlantı dizesinin okuduğu şekilde değiştirin: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`. Bu değişiklikten sonra, `Web.config` `<connectionStrings>` bölümü şuna benzer olmalıdır:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> [Önceki öğreticide](debugging-stored-procedures-cs.md)açıklandığı gibi, bir istemci uygulamasından bir ASP.NET Web sitesi gibi SQL Server nesnesinde hata ayıklarken bağlantı havuzunu devre dışı bıraktık. Yukarıda gösterilen bağlantı dizesi bağlantı havuzunu devre dışı bırakır (`Pooling=false`). Yönetilen saklı yordamlar ve UDF 'ler ASP.NET Web sitesinden hata ayıklamayı planlamıyorsanız bağlantı havuzunu etkinleştirin.

## <a name="step-3-creating-a-managed-stored-procedure"></a>3\. Adım: yönetilen saklı yordam oluşturma

Bir yönetilen saklı yordamı Northwind veritabanına eklemek için ilk olarak SQL Server projesinde saklı yordamı bir yöntem olarak oluşturmanız gerekir. Çözüm Gezgini, `ManagedDatabaseConstructs` proje adına sağ tıklayın ve yeni bir öğe eklemeyi seçin. Bu işlem, projeye eklenebilen yönetilen veritabanı nesnelerinin türlerini listeleyen yeni öğe Ekle iletişim kutusunu görüntüler. Şekil 8 ' de gösterildiği gibi, bunlar arasında saklı yordamlar ve Kullanıcı tanımlı Işlevler de dahildir.

Yalnızca, artık durdurulmuş olan tüm ürünleri döndüren bir saklı yordam ekleyerek başlayalım. Yeni saklı yordam dosyasını `GetDiscontinuedProducts.cs`olarak adlandırın.

[GetDiscontinuedProducts.cs adlı yeni bir saklı yordam eklemek ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**Şekil 8**: `GetDiscontinuedProducts.cs` adlı yeni bir saklı yordam ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))

Bu, aşağıdaki içeriğe sahip C# yeni bir sınıf dosyası oluşturur:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

Saklı yordamın `StoredProcedures`adlı bir `partial` sınıf dosyası içinde `static` yöntemi olarak uygulandığını unutmayın. Ayrıca, `GetDiscontinuedProducts` yöntemi, yöntemi saklı yordam olarak işaretleyen `SqlProcedure attribute`ile donatılmış.

Aşağıdaki kod, bir `SqlCommand` nesnesi oluşturur ve `CommandText` `Discontinued` alanı 1 ' e eşit olan ürünler için `Products` tablosundan sütunları döndüren bir `SELECT` sorgusuna ayarlar. Daha sonra komutu yürütür ve sonuçları istemci uygulamasına geri gönderir. `GetDiscontinuedProducts` yöntemine bu kodu ekleyin.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

Tüm yönetilen veritabanı nesnelerinin, çağıranın bağlamını temsil eden bir [`SqlContext` nesnesine](https://msdn.microsoft.com/library/ms131108.aspx) erişimi vardır. `SqlContext`, [`Pipe` özelliği](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)aracılığıyla bir [`SqlPipe` nesnesine](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) erişim sağlar. Bu `SqlPipe` nesnesi, SQL Server veritabanı ile çağıran uygulama arasında bilgi almak için kullanılır. Adından da anlaşılacağı gibi [`ExecuteAndSend` yöntemi](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) bir geçirilmiş `SqlCommand` nesnesi yürütür ve sonuçları istemci uygulamasına geri gönderir.

> [!NOTE]
> Yönetilen veritabanı nesneleri, küme tabanlı mantık yerine yordamsal mantığı kullanan saklı yordamlar ve UDF 'ler için idealdir. Yordamsal mantık, satır satır temelinde veri kümeleriyle çalışmayı veya skaler verilerle çalışmayı içerir. Ancak yeni oluşturduğumuz `GetDiscontinuedProducts` yöntemi, yordamsal bir mantık içermez. Bu nedenle, ideal olarak T-SQL saklı yordamı olarak uygulanmalıdır. Yönetilen saklı yordamlar oluşturmak ve dağıtmak için gereken adımları göstermek üzere yönetilen bir saklı yordam olarak uygulanır.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>4\. Adım: yönetilen saklı yordamı dağıtma

Bu kod tamamlandıktan sonra Northwind veritabanına dağıtmaya hazırız. SQL Server bir projeyi dağıtmak, kodu bir derlemeye derler, derlemeyi veritabanına kaydeder ve veritabanında ilgili nesneleri oluşturur ve bu nesneleri derlemede uygun yöntemlere ilişkilendirir. Dağıtım seçeneği tarafından gerçekleştirilen görevlerin tam bir kümesi 13. adımda daha hassas bir şekilde yazılmaktır. Çözüm Gezgini `ManagedDatabaseConstructs` proje adına sağ tıklayın ve Dağıt seçeneğini belirleyin. Ancak, dağıtım şu hata ile başarısız olur: ' EXTERNAL ' yakınında yanlış sözdizimi. Bu özelliği etkinleştirmek için geçerli veritabanının uyumluluk düzeyini daha yüksek bir değere ayarlamanız gerekebilir. Saklı yordam `sp_dbcmptlevel`için yardıma bakın.

Derlemeyi Northwind veritabanıyla kaydetmeye çalışırken bu hata iletisi oluşur. Bir derlemeyi SQL Server 2005 veritabanı ile kaydetmek için veritabanının uyumluluk düzeyi 90 olarak ayarlanmalıdır. Varsayılan olarak, yeni SQL Server 2005 veritabanlarının uyumluluk düzeyi 90 ' dir. Ancak, Microsoft SQL Server 2000 kullanılarak oluşturulan veritabanlarının varsayılan uyumluluk düzeyi 80 ' dir. Northwind veritabanı başlangıçta Microsoft SQL Server 2000 veritabanı olduğundan, uyumluluk düzeyi Şu anda 80 olarak ayarlanmıştır ve bu nedenle yönetilen veritabanı nesnelerini kaydettirmek için 90.

Veritabanı s uyumluluk düzeyini güncelleştirmek için Management Studio yeni bir sorgu penceresi açın ve şunu girin:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

Yukarıdaki sorguyu çalıştırmak için araç çubuğundaki yürütme simgesine tıklayın.

[Northwind veritabanı uyumluluk düzeyini ![güncelleştirme](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**Şekil 9**: Northwind veritabanı uyumluluk düzeyini güncelleştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))

Uyumluluk düzeyini güncelleştirdikten sonra SQL Server projeyi yeniden dağıtın. Bu sefer dağıtım hatasız tamamlanmalıdır.

SQL Server Management Studio dönün, Nesne Gezgini Northwind veritabanına sağ tıklayın ve Yenile ' yi seçin. Daha sonra, programlama klasörü detayına gidin ve ardından derlemeler klasörünü genişletin. Şekil 10 ' da gösterildiği gibi, Northwind veritabanı artık `ManagedDatabaseConstructs` projesi tarafından oluşturulan derlemeyi içerir.

![ManagedDatabaseConstructs derlemesi artık Northwind veritabanına kayıtlı](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**Şekil 10**: `ManagedDatabaseConstructs` derlemesi artık Northwind veritabanına kayıtlı

Ayrıca, saklı yordamlar klasörünü genişletin. `GetDiscontinuedProducts`adlı bir saklı yordam görürsünüz. Bu saklı yordam, dağıtım işlemi tarafından oluşturulmuştur ve `ManagedDatabaseConstructs` derlemesindeki `GetDiscontinuedProducts` yöntemine işaret eder. `GetDiscontinuedProducts` saklı yordamı yürütüldüğünde, bu, sırasıyla `GetDiscontinuedProducts` yöntemini yürütür. Bu yönetilen bir saklı yordam olduğundan, Management Studio ile düzenlenemez (Bu nedenle, saklı yordam adının yanındaki kilit simgesi).

![GetDiscontinuedProducts saklı yordamı saklı yordamlar klasöründe listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**Şekil 11**: `GetDiscontinuedProducts` saklı yordam saklı yordamlar klasöründe listelenir

Yönetilen saklı yordamı çağırabilmemiz için aşmamız gereken bir daha aceye sahip olmaya devam ediyoruz: veritabanı yönetilen kodun yürütülmesini engelleyecek şekilde yapılandırılmıştır. Yeni bir sorgu penceresi açıp `GetDiscontinuedProducts` saklı yordamını yürüterek bunu doğrulayın. Şu hata iletisini alırsınız: .NET Framework Kullanıcı kodu yürütme devre dışı bırakıldı. Clr etkin yapılandırma seçeneğini etkinleştirin.

Northwind veritabanı yapılandırma bilgilerini incelemek için, komut `exec sp_configure` sorgu penceresinde girin ve yürütün. Bu, clr etkin ayarının Şu anda 0 olarak ayarlandığını gösterir.

[![clr etkin ayarı şu anda 0 olarak ayarlanmış](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**Şekil 12**: clr etkin ayarı şu anda 0 olarak ayarlanmıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))

Şekil 12 ' deki her yapılandırma ayarının, ile listelenmiş dört değeri olduğunu unutmayın: en düşük ve en yüksek değerler ve yapılandırma ve çalıştırma değerleri. Clr etkin ayarının yapılandırma değerini güncelleştirmek için aşağıdaki komutu yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

`exec sp_configure` yeniden çalıştırırsanız yukarıdaki bildirimin clr özellikli ayar s yapılandırma değerini 1 olarak güncelleştirdiklerini, ancak çalıştırma değerinin hala 0 olarak ayarlandığını görürsünüz. Bu yapılandırma değişikliğinin etkili olması için, Run değerini geçerli yapılandırma değerine ayarlayacağız [`RECONFIGURE` komutunu](https://msdn.microsoft.com/library/ms176069.aspx)yürütmemiz gerekir. Sorgu penceresinde `RECONFIGURE` girin ve araç çubuğundaki yürütme simgesine tıklayın. Şimdi `exec sp_configure` çalıştırırsanız, clr etkinleştirilmiş ayar s yapılandırması ve çalıştırma değerleri için 1 değerini görmeniz gerekir.

Clr etkinleştirilmiş yapılandırma tamamlandıktan sonra yönetilen `GetDiscontinuedProducts` saklı yordamını çalıştırmaya hazırız. Sorgu penceresinde `exec` `GetDiscontinuedProducts`komutunu girin ve yürütün. Saklı yordamı çağırmak `GetDiscontinuedProducts` yönteminde karşılık gelen yönetilen kodun yürütülmesine neden olur. Bu kod, kullanımdan kaldırılmıştır ve bu verileri bu örnekteki SQL Server Management Studio çağıran uygulamaya döndüren `SELECT` bir sorgu yayınlar. Management Studio bu sonuçları alır ve sonuçlar penceresinde görüntüler.

[GetDiscontinuedProducts saklı yordamını ![, tüm durdurulmuş ürünleri döndürür](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**Şekil 13**: `GetDiscontinuedProducts` saklı yordam, tüm durdurulmuş ürünleri döndürür ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>5\. Adım: giriş parametrelerini kabul eden yönetilen saklı yordamlar oluşturma

Bu öğreticiler genelinde oluşturduğumuz sorguların ve saklı yordamların birçoğu, kullanılan *parametreleri*içerir. Örneğin, [yazılan veri kümesi Için yeni saklı yordamlar oluşturma TableAdapters](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) öğreticisinde, `@CategoryID`adlı bir giriş parametresini kabul eden `GetProductsByCategoryID` adlı bir saklı yordam oluşturduk. Daha sonra saklı yordam, `CategoryID` alanı sağlanan `@CategoryID` parametresinin değeri ile eşleşen tüm ürünleri geri döndürür.

Giriş parametrelerini kabul eden bir yönetilen saklı yordam oluşturmak için, bu parametreleri yöntem s tanımında belirtmeniz yeterlidir. Bunu göstermek için, s `GetProductsWithPriceLessThan`adlı `ManagedDatabaseConstructs` projesine başka bir yönetilen saklı yordam ekleyelim. Bu yönetilen saklı yordam, bir fiyat belirten giriş parametresini kabul eder ve `UnitPrice` alanı parametre değerinden küçük olan tüm ürünleri döndürür.

Projeye yeni bir saklı yordam eklemek için `ManagedDatabaseConstructs` proje adına sağ tıklayın ve yeni bir saklı yordam eklemeyi seçin. Dosyayı `GetProductsWithPriceLessThan.cs` olarak adlandırın. Adım 3 ' te gördüğünüz gibi, bu, `partial` sınıfı `StoredProcedures`C# yerleştirilmiş `GetProductsWithPriceLessThan` adlı bir yöntemle yeni bir sınıf dosyası oluşturur.

`GetProductsWithPriceLessThan` yöntemi tanımını `price` adlı bir [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) giriş parametresi kabul edecek şekilde güncelleştirin ve yürütmek için kodu yazın ve sorgu sonuçlarını döndürün:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

`GetProductsWithPriceLessThan` yöntemi tanımı ve kodu, adım 3 ' te oluşturulan `GetDiscontinuedProducts` yönteminin tanımına ve koduna benzer. Tek farklar `GetProductsWithPriceLessThan` yönteminin giriş parametresi olarak kabul ettesidir (`price`), `SqlCommand` s sorgusu bir parametre (`@MaxPrice`) içerir ve `SqlCommand` s `Parameters` koleksiyonuna bir parametre eklenir ve `price` değişkeninin değeri atanır.

Bu kodu ekledikten sonra SQL Server projesini yeniden dağıtın. Sonra, SQL Server Management Studio ' a dönüp saklı yordamlar klasörünü yenileyin. `GetProductsWithPriceLessThan`yeni bir giriş görmeniz gerekir. Bir sorgu penceresinde, Şekil 14 ' ün gösterdiği gibi, $25 ' den küçük tüm ürünleri listelendirilecektir ve `exec GetProductsWithPriceLessThan 25`komutu yürütün.

[$25 altındaki ![ürünleri görüntülenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**Şekil 14**: $25 altındaki ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>6\. Adım: yönetilen saklı yordamı veri erişim katmanından çağırma

Bu noktada, `GetDiscontinuedProducts` ve `GetProductsWithPriceLessThan` yönetilen saklı yordamları `ManagedDatabaseConstructs` projesine ekledik ve bunları Northwind SQL Server veritabanına kaydettiniz. Ayrıca, bu yönetilen saklı yordamları SQL Server Management Studio 'tan de çağırdık (bkz. Şekil s 13 ve 14). Ancak, ASP.NET uygulamamız tarafından yönetilen bu saklı yordamları kullanabilmesi için, bunları mimarideki veri erişimi ve Iş mantığı katmanlarına eklememiz gerekir. Bu adımda, türü belirtilmiş DataSet [s TableAdapters öğreticisi için başlangıçta yeni saklı yordamlar oluşturma](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) bölümünde oluşturulan `NorthwindWithSprocs` türü belirtilmiş veri kümesindeki `ProductsTableAdapter` iki yeni yöntem ekleyeceğiz. Adım 7 ' de, BLL 'ye karşılık gelen yöntemleri ekleyeceğiz.

Visual Studio 'da türü belirlenmiş `NorthwindWithSprocs` veri kümesini açın ve `GetDiscontinuedProducts`adlı `ProductsTableAdapter` yeni bir yöntem ekleyerek başlayın. TableAdapter 'a yeni bir yöntem eklemek için, tasarımcıda TableAdapter s adına sağ tıklayın ve bağlam menüsünden sorgu Ekle seçeneğini belirleyin.

> [!NOTE]
> Northwind veritabanını `App_Data` klasöründen SQL Server 2005 Express Sürüm veritabanı örneğine taşıdığımızdan, Web. config dosyasındaki karşılık gelen bağlantı dizesinin bu değişikliği yansıtacak şekilde güncellenmesi zorunludur. 2\. adımda `Web.config``NORTHWNDConnectionString` değerini güncelleştirme yaptık. Bu güncelleştirmeyi yapmayı unuttuysanız, sorgu ekleme başarısız oldu iletisini görürsünüz. TableAdapter 'a yeni bir yöntem eklenmeye çalışılırken bir iletişim kutusunda nesne `Web.config` için bağlantı `NORTHWNDConnectionString` bulunamıyor. Bu hatayı çözmek için, Tamam ' a tıklayın ve ardından `Web.config` ' a gidin ve `NORTHWNDConnectionString` değerini 2. adım ' da anlatıldığı şekilde güncelleştirin. Ardından, yöntemi TableAdapter 'a yeniden eklemeyi deneyin. Bu süre hatasız çalışmalıdır.

Yeni bir yöntem eklendiğinde, eski öğreticilerde birçok kez kullandığımız TableAdapter sorgu Yapılandırma Sihirbazı başlatılır. İlk adım, TableAdapter 'ın veritabanına nasıl erişmesi gerektiğini belirtmesini ister: geçici bir SQL ifadesiyle veya yeni veya mevcut bir saklı yordam aracılığıyla. Veritabanı ile `GetDiscontinuedProducts` yönetilen saklı yordamı zaten oluşturup kaydettirdiğimiz için, mevcut saklı yordamı kullan seçeneğini belirleyin ve sonraki düğmesine basın.

[![varolan saklı yordamı kullan seçeneğini belirleyin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**Şekil 15**: mevcut saklı yordamı kullan seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))

Sonraki ekranda, yöntemin çağıracağı saklı yordam için bizi uyarır. Açılan listeden `GetDiscontinuedProducts` yönetilen saklı yordamı seçin ve Ileri ' ye tıklayın.

[![GetDiscontinuedProducts yönetilen saklı yordamını seçin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**Şekil 16**: `GetDiscontinuedProducts` yönetilen saklı yordamı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))

Daha sonra, saklı yordamın satırları, tek bir değeri veya herhangi bir şey döndürüp döndürmeyeceğini belirtmemiz istenir. `GetDiscontinuedProducts`, Discontinued ürün satırları kümesini döndürdüğünden, ilk seçeneği (tablosal veri) seçin ve Ileri ' ye tıklayın.

[Tablo verileri seçeneğini ![seçin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**Şekil 17**: tablo verisi seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))

Son sihirbaz ekranı, kullanılan veri erişim desenlerini ve elde edilen yöntemlerin adlarını belirtmemizi sağlar. Her iki onay kutusu işaretli bırakın ve yöntemleri `FillByDiscontinued` ve `GetDiscontinuedProducts`olarak adlandırın. Sihirbazı tamamladığınızda son ' a tıklayın.

[![, FillByDiscontinued ve GetDiscontinuedProducts metotlarını adlandırın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**Şekil 18**: yöntemleri `FillByDiscontinued` ve `GetDiscontinuedProducts` adlandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))

`GetProductsWithPriceLessThan` yönetilen saklı yordamın `ProductsTableAdapter` `FillByPriceLessThan` ve `GetProductsWithPriceLessThan` adlı yöntemleri oluşturmak için bu adımları tekrarlayın.

Şekil 19, `GetDiscontinuedProducts` ve `GetProductsWithPriceLessThan` yönetilen saklı yordamlar için `ProductsTableAdapter` Yöntemler eklendikten sonra veri kümesi tasarımcısının ekran görüntüsünü gösterir.

[![ProductsTableAdapter, bu adımda eklenen yeni yöntemleri Içerir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**Şekil 19**: `ProductsTableAdapter`, bu adımda eklenen yeni yöntemleri içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png))

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>7\. Adım: Ilgili yöntemleri Iş mantığı katmanına ekleme

Artık, 4 ve 5. adımlarda eklenen yönetilen saklı yordamları çağırmaya yönelik yöntemler eklemek için veri erişim katmanını güncelleştirdik. Iş mantığı katmanına ilgili yöntemleri eklememiz gerekiyor. Aşağıdaki iki yöntemi `ProductsBLLWithSprocs` sınıfına ekleyin:

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

Her iki yöntem de karşılık gelen DAL metodunu çağırıp `ProductsDataTable` örneğini döndürür. Her yöntemin üzerindeki `DataObjectMethodAttribute` biçimlendirmesi, bu yöntemlerin, veri kaynağı Yapılandırma Sihirbazı 'nın Seç sekmesindeki açılan listede yer almasına neden olur.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>8\. Adım: yönetilen saklı yordamları sunum katmanından çağırma

Iş mantığı ve veri erişimi katmanları, `GetDiscontinuedProducts` ve `GetProductsWithPriceLessThan` yönetilen saklı yordamları çağırma desteğini kapsayacak şekilde genişletiyorsa, artık bu saklı yordam sonuçlarını bir ASP.NET sayfası aracılığıyla görüntüleyebilir.

`AdvancedDAL` klasöründeki `ManagedFunctionsAndSprocs.aspx` sayfasını açın ve araç kutusundan bir GridView 'u tasarımcıya sürükleyin. GridView s `ID` özelliğini `DiscontinuedProducts` ve akıllı etiketinden `DiscontinuedProductsDataSource`adlı yeni bir ObjectDataSource 'a bağlayın. `ProductsBLLWithSprocs` sınıf s `GetDiscontinuedProducts` yönteminden verileri çekmek için ObjectDataSource 'ı yapılandırın.

[![, bu ObjectDataSource 'ı ProductsBLLWithSprocs sınıfını kullanacak şekilde yapılandırma](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**Şekil 20**: `ProductsBLLWithSprocs` sınıfını kullanmak için ObjectDataSource 'ı yapılandırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))

[![Seç sekmesindeki açılan listeden GetDiscontinuedProducts metodunu seçin](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**Şekil 21**: Seç sekmesindeki aşağı açılan listeden `GetDiscontinuedProducts` yöntemini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))

Bu kılavuz yalnızca ürün bilgilerini göstermek için kullanılacak olduğundan, GÜNCELLEŞTIRME, ekleme ve SILME sekmelerini (yok) ve ardından son ' a tıklayarak açılan listeleri ayarlayın.

Sihirbaz tamamlandıktan sonra Visual Studio, `ProductsDataTable`her veri alanı için otomatik olarak bir BoundField veya CheckBoxField ekler. `ProductName` ve `Discontinued`dışındaki tüm bu alanları kaldırmak için bir dakikanızı ayırın ve bu noktada, GridView ve ObjectDataSource 'un bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı ayırın. Sayfa ziyaret edildiğinde, ObjectDataSource `ProductsBLLWithSprocs` sınıf s `GetDiscontinuedProducts` yöntemini çağırır. Adım 7 ' de gördüğünüz gibi, bu yöntem `GetDiscontinuedProducts` saklı yordamını çağıran DAL s `ProductsDataTable` sınıf s `GetDiscontinuedProducts` yöntemine çağrı yapılır. Bu saklı yordam yönetilen bir saklı yordamdır ve 3. adımda oluşturduğumuz kodu yürüterek, Discontinued ürünlerini döndürür.

Yönetilen saklı yordam tarafından döndürülen sonuçlar, DAL tarafından bir `ProductsDataTable` paketlenir ve sonra BLL 'ye döndürülür. Bu, daha sonra bunları GridView 'a bağlandıkları ve görüntülenen sunum katmanına geri döndürür. Beklenen şekilde, kılavuz bu ürünleri kaldırılmıştır.

[Üretimi durdurulmuş ürünlerin listesi ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**Şekil 22**: Discontinued ürünleri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))

Daha fazla uygulama için, sayfaya bir TextBox ve başka bir GridView ekleyin. Bu GridView 'un, `ProductsBLLWithSprocs` sınıf s `GetProductsWithPriceLessThan` yöntemini çağırarak metin kutusuna girilen miktardan daha az ürün görüntülemesini sağlayabilirsiniz.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>9\. Adım: T-SQL UDF 'Leri oluşturma ve çağırma

Kullanıcı tanımlı Işlevler veya UDF 'ler, veritabanı nesneleridir ve programlama dillerinde işlevlerin semantiğini yakından taklit eder. İçindeki C#bir işlev gibi, UDF 'ler değişken sayıda giriş parametresi içerebilir ve belirli bir türün değerini döndürebilir. UDF, skaler veri döndürebilir; bir dize, bir tamsayı, vb. ya da tablo verileri. Skaler bir veri türü döndüren bir UDF ile başlayan her iki tür UDF öğesine hızlıca göz atalım.

Aşağıdaki UDF belirli bir ürünün envanterinin tahmini değerini hesaplar. Bu, belirli bir ürün için `UnitPrice`, `UnitsInStock`ve `Discontinued` değerleri ve `money`türünde bir değer döndüren üç giriş parametresi alarak bunu yapar. `UnitPrice` `UnitsInStock`tarafından çarpılarak envanterin tahmini değerini hesaplar. Üretimi durdurulmuş öğeler için bu değer yarıya iner.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

Bu UDF veritabanına eklendikten sonra, Programlanabilirlik klasörünü genişleterek, Işlevler ve sonra skaler değer Işlevleri Management Studio aracılığıyla bulunabilir. Bu, şöyle bir `SELECT` sorgusunda kullanılabilir:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

`udf_ComputeInventoryValue` UDF 'yi Northwind veritabanına ekledim; Şekil 23 ' te Management Studio görüntülendiğinde yukarıdaki `SELECT` sorgusunun çıktısı gösterilmektedir. Ayrıca, UDF 'nin Nesne Gezgini skaler değer Işlevleri klasörünün altında listelendiğini unutmayın.

[![her ürün stok değeri listelenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**Şekil 23**: her ürün stok değeri listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))

UDF 'ler tablo verilerini de döndürebilir. Örneğin, belirli bir kategoriye ait ürünleri döndüren bir UDF oluşturuyoruz:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF bir `@CategoryID` giriş parametresini kabul eder ve belirtilen `SELECT` sorgusunun sonuçlarını döndürür. Oluşturulduktan sonra, bu UDF bir `SELECT` sorgusunun `FROM` (veya `JOIN`) yan tümcesinde başvurulabilir. Aşağıdaki örnek, her bir içecek için `ProductID`, `ProductName`ve `CategoryID` değerlerini döndürür.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

`udf_GetProductsByCategoryID` UDF 'yi Northwind veritabanına ekledim; Şekil 24 ' te Management Studio görüntülendiğinde yukarıdaki `SELECT` sorgusunun çıktısı gösterilmektedir. Tablo verileri döndüren UDF 'ler Nesne Gezgini s tablo-değer Işlevleri klasöründe bulunabilir.

[ProductID, ProductName ve CategoryID ![her bir Içecek için listelenir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**Şekil 24**: `ProductID`, `ProductName`ve `CategoryID` her bir beiçecek için listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png))

> [!NOTE]
> UDF 'ler oluşturma ve kullanma hakkında daha fazla bilgi için, [Kullanıcı tanımlı IŞLEVLERE giriş](http://www.sqlteam.com/item.asp?ItemID=1955)konusuna bakın. Ayrıca, [Kullanıcı tanımlı Işlevlerin olumlu ve dezavantajlarına](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)göz atın.

## <a name="step-10-creating-a-managed-udf"></a>10. Adım: yönetilen UDF oluşturma

Yukarıdaki örneklerde oluşturulan `udf_ComputeInventoryValue` ve `udf_GetProductsByCategoryID` UDF 'ler T-SQL veritabanı nesneleridir. SQL Server 2005 Ayrıca, adım 3 ve 5 ' ten yönetilen saklı yordamlar gibi `ManagedDatabaseConstructs` projesine eklenebilen yönetilen UDF 'Leri destekler. Bu adım için, yönetilen kodda `udf_ComputeInventoryValue` UDF 'yi uygulayalim.

`ManagedDatabaseConstructs` projesine yönetilen bir UDF eklemek için, Çözüm Gezgini içindeki proje adına sağ tıklayın ve yeni bir öğe eklemeyi seçin. Yeni öğe Ekle iletişim kutusundan Kullanıcı tanımlı şablon ' u seçin ve yeni UDF dosyasını `udf_ComputeInventoryValue_Managed.cs`adlandırın.

[ManagedDatabaseConstructs projesine yeni bir yönetilen UDF eklemek ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**Şekil 25**: `ManagedDatabaseConstructs` projesine yeni BIR yönetilen UDF ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))

Kullanıcı tanımlı Işlev şablonu, adı sınıf dosya adı (`udf_ComputeInventoryValue_Managed`, bu örnekte) ile aynı olan bir yöntemle `UserDefinedFunctions` adlı bir `partial` sınıfı oluşturur. Bu yöntem, yöntemi yönetilen bir UDF olarak belirleyen [`SqlFunction` özniteliği](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)kullanılarak tasarlanmalıdır.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

`udf_ComputeInventoryValue` yöntemi şu anda bir [`SqlString` nesnesi](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) döndürüyor ve herhangi bir giriş parametresi kabul etmiyor. Yöntem tanımını, `UnitPrice`, `UnitsInStock`ve `Discontinued` olmak üzere üç giriş parametresi kabul edecek şekilde güncelleştirmemiz gerekiyor ve bir `SqlMoney` nesnesi döndürüyor. Envanter değerini hesaplama mantığı T-SQL `udf_ComputeInventoryValue` UDF ' deki ile aynıdır.

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

UDF yöntemi giriş parametrelerinin karşılık gelen SQL türlerinde olduğunu unutmayın: `UnitPrice` alanı için `SqlMoney`, `UnitsInStock`için [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) [ve`SqlBoolean``Discontinued`.](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) Bu veri türleri `Products` tabloda tanımlanan türleri yansıtır: `UnitPrice` sütununun türü `money`, `smallint`türü `UnitsInStock` sütunu ve `Discontinued` türündeki `bit`sütunu.

Kod, 0 değeri atanmış `inventoryValue` adlı bir `SqlMoney` örneği oluşturarak başlar. `Products` tablosu `UnitsInPrice` ve `UnitsInStock` sütunlarında veritabanı `NULL` değerleri sağlar. Bu nedenle, ilk olarak bu değerlerin `SqlMoney` nesne s [`IsNull` özelliği](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)aracılığıyla yaptığımız `NULL` s içerdiğinden emin olmanız gerekir. Hem `UnitPrice` hem de `UnitsInStock``NULL` olmayan değerler içeriyorsa, `inventoryValue` ürünün çarpımı olarak hesapladık. Daha sonra, `Discontinued` true ise değeri halliyoruz.

> [!NOTE]
> `SqlMoney` nesnesi yalnızca iki `SqlMoney` örneğinin birlikte çarpılmasına izin verir. `SqlMoney` örneğinin sabit bir kayan noktalı sayı ile çarpılmasına izin vermez. Bu nedenle, `inventoryValue` bırakmak için 0,5 değerine sahip yeni bir `SqlMoney` örneği ile çarpıyoruz.

## <a name="step-11-deploying-the-managed-udf"></a>11. Adım: yönetilen UDF dağıtma

Artık yönetilen UDF oluşturuldığına göre, bunu Northwind veritabanına dağıtmaya hazır hale gelmiştir. 4\. adımda gördüğünüz gibi, bir SQL Server projesindeki yönetilen nesneler, Çözüm Gezgini proje adına sağ tıklayıp bağlam menüsünden dağıt seçeneği belirlenerek dağıtılır.

Projeyi dağıttıktan sonra, SQL Server Management Studio döndürün ve skaler değerli Işlevler klasörünü yenileyin. Şimdi iki giriş görmeniz gerekir:

- `dbo.udf_ComputeInventoryValue`-9. adımda oluşturulan T-SQL UDF ve
- `dbo.udf ComputeInventoryValue_Managed`-henüz dağıtılan 10. adımda oluşturulan yönetilen UDF.

Bu yönetilen UDF 'yi test etmek için Management Studio içinden aşağıdaki sorguyu yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

Bu komut T-SQL `udf_ComputeInventoryValue` UDF yerine yönetilen `udf ComputeInventoryValue_Managed` UDF kullanır, ancak çıktı aynıdır. UDF s çıkışının ekran görüntüsünü görmek için Şekil 23 ' e geri bakın.

## <a name="step-12-debugging-the-managed-database-objects"></a>12. Adım: yönetilen veritabanı nesnelerinde hata ayıklama

[Saklı yordamlar hata ayıklaması](debugging-stored-procedures-cs.md) öğreticisinde, Visual Studio aracılığıyla SQL Server hata ayıklama için üç seçenekten bahsettik: doğrudan veritabanı hata ayıklaması, uygulama hata ayıklaması ve bir SQL Server projesinden hata ayıklama. Yönetilen veritabanı nesnelerine doğrudan veritabanı hata ayıklaması aracılığıyla hata ayıklanamaz, ancak bir istemci uygulamasından ve doğrudan SQL Server projesinden hata ayıklanabilir. Ancak, hata ayıklamanın çalışması için SQL Server 2005 veritabanı SQL/CLR hata ayıklamasına izin vermelidir. `ManagedDatabaseConstructs` projeyi ilk oluşturduğumuz, SQL/CLR hata ayıklamayı etkinleştirmek isteyip istediğimiz hakkında bilgi almak isteyip istemediğinizi hatırlayın (adım 2 ' de Şekil 6 ' ya bakın). Bu ayar, Sunucu Gezgini penceresinden veritabanına sağ tıklanarak değiştirilebilir.

![Veritabanının SQL/CLR hata ayıklamasına Izin verdiğinden emin olun](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**Şekil 26**: veritabanının SQL/CLR hata ayıklamasına izin verdiğinden emin olun

`GetProductsWithPriceLessThan` yönetilen saklı yordamda hata ayıklamak istediğinizi düşünün. `GetProductsWithPriceLessThan` yönteminin kodu içinde bir kesme noktası ayarlayarak başlayacağız.

[GetProductsWithPriceLessThan yönteminde bir kesme noktası ayarlamak ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**Şekil 27**: `GetProductsWithPriceLessThan` yönteminde bir kesme noktası ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))

SQL Server projesinden yönetilen veritabanı nesnelerinde hata ayıklamaya ilk göz atalım. Çözümümüzde iki proje bulunduğundan, SQL Server projeden hata ayıklamak için Web sitemizden birlikte `ManagedDatabaseConstructs` SQL Server proje, hata ayıklamaya başladığınızda Visual Studio 'Yu `ManagedDatabaseConstructs` SQL Server projesini başlatmasını ister. Çözüm Gezgini `ManagedDatabaseConstructs` projesine sağ tıklayın ve bağlam menüsünden başlangıç projesi olarak ayarla seçeneğini belirleyin.

`ManagedDatabaseConstructs` projesi hata ayıklayıcıdan başlatıldığında, SQL deyimlerini `Test Scripts` klasöründe bulunan `Test.sql` dosyasında yürütür. Örneğin, `GetProductsWithPriceLessThan` yönetilen saklı yordamı test etmek için, mevcut `Test.sql` dosya içeriğini aşağıdaki ifadesiyle değiştirin ve bu, 14,95 `@CategoryID` değerini geçirerek `GetProductsWithPriceLessThan` yönetilen saklı yordamı çağırır:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

Yukarıdaki betiği `Test.sql`alanına girdikten sonra hata ayıklama menüsüne gidip hata ayıklamayı Başlat ' ı ya da araç çubuğundaki yeşil oynat simgesini seçerek hata ayıklamayı başlatın. Bu işlem, çözüm içinde projeleri oluşturur, yönetilen veritabanı nesnelerini Northwind veritabanına dağıtır ve ardından `Test.sql` betiğini yürütür. Bu noktada, kesme noktası isabet eder ve `GetProductsWithPriceLessThan` yönteminde ilerleyebileceğiniz, giriş parametrelerinin değerlerini inceleyebileceğiniz vb.

[GetProductsWithPriceLessThan yöntemi içindeki kesme noktası ![Isabet ediyor](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**Şekil 28**: `GetProductsWithPriceLessThan` yönteminde kesme noktası isabet edildi ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))

Bir SQL veritabanı nesnesinin hata ayıklaması için bir istemci uygulama aracılığıyla ayıklanmak üzere, veritabanının uygulama hata ayıklamasını destekleyecek şekilde yapılandırılması zorunludur. Sunucu Gezgini veritabanında veritabanına sağ tıklayın ve uygulama hata ayıklama seçeneğinin işaretli olduğundan emin olun. Ayrıca, ASP.NET uygulamasını SQL hata ayıklayıcıyla tümleştirilecek ve bağlantı havuzunu devre dışı bırakacak şekilde yapılandırmamız gerekir. Bu adımlar, [saklı yordamlar](debugging-stored-procedures-cs.md) öğreticisinin adım 2 ' de ayrıntılı olarak açıklanmaktadır.

ASP.NET uygulamasını ve veritabanını yapılandırdıktan sonra, ASP.NET Web sitesini başlangıç projesi olarak ayarlayın ve hata ayıklamayı başlatın. Kesme noktası olan yönetilen nesnelerden birini çağıran bir sayfayı ziyaret ederseniz, uygulama durabilir ve denetim hata ayıklayıcıya açılır; burada Şekil 28 ' de gösterildiği gibi kodda adım adım gezinebilirsiniz.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>13. Adım: yönetilen veritabanı nesnelerini El Ile derleme ve dağıtma

SQL Server projeler, yönetilen veritabanı nesneleri oluşturmayı, derlemeyi ve dağıtmayı kolaylaştırır. Ne yazık ki SQL Server projeler yalnızca Visual Studio 'nun Professional ve Team Systems sürümlerinde kullanılabilir. Visual Web Developer veya Visual Studio 'nun standart sürümünü kullanıyorsanız ve yönetilen veritabanı nesnelerini kullanmak istiyorsanız, bunları el ile oluşturmanız ve dağıtmanız gerekir. Bu dört adımdan oluşur:

1. Yönetilen veritabanı nesnesi için kaynak kodunu içeren bir dosya oluşturun,
2. Nesneyi bir derlemede derleyin,
3. Derlemeyi SQL Server 2005 veritabanı ile kaydedin ve
4. SQL Server, derlemede uygun yöntemi işaret eden bir veritabanı nesnesi oluşturun.

Bu görevleri göstermek için, `UnitPrice` belirtilen bir değerden daha büyük olan ürünleri döndüren yeni bir yönetilen saklı yordam oluşturalım. Bilgisayarınızda `GetProductsWithPriceGreaterThan.cs` adlı yeni bir dosya oluşturun ve dosyaya aşağıdaki kodu girin (bunu gerçekleştirmek için Visual Studio, Not defteri veya herhangi bir metin düzenleyicisini kullanabilirsiniz):

[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

Bu kod, 5. adımda oluşturulan `GetProductsWithPriceLessThan` yöntemiyle neredeyse aynıdır. Tek farklar Yöntem isimleri, `WHERE` yan tümcesi ve sorguda kullanılan parametre adıdır. `GetProductsWithPriceLessThan` yöntemine geri döndüğünüzde, `WHERE` yan tümcesinin oku: `WHERE UnitPrice < @MaxPrice`. Burada, `GetProductsWithPriceGreaterThan`: `WHERE UnitPrice > @MinPrice` kullanırız.

Şimdi bu sınıfı bir derlemede derlemeniz gerekir. Komut satırından, `GetProductsWithPriceGreaterThan.cs` dosyasını kaydettiğiniz dizine gidin ve sınıf dosyasını bir derlemede derlemek için C# derleyicisini (`csc.exe`) kullanın:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

`csc.exe` içeren klasör, sistem s `PATH`içinde değilse, `%WINDOWS%\Microsoft.NET\Framework\version\`şöyle bir yola tam olarak başvurmanız gerekir:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]

[Derlemeye derleme GetProductsWithPriceGreaterThan.cs ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**Şekil 29**: bir derlemeye `GetProductsWithPriceGreaterThan.cs` derleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))

`/t` bayrağı, C# sınıf dosyasının bir dll (yürütülebilir değil) olarak derlenmesi gerektiğini belirtir. `/out` bayrağı, elde edilen derlemenin adını belirtir.

> [!NOTE]
> Komut satırından `GetProductsWithPriceGreaterThan.cs` sınıf dosyasını derlemek yerine, alternatif olarak Visual Studio Standard Edition 'da [Visual C# Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) veya ayrı bir sınıf kitaplığı projesi oluşturabilirsiniz. S Ren Jacob Lauritsen, `GetProductsWithPriceGreaterThan` saklı yordamı ve adım 3 C# , 5 ve 10 ' da oluşturulan iki yönetilen saklı yordam ve UDF için kod Içeren bir Visual Express Edition projesi sağladı. Ayrıca, ilgili veritabanı nesnelerini eklemek için gereken T-SQL komutlarını içeren s Ren Project.

Bir derlemeye derlenen kodla, derlemeyi SQL Server 2005 veritabanı içine kaydetmeye hazırız. Bu, T-SQL aracılığıyla, komut `CREATE ASSEMBLY`veya SQL Server Management Studio kullanılarak gerçekleştirilebilir. Management Studio kullanmaya odaklanalım.

Management Studio, Northwind veritabanındaki programlama klasörünü genişletin. Alt klasörlerinden biri derlemelerdir. Veritabanına yeni bir derlemeyi el ile eklemek için derlemeler klasörüne sağ tıklayın ve bağlam menüsünden Yeni derleme ' yi seçin. Bu, yeni derleme iletişim kutusunu görüntüler (bkz. Şekil 30). Araştır düğmesine tıklayın, yeni derduğumuz `ManuallyCreatedDBObjects.dll` derlemeyi seçin ve ardından derlemeyi veritabanına eklemek için Tamam ' a tıklayın. Nesne Gezgini `ManuallyCreatedDBObjects.dll` derlemesini görmemelisiniz.

[ManuallyCreatedDBObjects. dll derlemesini veritabanına eklemek ![](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**Şekil 30**: veritabanına `ManuallyCreatedDBObjects.dll` derlemeyi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))

![ManuallyCreatedDBObjects. dll Nesne Gezgini listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**Şekil 31**: `ManuallyCreatedDBObjects.dll` Nesne Gezgini listelenmiştir

Derlemeyi Northwind veritabanına ekledik, ancak bir saklı yordamı derlemedeki `GetProductsWithPriceGreaterThan` yöntemiyle ilişkilendirdik. Bunu gerçekleştirmek için yeni bir sorgu penceresi açın ve aşağıdaki betiği yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

Bu, `GetProductsWithPriceGreaterThan` adlı Northwind veritabanında yeni bir saklı yordam oluşturur ve bunu yönetilen yöntem `GetProductsWithPriceGreaterThan` (derlemede bulunan `StoredProcedures`sınıf `ManuallyCreatedDBObjects`) ile ilişkilendirir.

Yukarıdaki betiği yürüttükten sonra, Nesne Gezgini saklı yordamlar klasörünü yenileyin. Bunun yanında bir kilit simgesi olan `GetProductsWithPriceGreaterThan` yeni bir saklı yordam girişi görmeniz gerekir. Bu saklı yordamı test etmek için sorgu penceresine aşağıdaki betiği girin ve yürütün:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

Şekil 32 gösterdiği gibi, yukarıdaki komut, `UnitPrice` $24,95 ' den büyük olan bu ürünlerin bilgilerini görüntüler.

[![ManuallyCreatedDBObjects. dll Nesne Gezgini listelenmiştir](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**Şekil 32**: `ManuallyCreatedDBObjects.dll` Nesne Gezgini listelenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))

## <a name="summary"></a>Özet

Microsoft SQL Server 2005, yönetilen kod kullanılarak veritabanı nesnelerinin oluşturulmasına izin veren ortak dil çalışma zamanı (CLR) ile tümleştirme sağlar. Daha önce bu veritabanı nesneleri yalnızca T-SQL kullanılarak oluşturulabilir, ancak artık bu nesneleri gibi C#.NET programlama dillerini kullanarak oluşturmuyoruz. Bu öğreticide, yönetilen iki saklı yordam ve yönetilen Kullanıcı tanımlı bir Işlev oluşturduk.

Visual Studio s SQL Server proje türü, yönetilen veritabanı nesneleri oluşturmayı, derlemeyi ve dağıtılmasını kolaylaştırır. Üstelik, zengin hata ayıklama desteği sunar. Ancak SQL Server proje türleri yalnızca Visual Studio 'nun Professional ve Team Systems sürümlerinde kullanılabilir. Visual Web Developer veya Visual Studio 'nun standart sürümünü kullanan kişiler için, 13. adımda gördüğünüz gibi oluşturma, derleme ve dağıtım adımlarının el ile gerçekleştirilmesi gerekir.

Programlamanın kutlu olsun!

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kullanıcı tanımlı Işlevlerin avantajları ve dezavantajları](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Yönetilen kodda SQL Server 2005 nesneleri oluşturma](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005 ' de yönetilen kod kullanarak Tetikleyiciler oluşturma](http://www.15seconds.com/issue/041006.htm)
- [Nasıl yapılır: CLR SQL Server saklı yordamı oluşturma ve çalıştırma](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Nasıl yapılır: bir CLR SQL Server Kullanıcı tanımlı Işlev oluşturma ve çalıştırma](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Nasıl yapılır: SQL nesnelerini çalıştırmak için `Test.sql` betiğini düzenleme](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Kullanıcı tanımlı IŞLEVLERE giriş](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Yönetilen kod ve SQL Server 2005 (video)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-SQL başvurusu](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [İzlenecek yol: yönetilen kodda saklı yordam oluşturma](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, S. Bu makaleyi gözden geçirmenin yanı sıra, Ayrıca, yönetilen veritabanı nesnelerini C# el ile derlemek için bu makalede yer alan Visual Express Edition projesi de oluşturulmuştur. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](debugging-stored-procedures-cs.md)
> [İleri](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
