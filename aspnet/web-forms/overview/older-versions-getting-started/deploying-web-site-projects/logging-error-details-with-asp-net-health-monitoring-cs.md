---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
title: ASP.NET sistem durumu Izleme (C#) Ile hata ayrıntılarını günlüğe kaydetme Microsoft Docs
author: rick-anderson
description: Microsoft 'un sistem durumu izleme sistemi, işlenmemiş özel durumlar da dahil çeşitli Web olaylarını günlüğe kaydetmek için kolay ve özelleştirilebilir bir yol sağlar. Bu öğretici, trr...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: b1abb452-642a-4ff3-8504-37b85590ff79
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
msc.type: authoredcontent
ms.openlocfilehash: e52ed94f78d053701771690fce432d5a1d465b62
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637295"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-c"></a>ASP.NET Durum İzleme ile Hata Ayrıntılarını Günlüğe Kaydetme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_cs.pdf)

> Microsoft 'un sistem durumu izleme sistemi, işlenmemiş özel durumlar da dahil çeşitli Web olaylarını günlüğe kaydetmek için kolay ve özelleştirilebilir bir yol sağlar. Bu öğreticide, işlenmemiş özel durumları bir veritabanına günlüğe kaydetmek ve geliştiricilere bir e-posta iletisiyle bildirmek için sistem durumu izleme sisteminin ayarlanması gösterilmektedir.

## <a name="introduction"></a>Giriş

Günlüğe kaydetme, dağıtılan bir uygulamanın sistem durumunu izlemek ve ortaya çıkabilecek sorunları tanılamak için yararlı bir araçtır. Daha önce dağıtılan bir uygulamada meydana gelen hataların, düzeltilebilir olması için günlüğe kaydetmek özellikle önemlidir. `Error` olayı, bir ASP.NET uygulamasında işlenmeyen bir özel durum oluştuğunda tetiklenir; [önceki öğreticide](processing-unhandled-exceptions-cs.md) bir hata geliştiricisine bildirme ve `Error` olayı için bir olay işleyicisi oluşturarak ayrıntılarını günlüğe kaydetme işlemlerinin nasıl yapılacağı gösterildi. Ancak, bu görev ASP tarafından gerçekleştirilebileceği için hatanın ayrıntılarını günlüğe kaydetmek ve bir geliştiriciye bildirmek üzere `Error` olay işleyicisi oluşturma işlemi gereksizdir. NET 'in *sistem durumu izleme sistemi*.

Sistem durumu izleme sistemi, ASP.NET 2,0 ' de tanıtılmıştı ve uygulamanın veya isteğin ömrü boyunca oluşan olayları günlüğe kaydederek dağıtılan bir ASP.NET uygulamasının sistem durumunu izlemek üzere tasarlanmıştır. Sistem durumu izleme sistemi tarafından günlüğe kaydedilen olaylar, *sistem durumu izleme olayları* veya *Web olayları*olarak adlandırılır ve şunları içerir:

- Uygulamanın başladığı veya durduğu gibi uygulama ömür olayları
- Başarısız oturum açma girişimleri ve başarısız URL yetkilendirme istekleri dahil olmak üzere güvenlik olayları
- İşlenmemiş özel durumlar da dahil olmak üzere uygulama hataları, diğer hata türleri arasında durum ayrıştırma özel durumlarını, istek doğrulama özel durumlarını ve derleme hatalarını görüntüleyin.

Bir sistem durumu izleme olayı ortaya çıktığında, belirtilen sayıda *günlük kaynağında*günlüğe kaydedilebilir. Sistem durumu izleme sistemi, Web olaylarını bir Microsoft SQL Server veritabanına, Windows olay günlüğüne veya bir e-posta iletisiyle, diğerleri arasında günlüğe kaydetmek için kullanılan günlük kaynaklarıyla birlikte gelir. Ayrıca, kendi günlük kaynaklarınızı de oluşturabilirsiniz.

Sistem günlüklerinin sistem günlüklerinin, kullanılan günlük kaynaklarıyla birlikte `Web.config`olarak tanımlanmıştır. Birkaç dizi yapılandırma biçimlendirmesinde, işlenmemiş tüm özel durumları bir veritabanına kaydetmek ve e-posta yoluyla özel durum bildirmek için sistem durumu izlemeyi kullanabilirsiniz.

## <a name="exploring-the-health-monitoring-systems-configuration"></a>Sistem durumu Izleme sisteminin yapılandırmasını keşfetme

Sistem durumu izleme sisteminin davranışı, `Web.config`[`<healthMonitoring>` öğesinde](https://msdn.microsoft.com/library/2fwh2ss9.aspx) bulunan yapılandırma bilgileri tarafından tanımlanır. Bu yapılandırma bölümü, aşağıdaki üç önemli bilgi parçasını diğer şeyler arasında tanımlar:

1. Oluşturulan, ne zaman günlüğe kaydedilecek olan durum izleme olayları,
2. Günlük kaynakları ve
3. (1) içinde tanımlanan her bir sistem durumu izleme olayının (2) içinde tanımlanan günlük kaynaklarıyla eşlenme şekli.

Bu bilgiler üç alt yapılandırma öğesi aracılığıyla belirtilir: sırasıyla [`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx), [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)ve [`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx).

Varsayılan sistem durumu izleme sistem yapılandırma bilgileri `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` klasöründeki `Web.config` dosyasında bulunabilir. Bu varsayılan yapılandırma bilgileri, breçekimi için bazı biçimlendirmeler kaldırılarak aşağıda gösterilmiştir:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample1.xml)]

İlgilendiğiniz durum izleme olayları, bir sistem durumu izleme olayları sınıfına kolay bir ad veren `<eventMappings>` öğesinde tanımlanmıştır. Yukarıdaki biçimlendirme içinde `<eventMappings>` öğesi, "tüm hatalar" adlı insan kullanımı kolay adını, `WebBaseErrorEvent` türündeki sistem durumu izleme olaylarına ve `WebFailureAuditEvent`türündeki olayları izlemek için "hata denetimleri" olarak atar.

`<providers>` öğesi, günlük kaynaklarını tanımlar, böylece kullanıcılara kolay bir ad verir ve günlük kaynağa özgü yapılandırma bilgilerini belirtir. İlk `<add>` öğesi, `EventLogWebEventProvider` sınıfını kullanarak belirtilen sistem durumu izleme olaylarını günlüğe kaydeden "EventLogProvider" sağlayıcısını tanımlar. `EventLogWebEventProvider` sınıfı, olayı Windows olay günlüğü 'ne kaydeder. İkinci `<add>` öğesi, olayları `SqlWebEventProvider` sınıfı aracılığıyla bir Microsoft SQL Server veritabanına kaydeden "SqlWebEventProvider" sağlayıcısını tanımlar. "SqlWebEventProvider" yapılandırması, veritabanının bağlantı dizesini (`connectionStringName`) diğer yapılandırma seçenekleri arasında belirtir.

`<rules>` öğesi, `<eventMappings>` öğesinde belirtilen olayları `<providers>` öğesindeki günlük kaynaklarına eşler. Varsayılan olarak, ASP.NET Web uygulamaları işlenmeyen tüm özel durumları ve denetim başarısızlıklarını Windows olay günlüğü 'ne kaydeder.

## <a name="logging-events-to-a-database"></a>Olayları bir veritabanına kaydetme

Sistem durumu izleme sisteminin varsayılan yapılandırması, uygulamanın `Web.config` dosyasına bir `<healthMonitoring>` bölümü eklenerek, Web uygulaması tarafından Web uygulaması temelinde özelleştirilebilir. `<add>` öğesini kullanarak `<eventMappings>`, `<providers>`ve `<rules>` bölümlerine ek öğeler ekleyebilirsiniz. Varsayılan yapılandırmadan bir ayarı kaldırmak için `<remove>` öğesini kullanın veya bu bölümlerden birindeki tüm varsayılan değerleri kaldırmak için `<clear />` kullanın. Kitap Incelemeleri Web uygulamasını, `SqlWebEventProvider` sınıfını kullanarak işlenmemiş tüm özel durumları bir Microsoft SQL Server veritabanına günlüğe kaydetmek üzere yapılandıralim.

`SqlWebEventProvider` sınıfı, sistem durumu izleme sisteminin bir parçasıdır ve belirtilen bir SQL Server veritabanına bir sistem durumu izleme olayını günlüğe kaydeder. `SqlWebEventProvider` sınıfı, belirtilen veritabanının `aspnet_WebEvent_LogEvent`adlı bir saklı yordam içermesini bekler. Bu saklı yordam, olayın ayrıntılarını geçti ve olay ayrıntılarının depolanarak tasimiyle. İyi haberler, bu saklı yordamı veya olay ayrıntılarını depolamak için tabloyu oluşturmanıza gerek kalmaz. `aspnet_regsql.exe` aracını kullanarak bu nesneleri veritabanınıza ekleyebilirsiniz.

> [!NOTE]
> `aspnet_regsql.exe` Aracı, ASP desteği eklediğimiz sırada [ *uygulama hizmetleri öğreticisini kullanan bir Web sitesi yapılandırma* ](configuring-a-website-that-uses-application-services-cs.md) konusunda geri alınmıştır. NET 'in uygulama hizmetleri. Sonuç olarak, Book Incelemeleri Web sitesinin veritabanı, olay bilgilerini `aspnet_WebEvent_Events`adlı bir tabloya depolayan `aspnet_WebEvent_LogEvent` saklı yordamını zaten içeriyor.

Veritabanınıza gerekli saklı yordam ve tablo eklendikten sonra, tüm işlenmeyen özel durumları veritabanına kaydetmek için sistem durumu izlemeye söylemek önemlidir. Web sitenizin `Web.config` dosyasına aşağıdaki biçimlendirmeyi ekleyerek bunu gerçekleştirin:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample2.xml)]

Yukarıdaki sistem durumu izleme yapılandırması biçimlendirmesi, `<eventMappings>`, `<providers>`ve `<rules>` bölümlerinden önceden tanımlanmış sistem durumu izleme yapılandırma bilgilerini silmek için `<clear />` öğeleri kullanır. Daha sonra bu bölümlerin her birine tek bir giriş ekler.

- `<eventMappings>` öğesi, işlenmemiş bir özel durum oluştuğunda oluşturulan "tüm hatalar" adlı İlgilendiğiniz tek bir sistem durumu izleme olayını tanımlar.
- `<providers>` öğesi, `SqlWebEventProvider` sınıfını kullanan "SqlWebEventProvider" adlı tek bir günlük kaynağını tanımlar. `connectionStringName` özniteliği, `<connectionStrings>` bölümünde tanımlanan bağlantı dizemizin adı olan "BelgeAdı" olarak ayarlanmıştır.
- Son olarak, &lt;Rules&gt; öğesi, "tüm hatalar" olayının "SqlWebEventProvider" sağlayıcısı kullanılarak günlüğe kaydedilecek şekilde olduğunu gösterir.

Bu yapılandırma bilgileri, sistem durumu izleme sisteminin işlenmemiş tüm özel durumları kitap Incelemeleri veritabanına kullanmasını söyler.

> [!NOTE]
> `WebBaseErrorEvent` olayı yalnızca sunucu hataları için oluşturulur; bulunamayan bir ASP.NET kaynağına yönelik istek gibi HTTP hataları için oluşturulmaz. Bu, hem sunucu hem de HTTP hataları için oluşturulan `HttpApplication` sınıfının `Error` olayının davranışından farklıdır.

Sistem durumu izleme sistemini çalışırken görmek için, Web sitesini ziyaret edin ve `Genre.aspx?ID=foo`ziyaret ederek bir çalışma zamanı hatası oluşturun. Uygun hata sayfasını görmeniz gerekir-özel durum ayrıntıları sarı ekran hatası (yerel olarak ziyaret edildiğinde) veya özel hata sayfası (üretimde siteyi ziyaret edildiğinde). Arka planda, sistem durumu izleme sistemi hata bilgilerini veritabanına kaydetti. `aspnet_WebEvent_Events` tabloda bir kayıt olmalıdır (bkz. **Şekil 1**); Bu kayıt, az önce oluşan çalışma zamanı hatası hakkında bilgiler içerir.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image1.png)

**Şekil 1**: hata ayrıntıları `aspnet_WebEvent_Events` tablosuna kaydedildi  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-asp-net-health-monitoring-cs/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>Hata günlüğünü bir Web sayfasında görüntüleme

Web sitesinin geçerli yapılandırmasıyla, sistem durumu izleme sistemi işlenmeyen tüm özel durumları veritabanına kaydeder. Ancak sistem durumu izleme, hata günlüğünü bir Web sayfası aracılığıyla görüntülemek için herhangi bir mekanizma sağlamaz. Ancak, bu bilgileri veritabanından görüntüleyen bir ASP.NET sayfası oluşturabilirsiniz. (Kısa bir sürede göreceğiniz gibi, bir e-posta iletisinde hata ayrıntılarının size gönderilmesini seçebilirsiniz.)

Böyle bir sayfa oluşturursanız, yalnızca yetkili kullanıcıların hata ayrıntılarını görüntülemesine izin vermek için gerekli adımları gerçekleştirdiğinizden emin olun. Siteniz zaten Kullanıcı hesapları kullanıyorsa, sayfaya erişimi belirli kullanıcı veya rollere kısıtlamak için URL yetkilendirme kurallarını kullanabilirsiniz. Oturum açmış olan kullanıcıya göre Web sayfalarına erişim verme veya erişimi kısıtlama hakkında daha fazla bilgi için, [Web sitesi güvenlik öğreticilerime](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)bakın.

> [!NOTE]
> Sonraki öğreticide, ELMAH adlı alternatif bir hata günlüğü ve bildirim sistemi incelenmektedir. ELMAH, hem bir Web sayfasından hem de RSS akışı olarak hata günlüğünü görüntülemek için yerleşik bir mekanizma içerir.

## <a name="logging-events-to-email"></a>Olayları e-postaya kaydetme

Sistem durumu izleme sistemi, bir olayı bir e-posta iletisine "günlüğe kaydeder" bir günlük kaynak sağlayıcısı içerir. Günlük kaynağı, e-posta iletisi gövdesinde veritabanına kaydedilen bilgileri içerir. Bu günlük kaynağını, belirli bir sistem durumu izleme olayı gerçekleştiğinde bir geliştiriciye bildirmek için kullanabilirsiniz.

Bir özel durum oluştuğunda bir e-posta aldığımızda, Book Incelemeleri Web sitesinin yapılandırmasını güncelleştirelim. Bunu gerçekleştirmek için üç görev gerçekleştirmeniz gerekir:

1. ASP.NET Web uygulamasını e-posta gönderecek şekilde yapılandırın. Bu, e-posta iletilerinin `<system.net>` yapılandırma öğesi aracılığıyla nasıl gönderileceğini belirterek gerçekleştirilir. Bir ASP.NET uygulamasında e-posta iletileri gönderme hakkında daha fazla bilgi için, [ASP.net 'de e-posta gönderme](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx) ve [sistem .net. Mail hakkında SSS](http://systemnetmail.com/)bölümüne bakın.
2. E-posta günlüğü kaynak sağlayıcısını `<providers>` öğesine kaydedin ve
3. "Tüm hatalar" olayını (2) adımında eklenen günlük kaynak sağlayıcısına eşleyen `<rules>` öğesine bir giriş ekleyin.

Sistem durumu izleme sistemi iki e-posta günlüğü kaynak sağlayıcısı sınıfı içerir: `SimpleMailWebEventProvider` ve `TemplatedMailWebEventProvider`. [`SimpleMailWebEventProvider` sınıfı](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx) , olay ayrıntılarını içeren bir düz metin e-posta iletisi gönderir ve e-posta gövdesinin küçük bir özelleştirmesini sağlar. [`TemplatedMailWebEventProvider` sınıfı](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) ile, e-posta iletisinin gövdesi olarak işlenen biçimlendirme kullanılan bir ASP.NET sayfası belirtirsiniz. [`TemplatedMailWebEventProvider` sınıfı](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) e-posta iletisinin içeriği ve biçimi üzerinde çok daha fazla denetim sağlar, ancak e-posta iletisinin gövdesini üreten ASP.NET sayfasını oluşturmanız gerektiği için biraz daha fazla çalışma gerektirir. Bu öğretici, `SimpleMailWebEventProvider` sınıfını kullanmaya odaklanır.

`Web.config` dosyadaki sistem durumu izleme sisteminin `<providers>` öğesini `SimpleMailWebEventProvider` sınıfına ait bir günlük kaynağı içerecek şekilde güncelleştirin:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample3.xml)]

Yukarıdaki biçimlendirme `SimpleMailWebEventProvider` sınıfını günlük kaynak sağlayıcısı olarak kullanır ve bunu "EmailWebEventProvider" kolay adına atar. Üstelik `<add>` özniteliği, e-posta iletisinin Kimden ve Kimden adresleri gibi ek yapılandırma seçeneklerini içerir.

E-posta günlük kaynağı tanımlandığına göre, sistem durumu izleme sisteminin işlenmemiş özel durumları "günlüğe kaydetmek" için bu kaynağı kullanmasını söylemek önemlidir. Bu, `<rules>` bölümüne yeni bir kural eklenerek gerçekleştirilir:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample4.xml)]

`<rules>` bölümü artık iki kural içerir. Birincisi, "e-postaya tüm hatalar" adlı tüm işlenmeyen özel durumları "EmailWebEventProvider" günlük kaynağına gönderir. Bu kural, Web sitesindeki hatalar hakkındaki ayrıntıları belirtilen adres için gönderme etkisine sahiptir. "Tüm hatalar veritabanı" kuralı, hata ayrıntılarını sitenin veritabanına kaydeder. Sonuç olarak, sitede işlenmeyen bir özel durum olduğunda, ayrıntıları veritabanına kaydedilir ve belirtilen e-posta adresine gönderilir.

**Şekil 2** `Genre.aspx?ID=foo`ziyaret edildiğinde `SimpleMailWebEventProvider` sınıfı tarafından oluşturulan e-postayı gösterir.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image4.png)

**Şekil 2**: hata ayrıntıları bir e-posta iletisinde gönderilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](logging-error-details-with-asp-net-health-monitoring-cs/_static/image6.png))

## <a name="summary"></a>Özet

ASP.NET sistem durumu izleme sistemi, yöneticilerin dağıtılan bir Web uygulamasının sistem durumunu izlemesine olanak tanımak üzere tasarlanmıştır. Sistem durumu izleme olayları, uygulamanın ne zaman durdurduğu, bir kullanıcı sitede başarıyla oturum açtığında ya da işlenmeyen bir özel durum oluştuğunda olduğu gibi bazı işlemler katında ortaya çıkar. Bu olaylar, herhangi bir sayıda günlük kaynağında günlüğe kaydedilebilir. Bu öğretici, işlenmemiş özel durumların ayrıntılarının bir veritabanına ve bir e-posta iletisiyle nasıl günlüğe alınacağını gösterdi.

Bu öğretici, işlenmemiş özel durumları günlüğe kaydetmek için sistem durumu izlemenin kullanılmasına odaklanır, ancak sistem durumu izlemenin dağıtılan bir ASP.NET uygulamasının genel durumunu ölçecek şekilde tasarlandığını ve çok fazla sistem durumu izleme olayı ve günlük kaynağı içerdiğini göz önünde bulundurun Burada araştırılabilir. Ne kadar çok, kendi sistem durumu izleme olaylarınızı ve günlük kaynaklarınızı oluşturmanız gerekir. Sistem durumu izleme hakkında daha fazla bilgi edinmek istiyorsanız, [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)'ın [SISTEM durumu izleme SSS](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)aracılığıyla okumanız iyi bir ilk adımdır. Bunun [Için nasıl yapılır: ASP.NET 2,0 'de sistem durumu Izlemeyi kullanma](https://msdn.microsoft.com/library/ms998306.aspx)konusuna bakın.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET durum Izlemeye genel bakış](https://msdn.microsoft.com/library/bb398933.aspx)
- [ASP.NET sistem durumu Izleme sistemini yapılandırma ve özelleştirme](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [SSS-ASP.NET 2,0 'de sistem durumu Izleme](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [Nasıl yapılır: sistem durumu Izleme bildirimleri için e-posta gönderme](https://msdn.microsoft.com/library/ms227553.aspx)
- [Nasıl yapılır: ASP.NET 'de sistem durumu Izlemeyi kullanma](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET 'de sistem durumu Izleme](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [Önceki](processing-unhandled-exceptions-cs.md)
> [İleri](logging-error-details-with-elmah-cs.md)
