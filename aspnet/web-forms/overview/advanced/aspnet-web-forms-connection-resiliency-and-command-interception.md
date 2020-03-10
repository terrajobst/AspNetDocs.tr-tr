---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web Forms bağlantı dayanıklılığı ve komut Yakalaşmayı | Microsoft Docs
author: Erikre
description: Bu öğreticide, bağlantı dayanıklılığı ve komut yakalaşmayı desteklemek için örnek bir uygulamanın nasıl değiştirileceği açıklanmaktadır.
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598429"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web Forms Bağlantı Dayanıklılığı ve Komut Durdurma

by [Erik Reitan](https://github.com/Erikre)

Bu öğreticide, bağlantı dayanıklılığı ve komut yakalaşmayı desteklemek için Wingtip Toys örnek uygulamasını değiştirirsiniz. Bağlantı dayanıklılığını etkinleştirerek, Wingtip Toys örnek uygulaması, bir bulut ortamının tipik bir şekilde oluşması durumunda veri çağrılarını otomatik olarak yeniden dener. Ayrıca, komut yakalayıcı uygulayarak, Wingtip Toys örnek uygulaması, veritabanına gönderilen tüm SQL sorgularını günlüğe kaydetmek veya değiştirmek için yakalar.

> [!NOTE] 
> 
> Bu Web Forms öğretici, Tom Dykstra 'in aşağıdaki MVC öğreticisine dayalıdır:  
> [ASP.NET MVC uygulamasındaki Entity Framework bağlantı dayanıklılığı ve komut Yakalaşmayı](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>Öğrenecekleriniz:

- Bağlantı dayanıklılığı sağlama.
- Komut yakalaşmayı uygulama.

## <a name="prerequisites"></a>Önkoşullar

Başlamadan önce, bilgisayarınızda aşağıdaki yazılımların yüklü olduğundan emin olun:

- Web için [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) veya [Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework otomatik olarak yüklenir.
- Wingtip Toys örnek projesi, bu öğreticide açıklanan işlevselliği Wingtip Toys projesi içinde uygulayabilmeniz için. Aşağıdaki bağlantı, indirme ayrıntılarını sağlar:

    - [ASP.NET 4.5.1 Web Forms Ile çalışmaya başlama-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- Bu öğreticiyi tamamlamadan önce, [ASP.NET 4,5 Web Forms ve Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)kullanmaya başlarken ilgili öğretici serisini gözden geçirmeyi düşünün. Öğretici serisi, **wingtiptoys** projesi ve kodu hakkında bilgi sahibi olmanıza yardımcı olur.

## <a name="connection-resiliency"></a>Bağlantı dayanıklılığı

Bir uygulamayı Microsoft Azure 'a dağıtmaya göz önünde bulundurmanız gereken tek bir seçenek, veritabanını bir bulut veritabanı hizmeti olan **Windows** **Azure SQL veritabanı**'na dağıtmaktan biridir. Bir bulut veritabanı hizmetine bağlandığınızda, Web sunucunuz ve veritabanı sunucunuz aynı veri merkezinde doğrudan birbirine bağlandığında, geçici bağlantı hataları genellikle daha sık kullanılır. Bulut Web sunucusu ve bulut veritabanı hizmeti aynı veri merkezinde barındırılıyorsa bile, aralarında yük dengeleyiciler gibi sorunları oluşabilecek daha fazla ağ bağlantısı vardır.

Ayrıca, bir bulut hizmeti genellikle diğer kullanıcılar tarafından paylaşılır ve bu da yanıt verme hızı bundan etkilenebilir. Ve veritabanına erişiminiz, azaltma ile ilgili olabilir. Daraltma, veritabanı hizmetinin *hizmet düzeyi sözleşmesi* (SLA) ' de izin verilenden daha sık erişmeye çalıştığınızda özel durumlar oluşturduğu anlamına gelir.

Bir bulut hizmetine erişirken oluşan birçok veya daha fazla bağlantı sorunu geçicidir, diğer bir deyişle, kendilerini kısa bir süre içinde çözer. Bu nedenle, bir veritabanı işlemi deneyip genellikle geçici olan bir hata türü alırsanız, kısa bir bekleme sonrasında işlemi yeniden deneyebilir ve işlem başarılı olabilir. Otomatik olarak yeniden deneyerek geçici hataları idare ediyorsanız kullanıcılarınız için çok daha iyi bir deneyim sağlayabilirsiniz ve bunların çoğunu müşterinin üzerinde görünmez hale getirebilirsiniz. Entity Framework 6 ' daki bağlantı dayanıklılığı özelliği, başarısız olan SQL sorgularını yeniden deneme sürecini otomatikleştirir.

Bağlantı dayanıklılığı özelliğinin belirli bir veritabanı hizmeti için uygun şekilde yapılandırılması gerekir:

1. Hangi özel durumların geçici olma olasılığı olduğunu bilmelidir. Örneğin, program hatalarının neden olduğu hataları değil, ağ bağlantısında geçici bir kayıp oluşmasına neden olan hataları yeniden denemek istiyorsunuz.
2. Başarısız bir işlemin yeniden denemeleri arasında uygun bir süre beklemek zorunda olur. Bir toplu işlem için yeniden denemeler arasında, kullanıcının yanıt beklediği bir çevrimiçi Web sayfası için daha uzun sürebilir.
3. Daha önce uygun sayıda yeniden denemek zorunda olur. Çevrimiçi bir uygulamada yaptığınız bir toplu işlemde daha fazla kez yeniden denemek isteyebilirsiniz.

Bu ayarları, bir Entity Framework sağlayıcısı tarafından desteklenen tüm veritabanı ortamları için el ile yapılandırabilirsiniz.

Bağlantı dayanıklılığı 'nı etkinleştirmek için yapmanız gereken, derlemenizin `DbConfiguration` sınıfından türetilen bir sınıf oluşturur ve bu sınıfta, Entity Framework yeniden deneme ilkesi için başka bir terim olan SQL veritabanı yürütme stratejisi ayarlanır.

### <a name="implementing-connection-resiliency"></a>Bağlantı dayanıklılığı uygulama

1. Visual Studio 'da [wingtiptoys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) örnek Web Forms uygulamasını indirip açın.
2. **Wingtiptoys** uygulamasının *Logic* klasöründe, *WingtipToysConfiguration.cs*adlı bir sınıf dosyası ekleyin.
3. Mevcut kodu şu kodla değiştirin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

Entity Framework, bulduğu kodu `DbConfiguration`türetilen bir sınıfta otomatik olarak çalıştırır. *Web. config* dosyasında istemediğiniz koddaki yapılandırma görevlerini yapmak için `DbConfiguration` sınıfını kullanabilirsiniz. Daha fazla bilgi için bkz. [EntityFramework kod tabanlı yapılandırma](https://msdn.microsoft.com/data/jj680699).

1. *Logic* klasöründe, *AddProducts.cs* dosyasını açın.
2. Sarı renkle gösterildiği gibi `System.Data.Entity.Infrastructure` için `using` bir ifade ekleyin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. `AddProduct` yöntemine `catch` bir blok ekleyerek `RetryLimitExceededException` sarı renkle vurgulanmış şekilde günlüğe kaydedilir:   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

`RetryLimitExceededException` özel durumu ekleyerek daha iyi günlüğe kaydetme sağlayabilir veya kullanıcıya işlemi yeniden denemeyi seçebilecekleri bir hata mesajı görüntüleyebilirsiniz. `RetryLimitExceededException` özel durumu yakalanarak geçici olması olası tek hatalar zaten denenir ve birkaç kez başarısız olur. Döndürülen gerçek özel durum `RetryLimitExceededException` özel durumuna Sarmalanacak. Ayrıca, genel bir catch bloğu da eklemiş olursunuz. `RetryLimitExceededException` özel durumu hakkında daha fazla bilgi için bkz. [Entity Framework bağlantı dayanıklılığı/yeniden deneme mantığı](https://msdn.microsoft.com/data/dn456835).

## <a name="command-interception"></a>Komut yakaalımı

Bir yeniden deneme ilkesi açtığınızdan, bunun beklendiği gibi çalıştığını doğrulamak için nasıl test edersiniz? Özellikle yerel olarak çalıştırdığınız sırada geçici bir hata oluşmasını zorlamak çok kolay olur ve gerçek geçici hataları otomatik bir birim testi olarak tümleştirmeniz özellikle zordur. Bağlantı dayanıklılığı özelliğini sınamak için, Entity Framework SQL Server gönderdiği sorguları ve genellikle geçici olan bir özel durum türü ile SQL Server yanıtını değiştirmek için bir yol gerekir.

Bulut uygulamaları için en iyi yöntemi uygulamak üzere sorgu yakalamanın de kullanabilirsiniz: veritabanı hizmetleri gibi dış hizmetlere yapılan tüm çağrıların gecikmesini ve başarısını günlüğe kaydedin.

Öğreticinin bu bölümünde, hem günlüğe kaydetme hem de geçici hataların benzetimini yapmak için Entity Framework [*ele geçirme özelliğini*](https://msdn.microsoft.com/data/dn469464) kullanacaksınız.

### <a name="create-a-logging-interface-and-class"></a>Günlüğe kaydetme arabirimi ve sınıfı oluşturma

Günlüğe kaydetme için en iyi yöntem, `System.Diagnostics.Trace` veya bir günlük sınıfına yapılan Sabit kodlama yerine bir [`interface`](https://msdn.microsoft.com/library/ms173156.aspx) kullanarak yapılır. Bu, daha sonra bunu yapmanız gerekiyorsa, daha sonra günlüğe kaydetme mekanizmanızı değiştirmeyi kolaylaştırır. Bu bölümde, günlük arabirimini ve bunu uygulamak için bir sınıf oluşturacaksınız.

Yukarıdaki yordama bağlı olarak, Visual Studio 'da **wingtiptoys** örnek uygulamasını indirmiş ve açtık.

1. **Wingtiptoys** projesinde bir klasör oluşturun ve *günlüğe kaydetmeyi*adlandırın.
2. *Günlüğe kaydetme* klasöründe *ILogger.cs* adlı bir sınıf dosyası oluşturun ve varsayılan kodu şu kodla değiştirin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   Arabirim, günlüklerin göreli önemini belirtmek için üç izleme düzeyi sağlar ve bir diğeri de veritabanı sorguları gibi dış hizmet çağrıları için gecikme bilgilerini sağlamak üzere tasarlanmıştır. Günlüğe kaydetme yöntemlerinin bir özel durum iletmenizi sağlayan aşırı yüklemeleri vardır. Bu, yığın izleme ve iç özel durumlar dahil olmak üzere özel durum bilgilerinin, uygulama genelinde her günlük yöntemi çağrısında yapılmak yerine, arabirimini uygulayan sınıf tarafından güvenilir bir şekilde günlüğe kaydedilmesini sağlar.  
  
   `TraceApi` yöntemleri, SQL veritabanı gibi bir dış hizmete yapılan her çağrının gecikmesini izlemenize olanak sağlar.
3. *Günlüğe kaydetme* klasöründe *Logger.cs* adlı bir sınıf dosyası oluşturun ve varsayılan kodu şu kodla değiştirin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

Uygulama, izlemeyi yapmak için `System.Diagnostics` kullanır. Bu, izleme bilgilerini oluşturmayı ve kullanmayı kolaylaştıran .NET 'in yerleşik bir özelliğidir. `System.Diagnostics` izleme ile kullanabileceğiniz birçok &quot;dinleyicisi vardır&quot;, dosyaları dosyalara yazmak, örneğin veya Windows Azure 'da blob depolamaya yazmak için. [Visual Studio 'Da Microsoft Azure Web siteleri sorunlarını giderme](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)konusunda daha fazla bilgi için bazı seçeneklere ve diğer kaynakların bağlantılarına bakın. Bu öğreticide, günlüklere yalnızca Visual Studio **çıktı** penceresinde bakacaksınız.

Bir üretim uygulamasında, `System.Diagnostics`dışındaki izleme çerçevelerini kullanmayı düşünebilirsiniz ve `ILogger` arabirimi bunu yapmayı seçerseniz, farklı bir izleme mekanizmasına geçiş yapmayı nispeten daha kolay hale getirir.

### <a name="create-interceptor-classes"></a>Yakalayıcısı sınıfları oluşturma

Daha sonra, bir sorgu veritabanına her gönderilirken, biri geçici hataların benzetimini yapmak ve bir günlüğe kaydetmek için Entity Framework sınıfların her seferinde arayacaktır. Bu yakalayıcısı sınıfları `DbCommandInterceptor` sınıfından türetilmelidir. Bunlar içinde, sorgu yürütülene kadar otomatik olarak çağrılan yöntem geçersiz kılmaları yazarsınız. Bu yöntemlerde veritabanına gönderilen sorguyu inceleyebilir veya günlüğe kaydedebilir ve sorguyu veritabanına geçirmeden bile veritabanını veritabanına gönderilmeden önce değiştirebilir veya Entity Framework kendinize geri dönebilme sağlayabilirsiniz.

1. Veritabanına gönderilmeden önce her SQL sorgusunu günlüğe kaydedilecek bir kod dosyası oluşturmak için, *Logic* klasöründe *InterceptorLogging.cs* adlı bir sınıf dosyası oluşturun ve varsayılan kodu aşağıdaki kodla değiştirin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   Başarılı sorgular veya komutlar için bu kod, gecikme bilgilerine sahip bir bilgi günlüğü yazar. Özel durumlar için bir hata günlüğü oluşturur.
2. *Adminpage. aspx*adlı sayfada **ad** metin kutusuna &quot;throw&quot; girerken, hata oluştur ' u oluşturmak için, *Logic* klasöründe *InterceptorTransientErrors.cs* adlı bir sınıf dosyası oluşturun ve varsayılan kodu aşağıdaki kodla değiştirin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    Bu kod yalnızca birden fazla veri satırı döndürebilen sorgular için çağrılan `ReaderExecuting` yöntemini geçersiz kılar. Diğer sorgu türleri için bağlantı dayanıklılığını denetlemek isterseniz, günlük kaydı yakalayıcısı sırasında `NonQueryExecuting` ve `ScalarExecuting` yöntemleri de geçersiz kılabilirsiniz.  
  
   Daha sonra, "Yönetici" olarak oturum açacak ve üst gezinti çubuğunda **yönetici** bağlantısını seçersiniz. Ardından, *adminpage. aspx* sayfasında, &quot;throw&quot;adlı bir ürün ekleyeceksiniz. Kod, genellikle geçici olarak bilinen bir tür olan 20 hata numarası için bir kukla SQL veritabanı özel durumu oluşturur. Şu anda geçici olarak tanınan diğer hata numaraları 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 ve 40613 ' dir, ancak bunlar SQL veritabanı 'nın yeni sürümlerindeki değişikliğe tabidir. Ürün, *InterceptorTransientErrors.cs* dosyasının kodunda izleyebilmeniz Için "geçişli Enterrorexbol" olarak yeniden adlandırılacaktır.  
  
   Kod, sorguyu çalıştırmak ve sonuçları geri geçirmek yerine Entity Framework özel durumu döndürür. Geçici durum *dört* kez döndürülür ve sonra kod, sorguyu veritabanına geçirmenin normal yordamına geri döner.

    Her şey günlüğe kaydedildiği için Entity Framework, son başarılı olmadan önce sorguyu dört kez yürütmeye çalıştığını ve uygulamadaki tek fark, sorgu sonuçlarıyla bir sayfanın işlenmesine daha uzun sürmelecektir.  
  
   Entity Framework kaç kez yeniden deneneceğini yapılandırılabilir; kod, SQL veritabanı yürütme ilkesi için varsayılan değer olan dört kez belirtilir. Yürütme ilkesini değiştirirseniz, geçici hataların kaç kez oluşturulduğunu belirten kodu burada da değiştirirsiniz. Ayrıca, Entity Framework `RetryLimitExceededException` özel durumu oluşturması için daha fazla özel durum oluşturmak üzere kodu değiştirebilirsiniz.
3. *Global. asax*dosyasında aşağıdaki using deyimlerini ekleyin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. Ardından, vurgulanan satırları `Application_Start` yöntemine ekleyin:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

Bu kod satırları, Entity Framework sorguları veritabanına gönderdiğinde, yakacının kodun çalışmasına neden olur. Geçici hata benzetimi ve günlüğe kaydetme için ayrı yakalayıcısı sınıfları oluşturduğunuza göre, bunları bağımsız olarak etkinleştirip devre dışı bırakabildiğinize dikkat edin.   
  
 Kodlarınızın herhangi bir yerinden `DbInterception.Add` yöntemini kullanarak yakalayıcılar ekleyebilirsiniz; `Application_Start` yönteminde olması gerekmez. Başka bir seçenek de `Application_Start` yöntemine yakalayıcılar eklemediğiniz takdirde, *WingtipToysConfiguration.cs* adlı sınıfı güncellemek veya eklemek ve `WingtipToysConfiguration` sınıfının oluşturucusunun sonuna yukarıdaki kodu koymak olacaktır.

Bu kodu yerleştirdiğiniz her yerde, aynı dinleyici için `DbInterception.Add` birden çok kez yürütmemeye dikkat edin ya da ek dinleyici örnekleri alırsınız. Örneğin, günlüğe kaydetme yakalayıcısını iki kez eklerseniz, her SQL sorgusu için iki günlük görürsünüz.

Yakalayıcılar kayıt sırasında (`DbInterception.Add` yönteminin çağrıldığı sıra) yürütülür. Sipariş, yakalayıcıyı ne yaptığınıza bağlı olarak değişebilir. Örneğin, bir dinleyici, `CommandText` özelliğinde aldığı SQL komutunu değiştirebilir. SQL komutunu değiştirmezse, sonraki dinleyici özgün SQL komutuna değil değiştirilmiş SQL komutunu alır.

Geçici hata benzetim kodunu, Kullanıcı arabirimine farklı bir değer girerek geçici hatalara neden olmanızı sağlayan bir şekilde yazmış oldunuz. Alternatif olarak, belirli bir parametre değerini denetlemeden geçici özel durumların sırasını her zaman oluşturmak için yakalayıcısı kodunu yazabilirsiniz. Daha sonra, yalnızca geçici hatalar oluşturmak istediğinizde, yakalayıcıyı ekleyebilirsiniz. Ancak bunu yaparsanız, veritabanının başlatılması tamamlanana kadar yakalayıcıyı eklemeyin. Diğer bir deyişle, geçici hatalar oluşturmaya başlamadan önce varlık kümelerinizin birinde sorgu gibi en az bir veritabanı işlemi yapın. Entity Framework, veritabanı başlatma sırasında birkaç sorgu yürütür ve bir işlem içinde yürütülmemişse, başlatma sırasında oluşan hatalar bağlamın tutarsız bir duruma gelmesine neden olabilir.

## <a name="test-logging-and-connection-resiliency"></a>Test günlüğü ve bağlantı dayanıklılığı

1. Visual Studio 'da **F5** ' e basarak uygulamayı hata ayıklama modunda çalıştırın ve ardından parola olarak "Pa $ $Word" kullanarak "Yönetici" olarak oturum açın.
2. Üstteki gezinti çubuğundan **yönetici** ' yi seçin.
3. Uygun açıklama, Fiyat ve resim dosyası ile "Throw" adlı yeni bir ürün girin.
4. **Ürün Ekle** düğmesine basın.  
   Entity Framework sorguyu birkaç kez yeniden denenirken tarayıcının birkaç saniye boyunca askıda olduğunu fark edeceksiniz. İlk yeniden deneme çok hızlı gerçekleşir, ardından her ek yeniden denemeden önce bekleme artar. Her yeniden denemeden önce daha uzun süre bekleme işlemi *üstel geri* alma çağırılacaktır.
5. Sayfa artık yüklenmeye denenene kadar bekleyin.
6. Projeyi durdurun ve izleme çıktısını görmek için Visual Studio **çıktı** penceresine bakın. **Çıkış** penceresini, **hata ayıkla** -&gt; **Windows** -&gt; **çıktısını**seçerek bulabilirsiniz. Günlükçüizin tarafından yazılan diğer birkaç günlüğü kaydırarak ilerleyebilmeniz gerekebilir.  
  
   Veritabanına gönderilen gerçek SQL sorgularını görebildiğine dikkat edin. Kullanmaya başlamak için Entity Framework ilk sorgu ve komutları görürsünüz, veritabanı sürümü ve geçiş geçmişi tablosu denetleniyor.   
    ![Çıktı Penceresi](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   Uygulamayı durdurmadığınız ve yeniden başlatana kadar bu testi yineleyemiyorum. Uygulamanın tek bir çalıştırmasında bağlantı dayanıklılığını birden çok kez test etmek isterseniz, `InterceptorTransientErrors` hata sayacını sıfırlamak için kod yazabilirsiniz.
7. Yürütme stratejisinin (yeniden deneme ilkesi) yaptığı farkı görmek için, *mantıksal* klasördeki *WingtipToysConfiguration.cs* dosyasında `SetExecutionStrategy` satırı açıklama olarak ayıklayın, **yönetici** sayfasını hata ayıklama modunda yeniden çalıştırın ve &quot;throw&quot; adlı ürünü yeniden ekleyin.  
  
   Bu kez, hata ayıklayıcı ilk oluşturulan özel durum üzerinde sorguyu ilk kez yürütmeyi denediğinde hemen duraklar.  
    ![Hata ayıklama-ayrıntıları görüntüle](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. *WingtipToysConfiguration.cs* dosyasındaki `SetExecutionStrategy` satırının açıklamasını kaldırın.

## <a name="summary"></a>Özet

Bu öğreticide bağlantı dayanıklılığı ve komut yakalaşmayı desteklemek için Web Forms örnek bir uygulamayı nasıl değiştireceğiniz gördünüz.

## <a name="next-steps"></a>Sonraki Adımlar

ASP.NET Web Forms bağlantı dayanıklılığı ve komut yakalaşmayı inceledikten sonra, [ASP.NET 4,5 ' deki zaman uyumsuz yöntemler](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)ASP.NET Web Forms konusunu gözden geçirin. Konu başlığı altında, Visual Studio kullanarak zaman uyumsuz ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgiler verilir.
