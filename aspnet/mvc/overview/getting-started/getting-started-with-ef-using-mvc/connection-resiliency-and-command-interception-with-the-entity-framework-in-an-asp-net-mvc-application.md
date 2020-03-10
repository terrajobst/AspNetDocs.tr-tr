---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasında EF ile bağlantı dayanıklılığı ve komut yakalaşmayı kullanın'
author: tdykstra
description: Bu öğreticide bağlantı dayanıklılığı ve komut yakalaşmayı kullanmayı öğreneceksiniz. Entity Framework 6 ' nın iki önemli özelliği vardır.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583456"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>Öğretici: bir ASP.NET MVC uygulamasında Entity Framework ile bağlantı dayanıklılığı ve komut yakalaşmayı kullanma

Şimdiye kadar uygulama, geliştirme bilgisayarınızda IIS Express yerel olarak çalışıyor. Gerçek bir uygulamayı diğer kişilerin Internet üzerinden kullanmasına olanak sağlamak için, bir Web barındırma sağlayıcısına dağıtmanız ve veritabanını bir veritabanı sunucusuna dağıtmanız gerekir.

Bu öğreticide bağlantı dayanıklılığı ve komut yakalaşmayı kullanmayı öğreneceksiniz. Bunlar, bulut ortamına dağıtım yaparken özellikle değerli olan Entity Framework 6 ' nın iki önemli özellikleridir: bağlantı dayanıklılığı (geçici hatalar için otomatik yeniden denemeler) ve komut yakalama (veritabanına gönderilen tüm SQL sorgularını yakala günlüğe kaydetmek veya değiştirmek için).

Bu bağlantı dayanıklılığı ve komut ele geçirme öğreticisi isteğe bağlıdır. Bu öğreticiyi atlarsanız, sonraki öğreticilerde bazı küçük ayarlamaların yapılması gerekir.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Bağlantı dayanıklılığı 'nı etkinleştir
> * Komut yakalaşmayı etkinleştir
> * Yeni yapılandırmayı test etme

## <a name="prerequisites"></a>Önkoşullar

* [Sıralama, Filtreleme ve Sayfalama](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>Bağlantı dayanıklılığı 'nı etkinleştir

Windows Azure 'a uygulamayı dağıttığınızda veritabanını bir bulut veritabanı hizmeti olan Windows Azure SQL veritabanı 'na dağıtırsınız. Bir bulut veritabanı hizmetine bağlandığınızda, Web sunucunuz ve veritabanı sunucunuz aynı veri merkezinde doğrudan birbirine bağlandığında, geçici bağlantı hataları genellikle daha sık kullanılır. Bulut Web sunucusu ve bulut veritabanı hizmeti aynı veri merkezinde barındırılıyorsa bile, aralarında yük dengeleyiciler gibi sorunları oluşabilecek daha fazla ağ bağlantısı vardır.

Ayrıca, bir bulut hizmeti genellikle diğer kullanıcılar tarafından paylaşılır ve bu da yanıt verme hızı bundan etkilenebilir. Ve veritabanına erişiminiz, azaltma ile ilgili olabilir. Daraltma, veritabanı hizmetinin Hizmet Düzeyi Sözleşmesi (SLA) ' de izin verilenden daha sık erişmeye çalıştığınızda özel durumlar oluşturduğu anlamına gelir.

Bir bulut hizmetine erişirken bir çok veya en çok bağlantı sorunu geçicidir, diğer bir deyişle, kendilerini kısa bir süre içinde çözer. Bu nedenle, bir veritabanı işlemi deneyip genellikle geçici olan bir hata türü alırsanız, kısa bir bekleme sonrasında işlemi yeniden deneyebilir ve işlem başarılı olabilir. Otomatik olarak yeniden deneyerek geçici hataları idare ediyorsanız kullanıcılarınız için çok daha iyi bir deneyim sağlayabilirsiniz ve bunların çoğunu müşterinin üzerinde görünmez hale getirebilirsiniz. Entity Framework 6 ' daki bağlantı dayanıklılığı özelliği, başarısız olan SQL sorgularını yeniden deneme sürecini otomatikleştirir.

Bağlantı dayanıklılığı özelliğinin belirli bir veritabanı hizmeti için uygun şekilde yapılandırılması gerekir:

- Hangi özel durumların geçici olma olasılığı olduğunu bilmelidir. Örneğin, program hatalarının neden olduğu hataları değil, ağ bağlantısında geçici bir kayıp oluşmasına neden olan hataları yeniden denemek istiyorsunuz.
- Başarısız bir işlemin yeniden denemeleri arasında uygun bir süre beklemek zorunda olur. Bir toplu işlem için yeniden denemeler arasında, kullanıcının yanıt beklediği bir çevrimiçi Web sayfası için daha uzun sürebilir.
- Daha önce uygun sayıda yeniden denemek zorunda olur. Çevrimiçi bir uygulamada yaptığınız bir toplu işlemde daha fazla kez yeniden denemek isteyebilirsiniz.

Bu ayarları bir Entity Framework sağlayıcısı tarafından desteklenen herhangi bir veritabanı ortamı için el ile yapılandırabilirsiniz, ancak genellikle Windows Azure SQL veritabanı 'nı kullanan bir çevrimiçi uygulama için iyi çalışan varsayılan değerler sizin için zaten yapılandırılmıştır ve Bunlar, Contoso Üniversitesi uygulaması için uyguladığınız ayarlardır.

Bağlantı dayanıklılığı 'nı etkinleştirmek için yapmanız gereken, derlemenizin [DBConfiguration](https://msdn.microsoft.com/data/jj680699.aspx) sınıfından türetilen bir sınıf oluşturur ve bu SıNıFTA, EF içinde, *yeniden deneme ilkesi*için başka bir terim olan SQL veritabanı *yürütme stratejisi*ayarlanır.

1. DAL klasöründe, *SchoolConfiguration.cs*adlı bir sınıf dosyası ekleyin.
2. Şablon kodunu aşağıdaki kodla değiştirin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Entity Framework, bulduğu kodu `DbConfiguration`türetilen bir sınıfta otomatik olarak çalıştırır. *Web. config* dosyasında istemediğiniz koddaki yapılandırma görevlerini yapmak için `DbConfiguration` sınıfını kullanabilirsiniz. Daha fazla bilgi için bkz. [EntityFramework kod tabanlı yapılandırma](https://msdn.microsoft.com/data/jj680699).
3. *StudentController.cs*' de, `System.Data.Entity.Infrastructure`için `using` bir ifade ekleyin.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. Onun yerine `RetryLimitExceededException` özel durumları yakalayabilmeleri için, `DataException` özel durumlarını yakalayacak tüm `catch` bloklarını değiştirin. Örneğin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    Kolay bir "yeniden dene" iletisi vermek için geçici olabilecek hataları belirlemeyi denemek üzere `DataException` kullanıyorsunuz. Ancak artık bir yeniden deneme ilkesi açtığınızdan, geçici olma olasılığı olan tek hatalar zaten denenir ve birkaç kez başarısız olur ve döndürülen gerçek özel durum `RetryLimitExceededException` özel durumuna kaydırılır.

Daha fazla bilgi için bkz. [Entity Framework bağlantı dayanıklılığı/yeniden deneme mantığı](https://msdn.microsoft.com/data/dn456835).

## <a name="enable-command-interception"></a>Komut yakalaşmayı etkinleştir

Bir yeniden deneme ilkesi açtığınızdan, bunun beklendiği gibi çalıştığını doğrulamak için nasıl test edersiniz? Özellikle yerel olarak çalıştırdığınız sırada geçici bir hata oluşmasını zorlamak çok kolay olur ve gerçek geçici hataları otomatik bir birim testi olarak tümleştirmeniz özellikle zordur. Bağlantı dayanıklılığı özelliğini sınamak için, Entity Framework SQL Server gönderdiği sorguları ve genellikle geçici olan bir özel durum türü ile SQL Server yanıtını değiştirmek için bir yol gerekir.

Bulut uygulamaları için en iyi yöntemi uygulamak üzere sorgu yakalamanın de kullanabilirsiniz: veritabanı hizmetleri gibi [dış hizmetlere yapılan tüm çağrıların gecikmesini ve başarısını günlüğe kaydedin](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) . EF6, günlüğü daha kolay hale getirmek için bir [adanmış günlüğe kaydetme API 'si](https://msdn.microsoft.com/data/dn469464) sağlar, ancak öğreticinin bu bölümünde, hem günlüğe kaydetme hem de geçici hataların benzetimini yapmak için Entity Framework [ele geçirme özelliğini](https://msdn.microsoft.com/data/dn469464) nasıl kullanacağınızı öğreneceksiniz.

### <a name="create-a-logging-interface-and-class"></a>Günlüğe kaydetme arabirimi ve sınıfı oluşturma

[Günlüğe kaydetme için en iyi yöntem](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) , System. Diagnostics. Trace 'e veya bir günlük sınıfına yapılan Sabit kodlama yerine bir arabirim kullanarak bunu gerçekleştirmelidir. Bu, daha sonra bunu yapmanız gerekiyorsa, daha sonra günlüğe kaydetme mekanizmanızı değiştirmeyi kolaylaştırır. Bu bölümde, günlük arabirimini ve bunu uygulamak için bir sınıf oluşturacaksınız./p >

1. Projede bir klasör oluşturun ve *günlüğe kaydetme*adını yazın.
2. *Günlüğe kaydetme* klasöründe *ILogger.cs*adlı bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    Arabirim, günlüklerin göreli önemini belirtmek için üç izleme düzeyi sağlar ve bir diğeri de veritabanı sorguları gibi dış hizmet çağrıları için gecikme bilgilerini sağlamak üzere tasarlanmıştır. Günlüğe kaydetme yöntemlerinin bir özel durum iletmenizi sağlayan aşırı yüklemeleri vardır. Bu, yığın izleme ve iç özel durumlar dahil olmak üzere özel durum bilgilerinin, uygulama genelinde her günlük yöntemi çağrısında yapılmak yerine, arabirimini uygulayan sınıf tarafından güvenilir bir şekilde günlüğe kaydedilmesini sağlar.

    Traceapı yöntemleri, SQL veritabanı gibi bir dış hizmete yapılan her çağrının gecikmesini izlemenize olanak sağlar.
3. *Günlüğe kaydetme* klasöründe *Logger.cs*adlı bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    Uygulama, izlemeyi yapmak için System. Diagnostics 'i kullanır. Bu, izleme bilgilerini oluşturmayı ve kullanmayı kolaylaştıran .NET 'in yerleşik bir özelliğidir. Dosyaları dosyalara yazmak, örneğin veya Azure 'daki blob depolamaya yazmak için System. Diagnostics izleme ile kullanabileceğiniz birçok "dinleyici" vardır. [Visual Studio 'Da Azure Web siteleri sorunlarını giderme](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)konusunda daha fazla bilgi için bazı seçeneklere ve diğer kaynakların bağlantılarına bakın. Bu öğreticide yalnızca Visual Studio **çıktı** penceresinde günlüklere bakacaksınız.

    Bir üretim uygulamasında System. Diagnostics dışındaki paketleri izlemeyi düşünebilirsiniz ve ILogger arabirimi, bunu yapmayı seçerseniz, farklı bir izleme mekanizmasına daha kolay geçiş yapmayı tercih edebilir.

### <a name="create-interceptor-classes"></a>Yakalayıcısı sınıfları oluşturma

Daha sonra, bir sorgu veritabanına her gönderilirken, biri geçici hataların benzetimini yapmak ve bir günlüğe kaydetmek için bir sorgu göndermek üzere Entity Framework sınıfları oluşturacaksınız. Bu yakalayıcısı sınıfları `DbCommandInterceptor` sınıfından türetilmelidir. Bunlar içinde, sorgu yürütülene kadar otomatik olarak çağrılan yöntem geçersiz kılmaları yazarsınız. Bu yöntemlerde veritabanına gönderilen sorguyu inceleyebilir veya günlüğe kaydedebilir ve sorguyu veritabanına geçirmeden bile veritabanını veritabanına gönderilmeden önce değiştirebilir veya Entity Framework kendinize geri dönebilme sağlayabilirsiniz.

1. Veritabanına gönderilen her SQL sorgusunu günlüğe alacak olan yakalayıcıyı sınıfını oluşturmak için, *dal* klasöründe *SchoolInterceptorLogging.cs* adlı bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    Başarılı sorgular veya komutlar için bu kod, gecikme bilgilerine sahip bir bilgi günlüğü yazar. Özel durumlar için bir hata günlüğü oluşturur.
2. **Arama** kutusuna "Throw" girerken işlevsiz geçici hatalar üreten bir şifre veren sınıfı oluşturmak Için, *dal* klasöründe *SchoolInterceptorTransientErrors.cs* adlı bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    Bu kod yalnızca birden fazla veri satırı döndürebilen sorgular için çağrılan `ReaderExecuting` yöntemini geçersiz kılar. Diğer sorgu türleri için bağlantı dayanıklılığını denetlemek isterseniz, günlük kaydı yakalayıcısı sırasında `NonQueryExecuting` ve `ScalarExecuting` yöntemleri de geçersiz kılabilirsiniz.

    Öğrenci sayfasını çalıştırdığınızda ve arama dizesi olarak "Throw" girdiğinizde bu kod, genellikle geçici olarak bilinen bir tür olan 20 hata numarası için bir kukla SQL veritabanı özel durumu oluşturur. Şu anda geçici olarak tanınan diğer hata numaraları 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 ve 40613 ' dir, ancak bunlar SQL veritabanı 'nın yeni sürümlerindeki değişikliğe tabidir.

    Kod, sorguyu çalıştırmak ve sorgu sonuçlarını geri geçirmek yerine Entity Framework özel durumu döndürür. Geçici durum dört kez döndürülür ve sonra kod, sorguyu veritabanına geçirmenin normal yordamına geri döner.

    Her şey günlüğe kaydedildiği için Entity Framework, son başarılı olmadan önce sorguyu dört kez yürütmeye çalıştığını ve uygulamadaki tek fark, sorgu sonuçlarıyla bir sayfanın işlenmesine daha uzun sürmelecektir.

    Entity Framework kaç kez yeniden deneneceğini yapılandırılabilir; kod, SQL veritabanı yürütme ilkesi için varsayılan değer olan dört kez belirtilir. Yürütme ilkesini değiştirirseniz, geçici hataların kaç kez oluşturulduğunu belirten kodu burada da değiştirirsiniz. Ayrıca, Entity Framework `RetryLimitExceededException` özel durumu oluşturması için daha fazla özel durum oluşturmak üzere kodu değiştirebilirsiniz.

    Arama kutusuna girdiğiniz değer `command.Parameters[0]` ve `command.Parameters[1]` (biri ad ve soyadı için kullanılır) olacaktır. "% Throw%" değeri bulunursa, bazı öğrencilerin bulunması ve döndürülmesi için bu parametrelerde "Throw" değiştirilmiştir.

    Bu, uygulama kullanıcı arabirimine bazı girişlerin değiştirilmesine göre bağlantı dayanıklılığı test etmenin kolay bir yoludur. Ayrıca, daha sonra *Dbyakacu. Add* yöntemi hakkındaki açıklamalarda açıklandığı gibi tüm sorgular veya güncelleştirmeler için geçici hatalar üreten bir kod yazabilirsiniz.
3. *Global. asax*dosyasında aşağıdaki `using` deyimlerini ekleyin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. Vurgulanan satırları `Application_Start` yöntemine ekleyin:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    Bu kod satırları, Entity Framework sorguları veritabanına gönderdiğinde, yakacının kodun çalışmasına neden olur. Geçici hata benzetimi ve günlüğe kaydetme için ayrı yakalayıcısı sınıfları oluşturduğunuza göre, bunları bağımsız olarak etkinleştirip devre dışı bırakabildiğinize dikkat edin.

    Kodlarınızın herhangi bir yerinden `DbInterception.Add` yöntemini kullanarak yakalayıcılar ekleyebilirsiniz; `Application_Start` yönteminde olması gerekmez. Diğer bir seçenek de, yürütme ilkesini yapılandırmak için daha önce oluşturduğunuz DbConfiguration sınıfına bu kodu koymaktır.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    Bu kodu yerleştirdiğiniz her yerde, aynı dinleyici için `DbInterception.Add` birden çok kez yürütmemeye dikkat edin ya da ek dinleyici örnekleri alırsınız. Örneğin, günlüğe kaydetme yakalayıcısını iki kez eklerseniz, her SQL sorgusu için iki günlük görürsünüz.

    Yakalayıcılar kayıt sırasında (`DbInterception.Add` yönteminin çağrıldığı sıra) yürütülür. Sipariş, yakalayıcıyı ne yaptığınıza bağlı olarak değişebilir. Örneğin, bir dinleyici, `CommandText` özelliğinde aldığı SQL komutunu değiştirebilir. SQL komutunu değiştirmezse, sonraki dinleyici özgün SQL komutuna değil değiştirilmiş SQL komutunu alır.

    Geçici hata benzetim kodunu, Kullanıcı arabirimine farklı bir değer girerek geçici hatalara neden olmanızı sağlayan bir şekilde yazmış oldunuz. Alternatif olarak, belirli bir parametre değerini denetlemeden geçici özel durumların sırasını her zaman oluşturmak için yakalayıcısı kodunu yazabilirsiniz. Daha sonra, yalnızca geçici hatalar oluşturmak istediğinizde, yakalayıcıyı ekleyebilirsiniz. Ancak bunu yaparsanız, veritabanının başlatılması tamamlanana kadar yakalayıcıyı eklemeyin. Diğer bir deyişle, geçici hatalar oluşturmaya başlamadan önce varlık kümelerinizin birinde sorgu gibi en az bir veritabanı işlemi yapın. Entity Framework, veritabanı başlatma sırasında birkaç sorgu yürütür ve bir işlem içinde yürütülmemişse, başlatma sırasında oluşan hatalar bağlamın tutarsız bir duruma gelmesine neden olabilir.

## <a name="test-the-new-configuration"></a>Yeni yapılandırmayı test etme

1. **F5** tuşuna basarak uygulamayı hata ayıklama modunda çalıştırın ve ardından **öğrenciler** sekmesine tıklayın.
2. İzleme çıktısını görmek için Visual Studio **çıktı** penceresine bakın. Günlükçüizin tarafından yazılan günlüklere ulaşmak için bazı JavaScript hatalarının ölçeğini kaydırarak ilerleyemeyebilirsiniz.

    Veritabanına gönderilen gerçek SQL sorgularını görebildiğine dikkat edin. Kullanmaya başlamak için Entity Framework ilk sorgu ve komutları görürsünüz, veritabanı sürümü ve geçiş geçmişi tablosu denetleniyor (sonraki öğreticide geçişler hakkında bilgi edineceksiniz). Ayrıca, kaç öğrencinin olduğunu öğrenmek için disk belleği sorgusu, son olarak da öğrenci verilerini alan sorguyu görürsünüz.

    ![Normal sorgu için günlüğe kaydetme](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. **Öğrenciler** sayfasında, arama dizesi olarak "Throw" yazın ve **Ara**' ya tıklayın.

    ![Throw arama dizesi](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Entity Framework sorguyu birkaç kez yeniden denenirken tarayıcının birkaç saniye boyunca askıda olduğunu fark edeceksiniz. İlk yeniden deneme çok hızlı gerçekleşir ve sonra her ek yeniden denemeden önce beklenecek kadar bekler. Her yeniden denemeden önce daha uzun süre bekleme işlemi *üstel geri*alma çağırılacaktır.

    Sayfa görüntülendiğinde, adlarında "bir" olan öğrencileri gösteren çıktı penceresine bakın ve aynı sorgunun beş kez denendiğini, ilk dört kez geçici durum döndürdüğünü görürsünüz. Her geçici hata için, `SchoolInterceptorTransientErrors` sınıfında geçici hatayı oluştururken yazdığınız günlüğü görürsünüz ("komut için geçici hata döndürülüyor...") ve `SchoolInterceptorLogging` özel durumu aldığında yazılan günlüğü görürsünüz.

    ![Yeniden denemeleri gösteren çıktıyı günlüğe kaydetme](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    Bir arama dizesi girdiğinizden, öğrenci verileri döndüren sorgu parametreleştirilemiştir:

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    Parametrelerin değerini günlüğe kaydedemedi, ancak bunu yapabilirsiniz. Parametre değerlerini görmek isterseniz, bir günlük kodu yazmak için, bu yöntem içinde aldığınız `DbCommand` nesnesinin `Parameters` özelliğinden parametre değerlerini alabilirsiniz.

    Uygulamayı durdurmadığınız ve yeniden başlatana kadar bu testi yineleyemiyorum. Uygulamanın tek bir çalıştırmasında bağlantı dayanıklılığını birden çok kez test etmek isterseniz, `SchoolInterceptorTransientErrors`hata sayacını sıfırlamak için kod yazabilirsiniz.
4. Yürütme stratejisinin (yeniden deneme ilkesi) yaptığı farkı görmek için, *SchoolConfiguration.cs*'deki `SetExecutionStrategy` satırı açıklama olarak ayıklayın, öğrenciler sayfasını hata ayıklama modunda yeniden çalıştırın ve "Throw" ifadesini yeniden aratın.

    Bu kez, hata ayıklayıcı ilk oluşturulan özel durum üzerinde sorguyu ilk kez yürütmeyi denediğinde hemen duraklar.

    ![Kukla özel durum](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. *SchoolConfiguration.cs*Içinde *Setexecutionstrateji* hattının açıklamasını kaldırın.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)bölümünde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Etkin bağlantı dayanıklılığı
> * Komut yakalaşmayı etkin
> * Yeni yapılandırma test edildi

Code First geçişleri ve Azure dağıtımı hakkında bilgi edinmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Code First geçişleri ve Azure dağıtımı](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
