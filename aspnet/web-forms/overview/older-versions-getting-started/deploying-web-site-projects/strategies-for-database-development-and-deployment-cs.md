---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
title: Veritabanı geliştirme ve dağıtım stratejileri (C#) | Microsoft Docs
author: rick-anderson
description: Veri temelli bir uygulamayı ilk kez dağıttığınızda geliştirme ortamındaki veritabanını üretim ortamına taşıyabilirsiniz. bu B...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 3e8b0627-3eb7-488e-807e-067cba7cec05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
msc.type: authoredcontent
ms.openlocfilehash: 4d9dbaf41926b43af171619ee34f58da84b5dab1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582164"
---
# <a name="strategies-for-database-development-and-deployment-c"></a>Veritabanı Geliştirme ve Dağıtma Stratejileri (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_cs.pdf)

> Veri temelli bir uygulamayı ilk kez dağıttığınızda geliştirme ortamındaki veritabanını üretim ortamına taşıyabilirsiniz. bu Ancak sonraki dağıtımlarda, daha sonra, üretim veritabanına girilen verilerin üzerine yazar. Bunun yerine, bir veritabanını dağıtmak, üretim veritabanına son dağıtımdan bu yana geliştirme veritabanına yapılan değişiklikleri uygulamayı içerir. Bu öğreticide bu zorluk incelenir ve son dağıtımdan sonra veritabanına yapılan değişiklikleri zaman zaman ve uygulama konusunda yardımcı olmak için çeşitli stratejiler sunulmaktadır.

## <a name="introduction"></a>Giriş

Önceki öğreticilerde anlatıldığı gibi, bir ASP.NET uygulaması dağıtmak, ilgili içeriğin geliştirme ortamından üretim ortamına kopyalanmasını gerektirir. Dağıtım tek seferlik bir olay değildir, ancak bunun yerine yazılımın yeni bir sürümü yayınlandığında veya hata ya da güvenlik kaygıları tanımlandığında ve ele edildiğinde meydana gelen bir şey olur. ASP.NET sayfalarını, görüntülerini, JavaScript dosyalarını ve diğer dosyaları üretim ortamına kopyalarken, bu dosyanın son dağıtımdan bu yana nasıl değiştirildiği konusunda kendinize sorun olması gerekmez. Var olan içeriğin üzerine yazarak dosyayı üretime taşıyabilirsiniz. Ne yazık ki bu kolaylık, veritabanını dağıtmaya genişlemez.

Veri temelli bir uygulamayı ilk kez dağıttığınızda geliştirme ortamındaki veritabanını üretim ortamına taşıyabilirsiniz. bu Ancak sonraki dağıtımlarda, daha sonra, üretim veritabanına girilen verilerin üzerine yazar. Bunun yerine, bir veritabanını dağıtmak, üretim veritabanına son dağıtımdan bu yana geliştirme veritabanına yapılan *değişiklikleri* uygulamayı içerir. Bu öğreticide bu zorluk incelenir ve son dağıtımdan sonra veritabanına yapılan değişiklikleri zaman zaman ve uygulama konusunda yardımcı olmak için çeşitli stratejiler sunulmaktadır.

## <a name="the-challenges-of-deploying-a-database"></a>Veritabanı dağıtma sorunları

Veri tabanlı bir uygulama ilk kez dağıtılmadan önce, bir veri tabanlı uygulamayı ilk kez dağıttığınıza bir veri odaklı uygulama dağıtırken, veritabanını bir veri temelli uygulama dağıtırken üretim ortamına geliştirme ortamı. Ancak uygulama dağıtıldıktan sonra, veritabanının iki kopyası vardır: bir geliştirme ve diğeri üretimde.

Dağıtımlar arasında geliştirme ve üretim veritabanları eşitlenmemiş olabilir. Üretim veritabanı şeması değişmeden kaldığı halde, yeni özellikler eklendikçe geliştirme veritabanı şeması değişebilir. Sütunları, tabloları, görünümleri veya saklı yordamları ekleyebilir veya kaldırabilirsiniz. Geliştirme veritabanına eklenen önemli veriler de olabilir. Birçok veri tabanlı uygulama, Kullanıcı tarafından düzenlenemeyen, uygulamaya özgü veriler ile doldurulmuş arama tabloları içerir. Örneğin, bir açık eksiltme Web sitesinde, yeni, Iyi ve dengeli gibi, auctionıed olan öğenin koşulunu tanımlayan seçimleri içeren bir açılır liste bulunabilir. Bu seçenekleri doğrudan açılan listede sabit kodlamak yerine, bunları bir veritabanı tablosuna yerleştirmek genellikle daha iyidir. Geliştirme sırasında, daha sonra tabloya daha fazla zayıf adlı yeni bir koşul eklendiğinde, bu kayıt, uygulamanın dağıtılmasında üretim veritabanındaki arama tablosuna eklenmesi gerekir.

İdeal olarak, veritabanını dağıtmak, veritabanının geliştirmeden üretime kopyalanmasını içerir. Ancak, uygulamayı dağıttıktan ve geliştirmeye devam ettikten sonra, üretim veritabanının gerçek kullanıcılardan gerçek verilerle doldurulduğuna dikkat edin. Bu nedenle, bir sonraki dağıtımda veritabanını geliştirmeden üretime kopyalamak için üretim veritabanının üzerine yazılır ve var olan verileri kaybedersiniz. Net sonucu, son dağıtımdan bu yana geliştirme veritabanına yapılan değişiklikleri uygulamak için veritabanı bobin 'leri dağıtmakta olur.

Bir veritabanını dağıtmak, şemadaki değişiklikleri ve büyük olasılıkla son dağıtımdan bu yana verileri uygulamayı içerdiğinden, bu değişikliklerin üretime uygulanabilmesi için bir değişiklik geçmişinin korunması (veya dağıtım zamanında belirlenmesi) gerekir. Veri modeli üzerinde yapılan değişiklikleri yönetmeye ve uygulamaya yönelik çeşitli teknikler vardır.

### <a name="defining-the-baseline"></a>Taban çizgisini tanımlama

Uygulama veritabanınızdaki değişiklikleri sürdürmek için, değişikliklerin uygulandığı bir taban çizgisi olan bir başlangıç durumuna sahip olmanız gerekir. En az bir başlangıç durumu, tablo, görünüm veya saklı yordam içermeyen boş bir veritabanı olabilir. Bu tür bir taban çizgisi, ilk dağıtımdan sonra yapılan değişikliklerle birlikte tüm veritabanı tabloları, görünümler ve saklı yordamların oluşturulmasını içermesi gerektiğinden büyük bir değişiklik günlüğü ile sonuçlanır. Spektrumun diğer ucunda, ana temeli ilk olarak üretim ortamına dağıtılan veritabanının sürümü olarak ayarlayabilirsiniz. Bu seçenek, yalnızca ilk dağıtımdan sonra veritabanına yapılan değişiklikleri içerdiğinden, daha küçük bir değişiklik günlüğüne neden olur. Bu yaklaşım, tercih ederim. Tabii ki, yol yaklaşımının daha fazla bir ortasını seçerek, taban çizgisini veritabanının ilk oluşturma ve veritabanının ilk dağıtıldığı zaman arasında bir nokta olarak tanımlayarak tanımlayabilirsiniz.

Temeli seçtikten sonra, temel sürümü yeniden oluşturmak için yürütülebilecek bir SQL betiği oluşturmayı düşünün. Bu tür bir betik, veritabanının temel sürümünü hızlı bir şekilde yeniden oluşturmayı mümkün kılar. Bu işlevsellik özellikle, proje üzerinde çalışan birden fazla geliştirici veya test ya da hazırlama gibi ek ortamlarda, her birinin kendi kendine kopyasının olması gereken daha büyük projelerde yararlıdır.

Temel sürüme ait bir SQL betiği oluşturmak için, elden çıkarmada çeşitli araçlar vardır. SQL Server Management Studio (SSMS) ' den veritabanına sağ tıklayıp görevler alt menüsüne gidebilir ve betikler oluştur seçeneğini belirleyebilirsiniz. Bu, veritabanı s nesnelerinizi oluşturmak için SQL komutlarını içeren bir dosya oluşturmayı söylemek istediğiniz betik Sihirbazı 'Nı başlatır. Başka bir seçenek de veritabanı şeması oluşturmak için SQL komutları oluşturabilen, ancak veritabanı tablolarındaki verileri de oluşturabilen veritabanı Yayımlama Sihirbazı ' dır. Veritabanı Yayımlama Sihirbazı, *veritabanı dağıtma* öğreticisinde ayrıntılı olarak incelendi. Kullandığınız aracı ne olursa olsun, sonunda veritabanınızın temel sürümünü yeniden oluşturmak için kullanabileceğiniz bir betik dosyanız olması gerekir.

## <a name="documenting-the-database-changes-in-prose"></a>Veritabanı değişikliklerinin Proşirde belgelenme

Geliştirme aşaması sırasında veri modelinde değişiklik günlüğünün korunmanın en kolay yolu, değişiklikleri proo 'da kaydetmek. Örneğin, zaten dağıtılmış bir uygulamanın geliştirilmesi sırasında `Employees` tablosuna yeni bir sütun eklersiniz, `Orders` tablosundan bir sütunu kaldırır ve yeni bir tablo (`ProductCategories`) ekleyebilirsiniz, bir metin dosyası veya Microsoft Word belgesi aşağıdaki geçmişle birlikte korunur:

<a id="0.4_table01"></a>

| **Değiştirme tarihi** | **Değişiklik ayrıntıları** |
| --- | --- |
| 2009-02-03: | `Employees` tabloya sütun `DepartmentID` (`int`DEĞIL) eklendi. `Departments.DepartmentID` `Employees.DepartmentID`bir yabancı anahtar kısıtlaması eklendi. |
| 2009-02-05: | `Orders` tablosundan sütun `TotalWeight` kaldırıldı. Veriler ilişkili `OrderDetails` kayıtlarında zaten yakalandı. |
| 2009-02-12: | `ProductCategories` tablosu oluşturuldu. Üç sütun vardır: `ProductCategoryID` (`int`, `IDENTITY`, `NOT NULL`), `CategoryName` (`nvarchar(50)`, `NOT NULL`) ve `Active` (`bit`, `NOT NULL`). `ProductCategoryID`için bir birincil anahtar kısıtlaması ve `Active`için varsayılan değer olan 1 ' i eklediniz. |

Bu yaklaşımın birçok sakıncaları vardır. Başlangıçlara yönelik bir umuyoruz yoktur. Bu değişikliklerin her zaman, uygulama dağıtıldığında olduğu gibi bir veritabanına uygulanması gerekir. bir geliştirici her değişikliği birer birer el ile uygulamalıdır. Ayrıca, değişiklik günlüğünü kullanarak veritabanının belirli bir sürümünü taban çizgisinden yeniden oluşturmanız gerekiyorsa, bunun yapılması, günlüğün boyutu büyüdükçe daha fazla zaman alır. Bu yöntemin diğer sakıncası, her bir değişiklik günlüğü girişinin açıklık ve ayrıntı düzeyinin, değişikliği kaydeden kişiye ayrılmasının bir dezavantajı olur. Birden çok geliştiriciyle bir ekipte, bazıları diğerlerine göre daha ayrıntılı, daha okunaklı veya daha hassas girişler oluşturabilir. Ayrıca, yazım hataları ve insan ile ilgili diğer veri girişi hataları da mümkündür.

Veritabanı değişikliklerinin proşirde belgelenme birincil avantajı basittür. Veritabanı nesneleri oluşturmak ve değiştirmek için SQL söz dizimine alışkın olmanız gerekmez. Bunun yerine, değişiklikleri proo 'da kaydedebilir ve SQL Server Management Studio s grafik kullanıcı arabiriminden uygulayabilirsiniz.

Değişiklik günlüğlerinizin proo 'da saklanması çok karmaşık değildir ve kapsamdaki büyük olanlar gibi belirli projelerle iyi çalışmaz, veri modelinde sık sık değişikliklere sahiptir veya birden çok geliştirici içerir. Ancak, bu yaklaşımı, veri modelinde yalnızca zaman zaman değişiklik yapan küçük ve tek Man projelerinde çok iyi bir şekilde çalıştığını ve solo geliştiricisinin, veritabanı nesneleri oluşturmak ve değiştirmek için SQL sözdiziminde güçlü bir arka plana sahip olduğunu gördük.

> [!NOTE]
> Değişiklik günlüğündeki bilgiler, teknik olarak yalnızca dağıtım zamanına kadar gerekliyse, değişiklik geçmişini tutmanız önerilir. Ancak, tek bir sürekli büyüyen değişiklik günlüğü dosyasını korumak yerine, her veritabanı sürümü için farklı bir değişiklik günlük dosyası kullanmayı düşünün. Genellikle veritabanını her dağıtıldığında bir kez kullanmak isteyeceksiniz. Değişiklik günlüklerinin günlüğünü tutarak, taban çizgisinden başlayarak, sürüm 1 ' den başlayan değişiklik günlüğü betikleri ' ni yürüterek ve yeniden oluşturmanız gereken sürüme ulaşana kadar devam ederek herhangi bir veritabanı sürümünü yeniden oluşturabilirsiniz.

## <a name="recording-the-sql-change-statements"></a>SQL değişiklik deyimlerini kaydetme

Değişiklik günlüğünü sağlamanın birincil dezavantajı, Otomasyon olmamasıdır. İdeal olarak, dağıtım sırasında üretim veritabanında veritabanı değişikliklerinin uygulanması, yönergelerin bir listesini el ile gerçekleştirmek yerine bir komut dosyasını yürütmek için bir düğmeye tıklanması kadar kolay olabilir. Bu tür otomasyon, veri modelini değiştirmek için kullanılan SQL komutlarını içeren bir değişiklik günlüğü korunarak mümkündür.

SQL söz dizimi çeşitli veritabanı nesneleri oluşturmak ve değiştirmek için bir dizi deyim içerir. Örneğin, yürütüldüğünde [*create table deyimleri*](https://msdn.microsoft.com/library/ms174979.aspx), belirtilen sütun ve kısıtlamalara sahip yeni bir tablo oluşturur. [*Alter table ifadesi*](https://msdn.microsoft.com/library/ms190273.aspx) var olan bir tabloyu değiştirir, sütunları veya kısıtlamalarını ekleme, kaldırma veya değiştirme. Dizinler, görünümler, Kullanıcı tanımlı işlevler, saklı yordamlar, Tetikleyiciler ve diğer veritabanı nesneleri oluşturmak, değiştirmek ve bırakmak için de deyimler vardır.

Önceki örneğimize dönerek, zaten dağıtılmış bir uygulamanın geliştirilmesi sırasında, `Employees` tabloya yeni bir sütun eklersiniz, `Orders` tablosundan bir sütunu kaldırmalı ve yeni bir tablo (`ProductCategories`) ekleyebilirsiniz. Bu tür eylemler aşağıdaki SQL komutlarıyla bir değişiklik günlüğü dosyası oluşmasına neden olur:

[!code-sql[Main](strategies-for-database-development-and-deployment-cs/samples/sample1.sql)]

Bu değişiklikleri dağıtım zamanında üretim veritabanına göndermek tek tıklamayla bir işlemdir: SQL Server Management Studio açın, üretim veritabanınıza bağlanın, yeni bir sorgu penceresi açın, değişiklik günlüğünün içeriğini yapıştırın ve betiği çalıştırmak için Yürüt ' e tıklayın.

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>Veri modellerini eşitlemeye yönelik bir karşılaştırma aracı kullanma

Veritabanı değişikliklerinin tek tek içinde belgelenmesi kolaydır, ancak değişikliklerin uygulanması bir geliştiricinin üretim veritabanında her seferinde bir değişiklik yapmasını gerektirir; değişiklik SQL komutlarının belgelenmesi, bir düğmeye tıklayarak bu değişiklikleri üretim veritabanında uygulamayı kolay ve hızlı bir şekilde uygulamaya sunar, ancak SQL deyimlerini ve veritabanı nesneleri oluşturma ve değiştirme sözdizimini öğrenmeye ve bu sözdiziminin yönetimine gerek duyar. Veritabanı karşılaştırma araçları her iki yaklaşımdan en iyi şekilde yararlanın ve en kötü olanı atar.

Bir veritabanı karşılaştırma aracı, iki veritabanının şemasını veya verilerini karşılaştırır ve veritabanlarının nasıl farklı olduğunu gösteren bir özet raporu görüntüler. Ardından, bir düğmeye tıklayarak bir veya daha fazla veritabanı nesnesini eşitlemek için SQL komutları oluşturabilirsiniz. Bir Nutshell 'de, dağıtım zamanında geliştirme ve üretim veritabanlarını karşılaştırmak için bir veritabanı karşılaştırma aracı kullanabilirsiniz. bu sayede, yürütüldüğünde, değişiklikleri üretim veritabanı s şemasına uygular, böylece geliştirme veritabanı şemasını yansıtır.

Birçok farklı satıcı tarafından sunulan çeşitli üçüncü taraf veritabanı karşılaştırma araçları vardır. Bu tür bir örnek, [*kırmızı kapı yazılımına*](http://www.red-gate.com/)göre [*SQL karşılaştırmaktır*](http://www.red-gate.com/products/SQL_Compare/). Geliştirme ve üretim veritabanları şemalarını karşılaştırmak ve eşleştirmek için SQL Compare kullanma sürecini inceleyelim.

> [!NOTE]
> Bu yazma sırasında, SQL Compare 'in geçerli sürümü 7,1, standart sürüm maliyetlendirme $395 ile oluşturulmuştur. 14 günlük ücretsiz deneme sürümünü indirerek da izleyebilirsiniz.

SQL Compare başladığında, kaydedilen SQL Compare projelerini gösteren karşılaştırma projeleri iletişim kutusu açılır. Yeni bir proje oluşturun. Bu, Karşılaştırılacak veritabanları hakkında bilgi isteyen proje yapılandırma sihirbazını başlatır (bkz. Şekil 1). Geliştirme ve üretim ortamı veritabanlarının bilgilerini girin.

[Geliştirme ve üretim veritabanlarını karşılaştırma ![](strategies-for-database-development-and-deployment-cs/_static/image2.jpg)](strategies-for-database-development-and-deployment-cs/_static/image1.jpg)

**Şekil 1**: geliştirme ve üretim veritabanlarını karşılaştırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](strategies-for-database-development-and-deployment-cs/_static/image3.jpg))

> [!NOTE]
> Geliştirme ortamı veritabanınız, Web sitenizin `App_Data` klasöründeki bir SQL Express sürümü veritabanı dosyası ise Şekil 1 ' de gösterilen iletişim kutusundan seçmek için veritabanını SQL Server Express veritabanı sunucusuna kaydetmeniz gerekir. Bunu yapmanın en kolay yolu SQL Server Management Studio (SSMS) öğesini açmak, SQL Server Express veritabanı sunucusuna bağlanmak ve veritabanını eklemektir. Bilgisayarınızda SSMS yüklü değilse, ücretsiz [*SQL Server 2008 Management Studio temel sürümü*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en)indirip yükleyebilirsiniz.

Karşılaştırılacak veritabanlarını seçmeye ek olarak, Seçenekler sekmesinden çeşitli karşılaştırma ayarları da belirtebilirsiniz. Açmak isteyebileceğiniz bir seçenek, "kısıtlama ve dizin adlarını yoksay" dır. Önceki öğreticide, uygulama Hizmetleri veritabanı nesnelerini geliştirme ve üretim veritabanlarına eklediğimiz konusunda geri çekin. Bu nesneleri üretim veritabanında oluşturmak için `aspnet_regsql.exe` aracını kullandıysanız, birincil anahtar ve benzersiz kısıtlama adlarının geliştirme ve üretim veritabanları arasında farklı olduğunu fark edersiniz. Sonuç olarak, SQL Compare tüm uygulama hizmetleri tablolarının farklı olduğunu işaret eder. "Kısıtlama ve dizin adlarını yoksay" işaretini işaretsiz bırakabilir ve kısıtlama adlarını eşitleyebilir ya da SQL Compare 'in bu farklılıkları yoksaymasını sağlayabilirsiniz.

Karşılaştırılacak veritabanlarını seçtikten sonra (Karşılaştırma seçeneklerini gözden geçirdikten), karşılaştırmaya başlamak için şimdi Karşılaştır düğmesine tıklayın. Sonraki birkaç saniye içinde, SQL Compare iki veritabanının şemalarını inceler ve bunların nasıl farklı olduğunu gösteren bir rapor oluşturur. Ben, bu tür tutarsızlıklardan SQL Compare arabiriminde nasıl Not alınacağını göstermek için geliştirme veritabanında bazı değişiklikler yaptı. Şekil 2 ' de gösterildiği gibi, `Authors` tabloya `BirthDate` bir sütun ekledim, `Books` tablosundan `ISBN` sütununu kaldırdım ve yeni bir tablo ekledi. Bu, `Ratings`siteyi ziyaret eden kullanıcıların gözden geçirmeli kitapları almasına olanak tanır.

> [!NOTE]
> Bu öğreticide yapılan veri modeli değişiklikleri, bir veritabanı karşılaştırma aracı kullanmayı göstermek için yapılmıştır. Bu değişiklikleri veritabanında sonraki öğreticilerde bulamacaksınız.

[![SQL Compare geliştirme ve üretim veritabanları arasındaki farkları listeler](strategies-for-database-development-and-deployment-cs/_static/image5.jpg)](strategies-for-database-development-and-deployment-cs/_static/image4.jpg)

**Şekil 2**: SQL Compare geliştirme ve üretim veritabanları arasındaki farkları listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](strategies-for-database-development-and-deployment-cs/_static/image6.jpg))

SQL Compare, veritabanı nesnelerini gruplar halinde ayırır, her iki veritabanında da hangi nesnelerin olduğunu, ancak farklı olduğunu, tek bir veritabanında hangi nesnelerin aynı olduğunu, hangilerinin aynı olduğunu gösterir. Görebileceğiniz gibi, her iki veritabanında da bulunan ancak farklı olan `Authors` tablo, bir sütun eklenmiş olan ve `Books` tablo olan ve bir kaldırılan. Yalnızca geliştirme veritabanında bulunan, yeni oluşturulan `Ratings` tablosu olan bir nesne vardır. Ve her iki veritabanında da özdeş olan 117 nesne vardır.

Bir veritabanı nesnesi seçilirse, bu nesnelerin nasıl farklı olduğunu gösteren SQL farkları penceresi görüntülenir. Şekil 2 ' de en altta görüntülenen SQL farkları penceresi, geliştirme veritabanındaki `Authors` tablosunun, üretim veritabanındaki `Authors` tablosunda bulunmayan `BirthDate` sütununa sahip olduğunu vurgular.

Farkları gözden geçirdikten ve hangi nesneleri eşitleyeceğiniz seçtikten sonra, bir sonraki adım, üretim veritabanı şemasını geliştirme veritabanıyla eşleşecek şekilde güncelleştirmek için gereken SQL komutlarını oluşturmak için kullanılır. Bu, eşitleme Sihirbazı aracılığıyla gerçekleştirilir. Eşitleme Sihirbazı eşitlenecek nesneleri onaylar ve eylem planını özetler (bkz. Şekil 3). Veritabanlarını hemen eşitleyebilir veya boş bir şekilde çalıştırılabilen SQL komutlarıyla bir komut dosyası oluşturabilirsiniz.

[![veritabanları şemalarınızı eşitlemek için eşitleme Sihirbazı 'nı kullanın](strategies-for-database-development-and-deployment-cs/_static/image8.jpg)](strategies-for-database-development-and-deployment-cs/_static/image7.jpg)

**Şekil 3**: veritabanları şemalarınızı eşitlemek Için eşitleme Sihirbazı 'nı kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](strategies-for-database-development-and-deployment-cs/_static/image9.jpg))

Red kapısı yazılım s SQL karşılaştırması gibi veritabanı karşılaştırma araçları, değişiklikleri geliştirme veritabanı şemasına, üretim veritabanına kolayca işaret eden bir şekilde uygulamayı ve öğesini tıklamasını sağlar.

> [!NOTE]
> SQL Compare iki veritabanı *şeması*karşılaştırır ve eşitler. Ne yazık ki, iki veritabanı tablosu içindeki verileri karşılaştırmaz ve eşitlemez. Red kapısı yazılımı, iki veritabanı arasında verileri karşılaştıran ve eşitleyen [*SQL Data Compare*](http://www.red-gate.com/products/SQL_Data_Compare/) adlı bir ürün sunar, ancak SQL Compare 'ten ayrı bir üründür ve farklı bir $395.

## <a name="taking-the-application-offline-during-deployment"></a>Dağıtım sırasında uygulamayı çevrimdışına alma

Bu öğreticiler genelinde yaptığımız gibi, dağıtım birden çok adımdan oluşan bir işlemdir: ASP.NET sayfalarını, ana sayfaları, CSS dosyalarını, JavaScript dosyalarını, resimleri ve diğer gerekli içeriği geliştirme ortamından üretime kopyalama ortamınızın gerekirse, üretim ortamına özgü yapılandırma bilgilerini kopyalama; ve son dağıtımdan bu yana veri modeline değişiklikler uygulanıyor. Dosya sayısına ve veritabanınızın karmaşıklığına bağlı olarak, bu adımların tamamlanması birkaç saniye ila birkaç dakika sürebilir. Bu pencere sırasında, Web uygulaması akıcı bir x ve siteyi ziyaret eden kullanıcılar hata ya da beklenmeyen davranışlarla karşılaşabilir.

Bir Web sitesi dağıtıldığında, dağıtım tamamlanana kadar Web uygulamasını "çevrimdışı" yapmak en iyisidir. Uygulamayı çevrimdışı hale getirme (ve dağıtım işlemi tamamlandıktan sonra yedekleme işlemi tamamlandıktan sonra), bir dosyayı karşıya yüklemek ve silmek kadar kolaydır. ASP.NET 2,0 ' den başlayarak, uygulama s kök dizinindeki `app_offline.htm` adlı bir dosyanın boyutundaydı varlığı, tüm Web sitesini "çevrimdışı" olarak alır. Bu sitedeki bir ASP.NET sayfasına yönelik tüm istekler `app_offline.htm` dosyanın içeriğiyle otomatik olarak yanıt verilir. Bu dosya kaldırıldıktan sonra uygulama yeniden çevrimiçi duruma gelir.

Dağıtım sırasında bir uygulamayı çevrimdışına almak, dağıtım işlemine başlamadan önce bir `app_offline.htm` dosyasını üretim ortamı s kök dizinine yüklemek ve ardından bir dağıtım tamamlandıktan sonra (veya başka bir şekilde yeniden adlandırmak) için bir dosyası yükleme kadar basittir. Bu teknik hakkında daha fazla bilgi için John Peterson s makalesine ve bir [*ASP.NET uygulamasını çevrimdışı duruma*](http://www.15seconds.com/issue/061207.htm)getirme bölümüne bakın.

## <a name="summary"></a>Özet

Veritabanı dağıtımı etrafında veri odaklı uygulama merkezleri dağıtmanın ana zorluğu. Geliştirme ortamında ve diğeri de üretim ortamında veritabanının iki sürümü olduğu için, geliştirmeye yeni özellikler eklendikçe bu iki veritabanı şeması eşitlenmemiş hale gelebilir. Daha fazlası, üretim veritabanı gerçek kullanıcıların gerçek verileriyle Doldurulmakta olduğu için, uygulamayı oluşturan dosyaları (ASP.NET sayfaları) dağıttığınızda yaptığınız gibi, değiştirilen geliştirme veritabanıyla birlikte üretim veritabanının üzerine yazabilirsiniz. görüntü dosyaları, vb.). Bunun yerine, bir veritabanını dağıtmak, son dağıtımdan bu yana üretim veritabanındaki geliştirme veritabanına yapılan tam değişiklik kümesini uygulamayı gerektirir.

Bu öğretici, veritabanı değişikliklerinin günlüğünü sürdürmek ve uygulamak için üç tekniği incelemiştir. En basit yaklaşım, değişiklikleri proo 'da kaydetmek. Bu taktik, bu değişiklikleri üretim veritabanında el ile işleyen bir işlem haline getirir ancak veritabanı nesneleri oluşturmak ve değiştirmek için SQL komutlarının bilgisine gerek yoktur. Daha karmaşık bir yaklaşım ve daha büyük projeler veya birden çok geliştiricilere sahip projeler için çok daha çok daha fazla bir yaklaşım tablosu, değişiklikleri bir dizi SQL komutu olarak kaydetmek için kullanılır. Bu değişiklikler, hedef veritabanında bu değişiklikleri büyük ölçüde hastens. Her iki yaklaşımdan en iyi şekilde, kırmızı kapı yazılım s SQL karşılaştırması gibi bir veritabanı karşılaştırma aracı kullanılarak elde edilebilir.

Bu öğretici, veri odaklı bir uygulamanın dağıtılmasıyla ilgili odaklanmamıza önem vermez. Sonraki öğreticiler kümesi, üretim ortamındaki hatalara nasıl yanıt vereceğini inceler. Sarı ekran olması yerine kolay bir hata sayfasının nasıl görüntüleneceğini inceleyeceğiz. Hata ayrıntılarını günlüğe kaydetme ve bu tür hatalar oluştuğunda sizi uyarma hakkında bilgi edineceksiniz.

Programlamanın kutlu olsun!

> [!div class="step-by-step"]
> [Önceki](configuring-a-website-that-uses-application-services-cs.md)
> [İleri](displaying-a-custom-error-page-cs.md)
