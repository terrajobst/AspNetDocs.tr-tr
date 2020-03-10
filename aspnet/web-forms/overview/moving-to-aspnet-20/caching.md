---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Önbelleğe alma | Microsoft Docs
author: microsoft
description: İyi performanslı bir ASP.NET uygulaması için önbelleğe almanın anlaşılmasına önem verir. ASP.NET 1. x, önbelleğe alma için üç farklı seçenek önerdi; çıktı önbelleği,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575938"
---
# <a name="caching"></a>Önbelleğe Alma

[Microsoft](https://github.com/microsoft) tarafından

> İyi performanslı bir ASP.NET uygulaması için önbelleğe almanın anlaşılmasına önem verir. ASP.NET 1. x, önbelleğe alma için üç farklı seçenek önerdi; çıktı önbelleği, parça önbelleği ve önbellek API 'SI.

İyi performanslı bir ASP.NET uygulaması için önbelleğe almanın anlaşılmasına önem verir. ASP.NET 1. x, önbelleğe alma için üç farklı seçenek önerdi; çıktı önbelleği, parça önbelleği ve önbellek API 'SI. ASP.NET 2,0, bu yöntemlerin üçünü de sunar, ancak bazı önemli ek özellikler ekler. Birçok yeni önbellek bağımlılığı vardır ve geliştiriciler artık özel önbellek bağımlılıklarını da oluşturma seçeneğine sahiptir. Önbelleğe alma yapılandırması Ayrıca ASP.NET 2,0 ' de önemli ölçüde geliştirilmiştir.

## <a name="new-features"></a>Yeni Özellikler

## <a name="cache-profiles"></a>Önbellek profilleri

Önbellek profilleri, geliştiricilerin her bir sayfaya uygulanabilen belirli önbellek ayarlarını tanımlamasına olanak tanır. Örneğin, 12 saat sonra önbellekten süresi dolmalı bir sayfa varsa, bu sayfalara uygulanabilen bir önbellek profilini kolayca oluşturabilirsiniz. Yeni bir önbellek profili eklemek için yapılandırma dosyasının &lt;outputCacheSettings&gt; bölümünü kullanın. Örneğin, aşağıda, 12 saatlik önbellek süresini yapılandıran *TwoDay* adlı bir önbellek profilinin yapılandırması verilmiştir.

[!code-xml[Main](caching/samples/sample1.xml)]

Bu önbellek profilini belirli bir sayfaya uygulamak için, aşağıda gösterildiği gibi @ OutputCache yönergesinin CacheProfile özniteliğini kullanın:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Özel önbellek bağımlılıkları

ASP.NET 1. x geliştirici özel önbellek bağımlılıkları için kırılan. ASP.NET 1. x içinde, CacheDependency sınıfı Sealed idi ve geliştiricilerin kendi sınıflarını türemesini engelledi. ASP.NET 2,0 ' de, bu sınırlama kaldırılır ve geliştiriciler kendi özel önbellek bağımlılıklarını geliştirmek için ücretsizdir. CacheDependency sınıfı, dosyalar, dizinler veya önbellek anahtarlarına göre özel bir önbellek bağımlılığı oluşturulmasına olanak sağlar.

Örneğin, aşağıdaki kod, Web uygulamasının kökünde bulunan. xml adlı bir dosyayı temel alan yeni bir özel önbellek bağımlılığı oluşturur:

[!code-csharp[Main](caching/samples/sample3.cs)]

Bu senaryoda,,. xml dosyası değiştiğinde önbelleğe alınmış öğe geçersiz kılınır.

Önbellek anahtarları kullanılarak özel bir önbellek bağımlılığı oluşturmak da mümkündür. Bu yöntemi kullanarak, önbellek anahtarının kaldırılması önbelleğe alınmış verileri geçersiz kılar. Aşağıdaki örnekte bu gösterilmektedir:

[!code-csharp[Main](caching/samples/sample4.cs)]

Yukarıya eklenen öğeyi geçersiz kılmak için önbelleğe eklenen öğeyi önbellek anahtarı olarak davranacak şekilde kaldırmanız yeterlidir.

[!code-csharp[Main](caching/samples/sample5.cs)]

Önbellek anahtarı olarak davranan öğe anahtarının, önbellek anahtarlarının dizisine eklenen değerle aynı olması gerektiğini unutmayın.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Yoklama tabanlı SQL önbellek bağımlılıkları (tablo tabanlı bağımlılıklar da denir)

SQL Server 7 ve 2000 SQL önbellek bağımlılıkları için yoklama tabanlı modeli kullanın. Yoklama tabanlı model, tablodaki veriler değiştiğinde tetiklenen bir veritabanı tablosunda bir tetikleyici kullanır. Bu tetikleyici, ASP.NET tarafından düzenli aralıklarla kontrol edilen bildirim tablosunda bir **Changeıd** alanı güncelleştirir. **Changeıd** alanı güncellendiyse, ASP.net verilerin değiştiğini bilir ve önbelleğe alınmış verileri geçersiz kılar.

> [!NOTE]
> SQL Server 2005, yoklama tabanlı modeli de kullanabilir, ancak yoklama tabanlı model en etkili model olmadığından, SQL Server 2005 ile sorgu tabanlı bir model (daha sonra ele alınmıştır) kullanmanız önerilir.

Yoklama tabanlı modeli kullanarak SQL önbellek bağımlılığının düzgün şekilde çalışmasını sağlamak için, tablolarda bildirimlerin etkinleştirilmiş olması gerekir. Bu, SqlCacheDependencyAdmin sınıfı kullanılarak veya ASPNET\_regsql. exe yardımcı programı kullanılarak programlı bir şekilde gerçekleştirilebilir.

Aşağıdaki komut satırı, Products tablosunu SQL önbellek bağımlılığı için *dBASE* adlı bir SQL Server örneğinde bulunan Northwind veritabanına kaydeder.

[!code-console[Main](caching/samples/sample6.cmd)]

Yukarıdaki komutta kullanılan komut satırı anahtarlarının bir açıklaması aşağıda verilmiştir:

| **Komut satırı anahtarı** | **Amaç** |
| --- | --- |
| -S *sunucusu* | Sunucu adını belirtir. |
| -Ed | SQL önbellek bağımlılığı için veritabanının etkin olması gerektiğini belirtir. |
| -d *veritabanı\_adı* | SQL önbellek bağımlılığı için etkinleştirilmesi gereken veritabanı adını belirtir. |
| -E | ASPNET\_regsql 'in veritabanına bağlanırken Windows kimlik doğrulaması kullanması gerektiğini belirtir. |
| -et | SQL önbellek bağımlılığı için bir veritabanı tablosu etkinleştirdiğimiz belirtilir. |
| -t *tablo\_adı* | SQL önbellek bağımlılığı etkinleştirilecek veritabanı tablosunun adını belirtir. |

> [!NOTE]
> ASPNET\_regsql. exe ' ye yönelik başka anahtarlar da mevcuttur. Tam bir liste için, ASPNET\_regsql. exe-? komutunu çalıştırın. bir komut satırından.

Bu komut çalıştırıldığında SQL Server veritabanında aşağıdaki değişiklikler yapılır:

- **AspNet\_SqlCacheTablesForChangeNotification** tablosu eklenir. Bu tablo, SQL önbellek bağımlılığının etkinleştirildiği veritabanındaki her tablo için bir satır içerir.
- Aşağıdaki saklı yordamlar veritabanının içinde oluşturulur:

| AspNet\_SqlCachePollingStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification tablosunu sorgular ve SQL önbellek bağımlılığı için etkinleştirilen tüm tabloları ve her bir tablonun Changeıd değerini döndürür. Bu saklı yordam, verilerin değişip değişmediğini belirlemede yoklama için kullanılır. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification tablosunu sorgulayarak SQL önbellek bağımlılığı için etkinleştirilen tüm tabloları döndürür ve SQL önbellek bağımlılığı için etkinleştirilen tüm tabloları döndürür. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | Bildirim tablosuna gerekli girişi ekleyerek SQL önbellek bağımlılığı için bir tablo kaydeder ve tetikleyiciyi ekler. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | Bildirim tablosundaki girişi kaldırarak SQL önbellek bağımlılığı tablosunun kaydını siler ve tetikleyiciyi kaldırır. |
| AspNet\_Sqlcacheupdatechangeıdstoredprocedure | Değiştirilen tablo için Changeıd 'yi artırarak bildirim tablosunu güncelleştirir. ASP.NET, verilerin değişip değişmediğini anlamak için bu değeri kullanır. Aşağıda gösterildiği gibi, bu saklı yordam tablo etkinleştirildiğinde oluşturulan tetikleyici tarafından yürütülür. |

- Tablo  **_\_adı_\_AspNet\_SqlCacheNotification\_tetikleyicisi** SQL Server adlı bir tetikleyici oluşturulur. Bu tetikleyici, tabloda bir INSERT, UPDATE veya DELETE işlemi gerçekleştirildiğinde, AspNet\_Sqlcacheupdatechangeıdstoredprocedure komutunu yürütür.
- SQL Server **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** adlı bir rol veritabanına eklenir.

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server rolü ASPNET\_SqlCachePollingStoredProcedure için exec izinlerine sahiptir. Yoklama modelinin düzgün çalışması için, işlem hesabınızı ASPNET\_ChangeNotification\_ReceiveNotificationsOnlyAccess rolüne eklemeniz gerekir. ASPNET\_regsql. exe aracı bunu sizin için yapamayacak.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Yoklama tabanlı SQL önbellek bağımlılıklarını yapılandırma

Yoklama tabanlı SQL önbellek bağımlılıklarını yapılandırmak için gereken birkaç adım vardır. İlk adım, veritabanını ve tabloyu yukarıda anlatıldığı gibi etkinleştirmektir. Bu adım tamamlandıktan sonra yapılandırmanın geri kalanı aşağıdaki gibidir:

- ASP.NET yapılandırma dosyası yapılandırılıyor.
- SqlCacheDependency yapılandırma

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET yapılandırma dosyasını yapılandırma

Önceki modülde anlatıldığı gibi bir bağlantı dizesi eklemenin yanı sıra, aşağıda gösterildiği gibi &lt;sqlCacheDependency&gt; öğesiyle bir &lt;Cache&gt; öğesi de yapılandırmanız gerekir:

[!code-xml[Main](caching/samples/sample7.xml)]

Bu yapılandırma, *pubs* VERITABANıNDA bir SQL önbellek bağımlılığı sunar. &lt;sqlCacheDependency&gt; öğesinin pollTime özniteliğinin varsayılan olarak 60000 milisaniye veya 1 dakika olacağını unutmayın. (Bu değer 500 milisaniyeden az olamaz.) Bu örnekte, &lt;Add&gt; öğesi yeni bir veritabanı ekler ve yoklamanın süresini geçersiz kılar, bu da 9000000 milisaniyelik olarak ayarlanıyor.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency yapılandırma

Bir sonraki adım, SqlCacheDependency öğesini yapılandırmaktır. Bunu yapmanın en kolay yolu, şu şekilde @ Outcache yönergesinde SqlDependency özniteliği için değeri belirtmektir:

[!code-aspx[Main](caching/samples/sample8.aspx)]

Yukarıdaki @ OutputCache yönergesinde, *pubs* veritabanındaki *yazarlar* tablosu için bir SQL önbellek bağımlılığı yapılandırılmıştır. Birden çok bağımlılığı, şöyle bir noktalı virgülle ayırarak yapılandırılabilir:

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency 'yi yapılandırmaya yönelik başka bir yöntem bunu program aracılığıyla yapmak için kullanılır. Aşağıdaki kod, *pubs* veritabanındaki *yazarlar* tablosunda yeni bir SQL önbellek bağımlılığı oluşturur.

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL önbellek bağımlılığını programlı bir şekilde tanımlamayı kullanmanın avantajlarından biri, oluşabilecek tüm özel durumları işleyebilmeniz olabilir. Örneğin, bildirim için etkinleştirilmemiş bir veritabanı için SQL önbellek bağımlılığı tanımlamaya çalışırsanız, bir **DatabaseNotEnabledForNotificationException** özel durumu oluşturulur. Bu durumda, **SqlCacheDependencyAdmin. EnableNotifications** yöntemini çağırarak ve veritabanı adını geçirerek veritabanını bildirimler için etkinleştirmeyi deneyebilirsiniz.

Benzer şekilde, bildirim için etkinleştirilmemiş bir tablo için SQL önbellek bağımlılığı tanımlamaya çalışırsanız, bir **TableNotEnabledForNotificationException** oluşturulur. Daha sonra, veritabanı adı ve tablo adı geçirerek **SqlCacheDependencyAdmin. EnableTableForNotifications** metodunu çağırabilirsiniz.

Aşağıdaki kod örneği, bir SQL önbellek bağımlılığı yapılandırılırken özel durum işlemenin nasıl düzgün şekilde yapılandırılacağını göstermektedir.

[!code-csharp[Main](caching/samples/sample11.cs)]

Daha fazla bilgi: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Sorgu tabanlı SQL önbellek bağımlılıkları (yalnızca SQL Server 2005)

SQL önbellek bağımlılığı için SQL Server 2005 kullanılırken yoklama tabanlı model gerekli değildir. SQL Server 2005 ile kullanıldığında, SQL önbellek bağımlılıkları, SQL Server 2005 sorgu bildirimlerini kullanarak doğrudan SQL bağlantıları aracılığıyla SQL Server örneğine (başka yapılandırma gerekmez) iletişim kurar.

Sorgu tabanlı bildirimi etkinleştirmenin en kolay yolu, veri kaynağı nesnesinin **SqlCacheDependency** özniteliğini **CommandNotification** olarak ayarlayarak ve **EnableCaching** özniteliğini **true**olarak ayarlayarak bunu bildirimli olarak yapabilmenizi sağlar. Bu yöntemi kullanarak, kod gerekmez. Veri kaynağına karşı yürütülen bir komutun sonucu değişirse, önbellek verilerini geçersiz kılar.

Aşağıdaki örnekte SQL önbellek bağımlılığı için bir veri kaynağı denetimi yapılandırılır:

[!code-aspx[Main](caching/samples/sample12.aspx)]

Bu durumda, **SelectCommand** öğesinde belirtilen sorgu, ilk olarak gerçekleşenden farklı bir sonuç döndürürse, önbelleğe alınan sonuçlar geçersiz kılınır.

Ayrıca, **@ OutputCache** yönergesinin **SqlDependency** ÖZNITELIĞINI **CommandNotification**olarak ayarlayarak SQL önbellek bağımlılıkları için tüm veri kaynaklarınızı etkinleşmesini de belirtebilirsiniz. Aşağıdaki örnekte bu gösterilmektedir.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005 ' deki sorgu bildirimleri hakkında daha fazla bilgi için çevrimiçi SQL Server Books Online 'a bakın.

Sorgu tabanlı bir SQL önbellek bağımlılığı yapılandırmanın başka bir yöntemi, bunu programlı olarak SqlCacheDependency sınıfını kullanarak kullanmaktır. Aşağıdaki kod örneği, bunun nasıl yapıldığını göstermektedir.

[!code-csharp[Main](caching/samples/sample14.cs)]

Daha fazla bilgi: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Önbellek sonrası değiştirme

Bir sayfanın önbelleğe alınması, bir Web uygulamasının performansını ciddi ölçüde artırabilir. Ancak bazı durumlarda, sayfanın büyük bir kısmının önbelleğe alınması ve sayfadaki bazı parçaların dinamik olması gerekir. Örneğin, bir zaman kümesi için tamamen statik olan bir haber hikayeleri sayfası oluşturursanız, tüm sayfayı önbelleğe alınmış olarak ayarlayabilirsiniz. Her sayfa isteğinde değiştirilen bir döndürme ad başlığını eklemek isterseniz, sayfanın tanıtımı içeren bölümünün dinamik olması gerekir. Bir sayfayı önbelleğe alma, ancak bazı içerikleri dinamik olarak değiştirme için ASP.NET önbellek değiştirme 'yi kullanabilirsiniz. Önbellek sonrası değiştirme ile sayfanın tamamı, önbelleğe alma dışında tut olarak işaretlenen belirli bölümlerle önbelleğe alınmış çıktıdır. Ad başlıkları örneğinde, AdRotator denetimi, her kullanıcı için ve her sayfa yenileme için, reklamları dinamik olarak oluşturulacak şekilde önbellek sonrası değiştirme özelliğinden yararlanmanızı sağlar.

Önbellek sonrası değiştirme uygulamak için üç yol vardır:

- , Değiştirme denetimini kullanarak bildirimli olarak.
- Değiştirme denetimi API 'sini kullanarak programlı bir şekilde.
- AdRotator denetimini kullanarak örtülü olarak.

### <a name="substitution-control"></a>Değiştirme denetimi

ASP.NET değiştirme denetimi, önbelleğe alınmış sayfanın önbelleğe alma yerine dinamik olarak oluşturulan bir bölümünü belirtir. Sayfada dinamik içeriğin görünmesini istediğiniz konuma bir değiştirme denetimi yerleştirebilirsiniz. Çalışma zamanında, değiştirme denetimi MethodName özelliği ile belirttiğiniz bir yöntemi çağırır. Yöntem, daha sonra değiştirme denetiminin içeriğinin yerini alan bir dize döndürmelidir. Yöntemin, kapsayan sayfada veya UserControl denetiminde statik bir yöntem olması gerekir. Değiştirme denetiminin kullanılması, istemci tarafı önbelleğe alınabilirliğini sunucu önbelleğe alınabilirliğini olarak değiştirilmesine neden olur, böylece sayfa istemcide önbelleğe alınmaz. Bu, sayfa için gelecekteki isteklerin dinamik içerik oluşturmak üzere yöntemi yeniden çağırmasını sağlar.

### <a name="substitution-api"></a>Değiştirme API 'SI

Önbelleğe alınmış bir sayfa için programlı olarak dinamik içerik oluşturmak için, sayfa kodunuzda [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) yöntemini çağırabilirsiniz ve bir yöntemin adını parametre olarak geçirerek bir parametre olarak kullanabilirsiniz. Dinamik içeriğin oluşturulmasını işleyen yöntemi tek bir [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) parametresi alır ve bir dize döndürür. Döndürülen dize, belirtilen konumda değiştirilecek olan içeriktir. Değiştirme denetimini bildirimli olarak kullanmak yerine WriteSubstitution metodunu çağırmanın bir avantajı, sayfanın veya UserControl nesnesinin statik bir yöntemini çağırmak yerine herhangi bir rastgele nesnenin yöntemini çağırabilmeniz.

WriteSubstitution yönteminin çağrılması, istemci tarafı önbelleğe alınabilirliğini sunucu önbelleğe alınabilirliğini olarak değiştirilmesine neden olur, böylece sayfa istemcide önbelleğe alınmaz. Bu, sayfa için gelecekteki isteklerin dinamik içerik oluşturmak üzere yöntemi yeniden çağırmasını sağlar.

### <a name="adrotator-control"></a>AdRotator denetimi

AdRotator sunucu denetimi, dahili önbelleğe alma sonrası değiştirme desteği uygular. Sayfanıza bir AdRotator denetimi yerleştirirseniz, üst sayfanın önbelleğe alınıp alınmadığına bakılmaksızın her istekte benzersiz tanıtımlar işlenir. Sonuç olarak, bir AdRotator denetimi içeren bir sayfa yalnızca sunucu tarafında önbelleğe alınır.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy sınıfı

ControlCachePolicy sınıfı, Kullanıcı denetimleri kullanılarak parça önbelleklemesi için programlı denetim sağlar. ASP.NET, kullanıcı denetimlerini bir [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) örneği içinde katıştırır. BasePartialCachingControl Sınıfı, çıktı önbelleği etkin olan bir kullanıcı denetimini temsil eder.

[PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) denetiminin [BasePartialCachingControl. CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) özelliğine eriştiğinizde, her zaman geçerli bir ControlCachePolicy nesnesi alacaksınız. Ancak, bir [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) denetiminin [UserControl. CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) özelliğine eriştiğinizde, yalnızca Kullanıcı denetimi bir BasePartialCachingControl denetimiyle sarılmış ise geçerli bir ControlCachePolicy nesnesi alırsınız. Sarmalanmadığı takdirde, özelliği tarafından döndürülen ControlCachePolicy nesnesi, ilişkili bir BasePartialCachingControl içermediğinden, onu işlemeyi denediğinizde özel durumlar oluşturur. Bir UserControl örneğinin özel durum oluşturmadan önbelleğe almayı destekleyip desteklemediğini anlamak için, [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) özelliğini inceleyin.

ControlCachePolicy sınıfının kullanılması, çıktı önbelleğe almayı etkinleştirebilmenizin çeşitli yöntemlerinden biridir. Aşağıdaki listede, çıktı önbelleği 'ni etkinleştirmek için kullanabileceğiniz yöntemler açıklanmaktadır:

- Bildirim temelli senaryolarda çıktı önbelleğe almayı etkinleştirmek için [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) yönergesini kullanın.
- Arka plan kod dosyasındaki bir kullanıcı denetimi için önbelleğe almayı etkinleştirmek üzere [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) özniteliğini kullanın.
- Önceki yöntemlerden birini kullanarak ve [System. Web. UI. TemplateControl. LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) yöntemi kullanılarak dinamik olarak yüklenen BasePartialCachingControl örnekleriyle birlikte çalıştığınız programlama senaryolarında önbellek ayarlarını belirtmek için ControlCachePolicy sınıfını kullanın.

Bir ControlCachePolicy örneği, yalnızca denetim yaşam döngüsünün Init ve PreRender aşamaları arasında başarılı bir şekilde işlenebilir. Bir ControlCachePolicy nesnesini PreRender aşamasından sonra değiştirirseniz, Denetim oluşturulduktan sonra yapılan tüm değişiklikler önbellek ayarlarını etkilemediği için ASP.NET bir özel durum oluşturur (oluşturma aşamasında bir denetim önbelleğe alınır). Son olarak, bir kullanıcı denetim örneği (ve bu nedenle ControlCachePolicy nesnesi) yalnızca aslında işlendiğinde programlı düzenleme için kullanılabilir.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Önbelleğe alma yapılandırmasındaki değişiklikler-&lt;önbelleğe alma&gt; öğesi

ASP.NET 2,0 ' de önbelleğe alma yapılandırmasında birkaç değişiklik vardır. &lt;Caching&gt; öğesi ASP.NET 2,0 ' de yenidir ve yapılandırma dosyasında önbelleğe alma yapılandırma değişiklikleri yapmanıza olanak sağlar. Aşağıdaki öznitelikler kullanılabilir.

| **Öğe** | **Açıklama** |
| --- | --- |
| **önbellek** | İsteğe bağlı öğe. Genel uygulama önbelleği ayarlarını tanımlar. |
| **outputCache** | İsteğe bağlı öğe. Uygulama genelinde çıkış önbelleği ayarlarını belirtir. |
| **outputCacheSettings** | İsteğe bağlı öğe. Uygulamadaki sayfalara uygulanabilen çıkış önbelleği ayarlarını belirtir. |
| **sqlCacheDependency** | İsteğe bağlı öğe. Bir ASP.NET uygulamasının SQL önbellek bağımlılıklarını yapılandırır. |

### <a name="the-ltcachegt-element"></a>&lt;Cache&gt; öğesi

Aşağıdaki öznitelikler &lt;Cache&gt; öğesinde bulunabilir:

| **Öznitelik** | **Açıklama** |
| --- | --- |
| **Disablememori koleksiyonu** | İsteğe bağlı **Boolean** özniteliği. Makine bellek baskısı altında olduğunda gerçekleşen önbellek belleği koleksiyonunun devre dışı bırakılıp bırakılmadığını gösteren bir değer alır veya ayarlar. |
| **disableExpiration** | İsteğe bağlı **Boolean** özniteliği. Önbelleğin süresinin dolmasının devre dışı bırakılıp bırakılmadığını gösteren bir değer alır veya ayarlar. Devre dışı bırakıldığında, önbelleğe alınmış öğelerin süre sonu yoktur ve zaman aşımına uğradı önbellek öğelerinin arka planda atılması oluşmaz. |
| **privateBytesLimit** | İsteğe bağlı **Int64** özniteliği. Önbellek, süre dolmayan öğeleri temizlemeye ve belleği geri almaya çalışmadan önce uygulamanın özel baytlarının maksimum boyutunu gösteren bir değer alır veya ayarlar. Bu sınır, hem önbelleğin hem de çalışan uygulamadan normal bellek ek yükünün kullanıldığı belleği içerir. Sıfır ayarı, ASP.NET geri kazanma belleğin ne zaman başlatılacağını belirlemek için kendi buluşsal yöntemlerini kullanacağını gösterir. |
| **percentagePhysicalMemoryUsedLimit** | İsteğe bağlı **Int32** özniteliği. Önbellek, süre dolmayan öğeleri temizlemeye başlamadan önce bir uygulama tarafından tüketilen fiziksel belleğin maksimum yüzdesini gösteren bir değer alır veya ayarlar ve bu bellek kullanımı, önbellek tarafından kullanılan belleği da içerir çalışan uygulamanın normal bellek kullanımı. Sıfır ayarı, ASP.NET geri kazanma belleğin ne zaman başlatılacağını belirlemek için kendi buluşsal yöntemlerini kullanacağını gösterir. |
| **privateBytesPollTime** | İsteğe bağlı **TimeSpan** özniteliği. Uygulamanın özel bayt bellek kullanımı için yoklama arasındaki zaman aralığını gösteren bir değer alır veya ayarlar. |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; öğesi

&lt;outputCache&gt; öğesi için aşağıdaki öznitelikler bulunur.

|       <strong>Öznitelik</strong>        |                                                                                                                                                                                                                                                       <strong>Açıklama</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          İsteğe bağlı <strong>Boolean</strong> özniteliği. Sayfa çıktısı önbelleğini etkinleştirilir/devre dışı bırakır. Devre dışı bırakılırsa, programlama veya bildirim temelli ayarlardan bağımsız olarak hiçbir sayfa önbelleğe alınmaz. Varsayılan değer <strong>true</strong>'dur.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                İsteğe bağlı <strong>Boolean</strong> özniteliği. Uygulama parçası önbelleğini etkinleştirilir/devre dışı bırakır. Devre dışı bırakılırsa, kullanılan [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) yönergesi veya önbellek profilinden bağımsız olarak hiçbir sayfa önbelleğe alınmaz. , Yukarı akış proxy sunucularının yanı sıra tarayıcı istemcilerinin sayfa çıkışını önbelleğe alma girişiminde bulunmadığını belirten bir Cache-Control üst bilgisi içerir. Varsayılan değer <strong>false</strong>'dur.                                                 |
| <strong>Sendcachecontrolüstbilgisi</strong> |                                                                                                                                                      İsteğe bağlı <strong>Boolean</strong> özniteliği. <strong>Cache-Control: Private</strong> üstbilgisinin varsayılan olarak çıktı önbelleği modülü tarafından gönderilip gönderilmeyeceğini gösteren bir değer alır veya ayarlar. Varsayılan değer <strong>false</strong>'dur.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | İsteğe bağlı <strong>Boolean</strong> özniteliği. Http göndermeyi etkinleştirilir/devre dışı bırakır "<strong>, yanıtta \</strong ><em>" üst bilgisi değişir. Varsayılan değeri false olan "</em>* Vary: \*<strong>" üst bilgisi, önbelleğe alınmış çıkış sayfaları için gönderilir. Vary üst bilgisi gönderildiğinde, farklı sürümlerin Vary üst bilgisinde belirtilere bağlı olarak önbelleğe alınmasını sağlar. Örneğin, <em>farklılık gösterir: Kullanıcı aracıları</em> , isteği veren kullanıcı aracısına göre bir sayfanın farklı sürümlerini depolayacaktır. Varsayılan değer * * false şeklindedir</strong>. |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; öğesi

&lt;outputCacheSettings&gt; öğesi, daha önce açıklandığı gibi önbellek profillerinin oluşturulmasına izin verir. &lt;outputCacheSettings&gt; öğesi için tek alt öğe, önbellek profillerini yapılandırmak için &lt;outputCacheProfiles&gt; öğesidir.

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; öğesi

&lt;sqlCacheDependency&gt; öğesi için aşağıdaki öznitelikler bulunur.

| **Öznitelik** | **Açıklama** |
| --- | --- |
| **etkinletir** | Gerekli **Boole** özniteliği. İçin değişiklik yapılıp yapılmayacağını belirtir. |
| **pollTime** | İsteğe bağlı **Int32** özniteliği. SqlCacheDependency, veritabanı tablosunu değişiklikler için yokladığı sıklığı ayarlar. Bu değer, birbirini izleyen yoklamalar arasındaki milisaniye sayısına karşılık gelir. 500 milisaniyeden az bir şekilde ayarlanamaz. Varsayılan değer 1 dakikadır. |

### <a name="more-information"></a>Daha Fazla Bilgi

Önbellek yapılandırmasıyla ilgili bilmeniz gereken bazı ek bilgiler vardır.

- Çalışan işleminin özel bayt sınırı ayarlanmamışsa, önbellek aşağıdaki sınırların birini kullanır: 

    - x86 2GB: 800 MB veya fiziksel RAM %60, hangisi daha küçüktür
    - x86 3GB: fiziksel RAM 'in 1800MB veya %60 ' u, hangisi daha az
    - x64:1 terabaytlık veya fiziksel RAM %60, hangisi daha küçüktür
- Hem çalışan işlem özel baytları sayısı hem de &lt;Cache privateBytesLimit/&gt; ayarlanırsa, önbellek en az iki değeri kullanır.
- 1\. x içinde olduğu gibi, önbellek girdilerini düşürüyoruz ve GC çağrısı yaptık. İki nedenden dolayı toplayın: 

    - Özel bayt sınırına çok yakınız
    - Kullanılabilir bellek, %10 ' dan yakın veya bundan küçük
- &lt;Cache percentagePhysicalMemoryUseLimit/&gt; ayarını 100 olarak ayarlayarak düşük kullanılabilir bellek koşulları için kırpma ve önbelleği etkin bir şekilde devre dışı bırakabilirsiniz.
- 1\. x aksine, 2,0, son GC ise kırpmayı askıya alacak ve çağrıları toplayacaktır. Collect, (önbellek) bellek sınırının %1 ' inden büyük olan özel baytları veya yönetilen yığınlara ait boyutu düşürmedi.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: özel önbellek bağımlılıkları

1. Yeni bir Web sitesi oluşturun.
2. Cache. xml adlı yeni bir XML dosyası ekleyin ve bunu Web uygulamasının köküne kaydedin.
3. Aşağıdaki kodu, default. aspx öğesinin arka plan kodundaki\_Load yöntemine ekleyin: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Kaynak görünümünde default. aspx ' in en üstüne aşağıdakileri ekleyin: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Default. aspx ' i inceleyin. Zaman ne olacak?
6. Tarayıcıyı yenileyin. Zaman ne olacak?
7. Cache. xml ' i açın ve aşağıdaki kodu ekleyin: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Cache. xml ' i kaydedin.
9. Tarayıcınızı yenileyin. Zaman ne olacak?
10. Daha önce önbelleğe alınmış değerleri görüntülemek yerine zamanın neden güncelleştirildiğini açıklayın:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Laboratuvar 2: yoklama tabanlı önbellek bağımlılıklarını kullanma

Bu laboratuvar, bir GridView ve DetailsView denetimi aracılığıyla Northwind veritabanındaki verilerin düzenlenmesine izin veren önceki modülde oluşturduğunuz projeyi kullanır.

1. Projeyi Visual Studio 2005 ' de açın.
2. Veritabanı ve Ürünler tablosunu etkinleştirmek için ASPNET\_regsql yardımcı programını Northwind veritabanına göre çalıştırın. Bir Visual Studio komut Isteminden aşağıdaki komutu kullanın: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Aşağıdakileri Web. config dosyanıza ekleyin: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. ShowData. aspx adlı yeni bir WebForm ekleyin.
5. Aşağıdaki @ OutputCache yönergesini ShowData. aspx sayfasına ekleyin: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Aşağıdaki kodu, ShowData. aspx\_Load sayfasına ekleyin: 

    [!code-html[Main](caching/samples/sample21.html)]
7. ShowData. aspx öğesine yeni bir SqlDataSource denetimi ekleyin ve Northwind veritabanı bağlantısını kullanacak şekilde yapılandırın. İleri'ye tıklayın.
8. ProductName ve ProductID onay kutularını seçin ve Ileri ' ye tıklayın.
9. Son'a tıklayın.
10. ShowData. aspx sayfasına yeni bir GridView ekleyin.
11. Açılan listeden SqlDataSource1 öğesini seçin.
12. ShowData. aspx ' i kaydedin ve inceleyin. Görüntülenme zamanı hakkında bir dikkat edin.
