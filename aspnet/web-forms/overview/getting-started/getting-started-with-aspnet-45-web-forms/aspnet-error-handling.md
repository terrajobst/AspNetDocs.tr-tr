---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET hata Işleme | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: f420be369801208fa875d9a60e6e154afbe84aa7
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995316"
---
# <a name="aspnet-error-handling"></a>ASP.NET Hata İşleme

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, Wingtip Toys örnek uygulamasını hata işleme ve hata günlüğünü içerecek şekilde değiştirirsiniz. Hata işleme, uygulamanın hataları düzgün bir şekilde işlemesini ve hata iletilerini uygun şekilde görüntülemesini sağlar. Hata günlüğü, oluşan hataları bulup düzeltmenize izin verir. Bu öğreticide, önceki öğreticide "URL yönlendirme" oluşturulur ve Wingtip Toys öğretici serisinin bir parçasıdır.

## <a name="what-youll-learn"></a>Şunları öğreneceksiniz:

- Uygulamanın yapılandırmasına genel hata işleme ekleme.
- Uygulama, sayfa ve kod düzeylerinde hata işleme ekleme.
- Daha sonra gözden geçirme için hataları günlüğe kaydetme.
- Güvenliği tehlikeye Mayan hata iletilerini görüntüleme.
- Hata günlüğü modülleri ve Işleyiciler (ELMAH) hata günlüğünü uygulama.

## <a name="overview"></a>Genel Bakış

ASP.NET uygulamaları, yürütme sırasında oluşan hataları tutarlı bir şekilde işleyebilmelidir. ASP.NET, hataların uygulamalara tek bir şekilde bildirimde bulunmak için bir yol sağlayan ortak dil çalışma zamanını (CLR) kullanır. Bir hata oluştuğunda, bir özel durum oluşturulur. Bir özel durum, bir uygulamanın karşılaştığı herhangi bir hata, koşul veya beklenmedik davranışdır.

.NET Framework, özel durum `System.Exception` sınıfından devralan bir nesnedir. Bir sorunun oluştuğu bir kod alanından bir özel durum oluşur. Özel durum, çağrı yığınını uygulamanın özel durumu işlemek için kod sağladığı bir yere iletilir. Uygulama özel durumu işlemezse, tarayıcı hata ayrıntılarını görüntülemeye zorlanır.

En iyi uygulama olarak, kodunuzun içindeki `Try` bloklarda / `Catch` / `Finally` bulunan kod düzeyinde hataları işleyin. Bu blokları, kullanıcının oluşabilecek bağlamdaki sorunları düzeltebilmesi için yerleştirmeyi deneyin. Hata işleme blokları hatanın oluştuğu yerden çok uzakta ise, kullanıcılara sorunu çözmesi için gereken bilgileri sağlaması daha zordur.

### <a name="exception-class"></a>Özel durum sınıfı

Özel durum sınıfı, özel durumların devraldığı temel sınıftır. Çoğu özel durum nesnesi, `SystemException` sınıf `IndexOutOfRangeException` , sınıf veya `ArgumentNullException` sınıf gibi özel durum sınıfının türetilmiş sınıfının örnekleridir. Özel durum sınıfı, oluşan hata hakkında belirli bilgiler `StackTrace` sağlayan özelliği `InnerException` , özelliği ve `Message` özelliği gibi özelliklere sahiptir.

### <a name="exception-inheritance-hierarchy"></a>Özel durum devralma hiyerarşisi

Çalışma zamanı, bir özel durumla karşılaşıldığında çalışma zamanının aldığı `SystemException` sınıftan türetilen bir temel özel durum kümesine sahiptir. `IndexOutOfRangeException` Sınıf`ArgumentNullException` ve sınıf gibi özel durum sınıfından kalıtımla alan sınıfların çoğu ek üye uygulamaz. Bu nedenle, bir özel durum için en önemli bilgiler özel durumlar, özel durum adı ve özel durumda bulunan bilgiler hiyerarşisinde bulunabilir.

### <a name="exception-handling-hierarchy"></a>Özel durum Işleme hiyerarşisi

Bir ASP.NET Web Forms uygulamasında özel durumlar, belirli bir işleme hiyerarşisine göre işlenebilir. Bir özel durum aşağıdaki düzeylerde işlenebilir:

- Uygulama düzeyi
- Sayfa düzeyi
- Kod düzeyi

Bir uygulama özel durumları işlediğinde, özel durum sınıfından devralınan özel durum hakkında ek bilgiler genellikle alınır ve kullanıcıya gösterilir. Uygulamanın, sayfanın ve kod düzeyinin yanı sıra, özel durumları da HTTP modülü düzeyinde işleyebilir ve bir IIS özel işleyicisi kullanabilirsiniz.

### <a name="application-level-error-handling"></a>Uygulama düzeyi hata Işleme

Uygulamanızın yapılandırmasını değiştirerek ya da uygulamanızın `Application_Error` *Global. asax* dosyasına bir işleyici ekleyerek, varsayılan hataları uygulama düzeyinde işleyebilirsiniz.

`customErrors` *Web. config* dosyasına bir bölüm ekleyerek varsayılan hataları ve HTTP hatalarını işleyebilirsiniz. Bu `customErrors` bölüm, bir hata oluştuğunda kullanıcıların yeniden yönlendirileceği varsayılan sayfayı belirtmenize olanak tanır. Ayrıca, belirli durum kodu hataları için ayrı sayfalar belirtmenize olanak tanır.

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

Ne yazık ki, kullanıcıyı farklı bir sayfaya yönlendirmek için yapılandırmayı kullandığınızda oluşan hatanın ayrıntılarına sahip değilsiniz.

Ancak, `Application_Error` *Global. asax* dosyasındaki işleyiciye kod ekleyerek uygulamanızda herhangi bir yerde oluşan hataları yakalayabilirsiniz.

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>Sayfa düzeyi hata olayı Işleme

Sayfa düzeyindeki bir işleyici, kullanıcıyı Hatanın gerçekleştiği sayfaya döndürür, ancak denetimlerin örnekleri korunmadığı için sayfada artık hiçbir şey olmayacaktır. Uygulamanın kullanıcısına hata ayrıntılarını sağlamak için, hata ayrıntılarını sayfaya özel olarak yazmanız gerekir.

İşlenmemiş hataları günlüğe kaydetmek veya kullanıcıyı faydalı bilgileri görüntüleyebilen bir sayfaya almak için genellikle sayfa düzeyinde bir hata işleyicisi kullanırsınız.

Bu kod örneği, bir ASP.NET Web sayfasındaki hata olayı için bir işleyici gösterir. Bu işleyici, sayfadaki bloklar içinde `try` / `catch` henüz işlenmemiş tüm özel durumları yakalar.

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

Bir hatayı tamamladıktan sonra, sunucu nesnesinin ( `ClearError` `HttpServerUtility` sınıf) yöntemini çağırarak onu temizlemeniz gerekir, aksi takdirde daha önce oluşan bir hata görürsünüz.

### <a name="code-level-error-handling"></a>Kod düzeyinde hata Işleme

Try-catch deyimleri, farklı özel durumlar için işleyiciler belirten bir try bloğundan sonra bir veya daha fazla catch yan tümcesi içerir. Bir özel durum oluştuğunda, ortak dil çalışma zamanı (CLR) bu özel durumu işleyen catch ifadesini arar. Şu anda yürütülmekte olan yöntem bir catch bloğu içermiyorsa, CLR geçerli yöntemi çağıran yönteme bakar ve bu şekilde çağrı yığınını ve bu şekilde devam eder. Catch bloğu bulunmazsa, CLR kullanıcıya işlenmeyen bir özel durum iletisi görüntüler ve programın yürütülmesini engeller.

Aşağıdaki kod örneği, hataları işlemek `try` için kullanmanın / `catch` / `finally` yaygın bir yolunu gösterir.

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

Yukarıdaki kodda, try bloğu olası bir özel duruma karşı korunması gereken kodu içerir. Blok, bir özel durum oluşana ya da blok başarıyla tamamlanana kadar yürütülür. Bir `FileNotFoundException` özel durum `IOException` ya da özel durum oluşursa, yürütme farklı bir sayfaya aktarılır. Ardından, finally bloğunda yer alan kod, bir hata oluşup oluşmadığını, yürütülür.

## <a name="adding-error-logging-support"></a>Hata günlüğü desteği ekleme

Wingtip Toys örnek uygulamasına hata işleme eklemeden önce, `ExceptionUtility` *Logic* Folder 'a bir sınıf ekleyerek hata günlüğü desteği ekleyeceksiniz. Bunu yaparak, uygulama bir hata işlediğinde hata ayrıntıları hata günlüğü dosyasına eklenecektir.

1. *Logic* Folder öğesine sağ tıklayın ve ardından **Yeni öğe** **Ekle**  - &gt; ' yi seçin.   
   **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **görsel C#**   -kodşablonları grubunu seçin. &gt; Ardından, orta listeden **sınıf**' ı seçin ve **ExceptionUtility.cs**olarak adlandırın.
3. Seçin **ekleme**. Yeni sınıf dosyası görüntülenir.
4. Mevcut kodu şu kodla değiştirin:  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

Bir özel durum oluştuğunda, özel durum `LogException` yöntemini çağırarak özel durum günlük dosyasına yazılabilir. Bu yöntem, özel durum nesnesi ve özel durum kaynağıyla ilgili ayrıntıları içeren bir dize olmak üzere iki parametre alır. Özel durum günlüğü, *\_uygulama verileri* klasöründeki *hata günlüğü. txt* dosyasına yazılır.

### <a name="adding-an-error-page"></a>Hata sayfası ekleme

Wingtip Toys örnek uygulamasında, hataları göstermek için bir sayfa kullanılacaktır. Hata sayfası, site kullanıcılarına güvenli bir hata iletisi göstermek için tasarlanmıştır. Ancak Kullanıcı, kodun bulunduğu makinede yerel olarak sunulan bir HTTP isteği oluşturan bir geliştiricisiyseniz hata sayfasında ek hata ayrıntıları görüntülenir.

1. **Çözüm Gezgini** içinde proje adına (**Wingtip Toys**) sağ tıklayın ve **Yeni öğe** **Ekle**  - &gt; ' yi seçin.   
   **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **görsel C#**   -Webşablonları grubunu seçin. &gt; Orta listeden, **Ana sayfa Içeren Web formu**' nu seçin ve **ErrorPage. aspx**olarak adlandırın.
3. **Ekle**'yi tıklatın.
4. Ana sayfa olarak *site. Master* dosyasını seçin ve ardından **Tamam**' ı seçin.
5. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. Arka plan kodu (*ErrorPage.aspx.cs*) için varolan kodu aşağıdaki gibi görünecek şekilde değiştirin:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

Hata sayfası görüntülendiğinde, `Page_Load` olay işleyicisi yürütülür. `Page_Load` İşleyicisinde, hatanın ilk işlendiği konum belirlenir. Ardından, gerçekleşen son hata sunucu nesnesinin `GetLastError` yöntemini çağırarak belirlenir. Özel durum artık yoksa, genel bir özel durum oluşturulur. Ardından, HTTP isteği yerel olarak yapılmışsa tüm hata ayrıntıları gösterilir. Bu durumda, yalnızca Web uygulamasını çalıştıran yerel makinede bu hata ayrıntıları görüntülenir. Hata bilgileri görüntülendikten sonra, hata günlük dosyasına eklenir ve hata sunucudan temizlenir.

### <a name="displaying-unhandled-error-messages-for-the-application"></a>Uygulama için Işlenmemiş hata Iletilerini görüntüleme

`customErrors` *Web. config* dosyasına bir bölüm ekleyerek, uygulama genelinde oluşan basit hataları hızlı bir şekilde işleyebilirsiniz. Ayrıca, 404 dosyası bulunamadı gibi durum kodu değerlerine göre hataların nasıl işleneceğini belirtebilirsiniz.

#### <a name="update-the-configuration"></a>Yapılandırmayı güncelleştirme

`customErrors` *Web. config* dosyasına bir bölüm ekleyerek yapılandırmayı güncelleştirin.

1. **Çözüm Gezgini**' de, Wingtip Toys örnek uygulamasının kökündeki *Web. config* dosyasını bulun ve açın.
2. Bölümünü düğüm içindeki *Web. config* dosyasına aşağıdaki şekilde ekleyin: `<system.web>` `customErrors`   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. *Web. config* dosyasını kaydedin.

`customErrors` Bölümü, "on" olarak ayarlanan modu belirtir. Ayrıca, bir hata `defaultRedirect`oluştuğunda uygulamaya hangi sayfanın gidecağını belirten öğesini de belirtir. Ayrıca, bir sayfa bulunamadığında 404 hatasını nasıl işleyeceğinizi belirten belirli bir hata öğesi eklediniz. Bu öğreticide daha sonra, uygulama düzeyinde bir hatanın ayrıntılarını yakalayan ek hata işleme ekleyeceksiniz.

#### <a name="running-the-application"></a>Uygulamayı Çalıştırma

Güncelleştirilmiş yolları görmek için uygulamayı şimdi çalıştırabilirsiniz.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **F5** tuşuna basın.  
 Tarayıcı açılır ve *default. aspx* sayfasını gösterir.
2. Tarayıcıya aşağıdaki URL 'YI girin (bağlantı noktası numaranızı kullandığınızdan emin olun ):  
    `https://localhost:44300/NoPage.aspx`
3. Tarayıcıda görüntülenmekte olan *ErrorPage. aspx* ' i gözden geçirin. 

    ![ASP.NET hata Işleme-sayfa bulunamadı hatası](aspnet-error-handling/_static/image1.png)

Mevcut olmayan *Nopage. aspx* sayfasını istediğinizde hata sayfası, ek ayrıntılar varsa basit hata iletisini ve ayrıntılı hata bilgilerini gösterir. Ancak, Kullanıcı uzak bir konumdan var olmayan bir sayfa istediyse, hata sayfası yalnızca kırmızı renkte görünür.

### <a name="including-an-exception-for-testing-purposes"></a>Sınama amacıyla özel durum ekleme

Bir hata oluştuğunda uygulamanızın nasıl çalıştığını doğrulamak için, ASP.NET ' de kasıtlı olarak hata koşulları oluşturabilirsiniz. Wingtip Toys örnek uygulamasında, ne olacağını görmek için varsayılan sayfa yüklendiğinde bir test özel durumu oluşturacaksınız.

1. Visual Studio 'da *default. aspx* sayfasının arkasındaki kodu açın.   
   *Default.aspx.cs* arka plan kod sayfası görüntülenir.
2. `Page_Load` İşleyicisinde, işleyicinin aşağıdaki gibi görünmesi için kod ekleyin:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

Farklı özel durumlar türleri oluşturmak mümkündür. Yukarıdaki kodda, *default. aspx* sayfası yüklendiğinde bir `InvalidOperationException` oluşturulur.

#### <a name="running-the-application"></a>Uygulamayı Çalıştırma

Uygulamanın özel durumu nasıl işlediğini görmek için uygulamayı çalıştırabilirsiniz.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **CTRL + F5** tuşlarına basın.  
 Uygulama InvalidOperationException öğesini oluşturur. 

    > [!NOTE] 
    > 
    > Visual Studio 'da hatanın kaynağını görüntülemek için sayfayı koda girmeden görüntülemek için **CTRL + F5** tuşlarına basmanız gerekir.
2. Tarayıcıda görüntülenmekte olan *ErrorPage. aspx* ' i gözden geçirin. 

    ![ASP.NET hata Işleme-hata sayfası](aspnet-error-handling/_static/image2.png)

Hata ayrıntılarında görebileceğiniz gibi, özel durum, `customError` *Web. config* dosyasındaki bölümü tarafından yakalanmıştı.

### <a name="adding-application-level-error-handling"></a>Uygulama düzeyinde hata Işleme ekleme

`customErrors` *Web. config* dosyasındaki bölümü kullanarak özel durumu yakalamak yerine, özel durum hakkında çok az bilgi edinen, bu hatayı uygulama düzeyinde yakalayabilir ve hata ayrıntılarını alabilirsiniz.

1. **Çözüm Gezgini**, *Global.asax.cs* dosyasını bulun ve açın.
2. Aşağıdaki gibi görünmesi için bir **uygulama\_hata** işleyicisi ekleyin:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

Uygulamada bir hata oluştuğunda `Application_Error` işleyici çağırılır. Bu İşleyicide, son özel durum alınır ve gözden geçirilir. Özel durum işlenmemiş ise ve özel durum iç özel durum ayrıntıları içeriyorsa (yani, `InnerException` null değilse), uygulama yürütmeyi özel durum ayrıntılarının görüntülendiği hata sayfasına aktarır.

#### <a name="running-the-application"></a>Uygulamayı Çalıştırma

Uygulamayı, uygulama düzeyinde özel durumu işleyerek belirtilen ek hata ayrıntılarını görmek için çalıştırabilirsiniz.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **CTRL + F5** tuşlarına basın.  
 Uygulama öğesini oluşturur `InvalidOperationException` .
2. Tarayıcıda görüntülenmekte olan *ErrorPage. aspx* ' i gözden geçirin. 

    ![ASP.NET hata Işleme-uygulama düzeyi hatası](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>Sayfa düzeyinde hata Işleme ekleme

Sayfanın `ErrorPage` `@Page` yönergesine bir öznitelik ekleyerek veya sayfanın arka plan koduna bir `Page_Error` olay işleyicisi ekleyerek sayfaya sayfa düzeyinde hata işleme ekleme ekleyebilirsiniz. Bu bölümde, *ErrorPage. aspx* sayfasına `Page_Error` yürütmeyi aktaracaktır bir olay işleyicisi ekleyeceksiniz.

1. **Çözüm Gezgini**, *default.aspx.cs* dosyasını bulun ve açın.
2. Arka plan `Page_Error` kodun aşağıdaki gibi görünmesi için bir işleyici ekleyin:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

Sayfada bir hata oluştuğunda `Page_Error` olay işleyicisi çağrılır. Bu İşleyicide, son özel durum alınır ve gözden geçirilir. Bir `InvalidOperationException` gerçekleşirse`Page_Error` , olay işleyicisi yürütmeyi özel durum ayrıntılarının görüntülendiği hata sayfasına aktarır.

#### <a name="running-the-application"></a>Uygulamayı Çalıştırma

Güncelleştirilmiş yolları görmek için uygulamayı şimdi çalıştırabilirsiniz.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **CTRL + F5** tuşlarına basın.  
 Uygulama öğesini oluşturur `InvalidOperationException` .
2. Tarayıcıda görüntülenmekte olan *ErrorPage. aspx* ' i gözden geçirin. 

    ![ASP.NET hata Işleme-sayfa düzeyi hatası](aspnet-error-handling/_static/image4.png)
3. Tarayıcı pencerenizi kapatın.

### <a name="removing-the-exception-used-for-testing"></a>Test için kullanılan özel durum kaldırılıyor

Bu öğreticide daha önce eklediğiniz özel durumu oluşturmadan Wingtip Toys örnek uygulamasının çalışmasına izin vermek için özel durumu kaldırın.

1. *Varsayılan. aspx* sayfasının arkasındaki kodu açın.
2. `Page_Load` İşleyicide, işleyicinin aşağıdaki gibi görünmesi için özel durumu oluşturan kodu kaldırın:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>Kod düzeyinde hata günlüğü ekleme

Bu öğreticide daha önce bahsedildiği gibi, kod bölümünü çalıştırmayı denemek ve oluşan ilk hatayı işlemek için try/catch deyimleri ekleyebilirsiniz. Bu örnekte, hatanın daha sonra incelenebilecek olması için hata günlüğü dosyasına yalnızca hata ayrıntılarını yazarsınız.

1. **Çözüm Gezgini**, *Logic* klasöründe, *PayPalFunctions.cs* dosyasını bulun ve açın.
2. `HttpCall` Yöntemi, kodun aşağıdaki gibi görünmesi için güncelleştirin:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

Yukarıdaki kod, `ExceptionUtility` sınıfında bulunan `LogException` yöntemini çağırır. Bu öğreticide daha önce *ExceptionUtility.cs* sınıf dosyasını *Logic* Folder 'a eklediniz. `LogException` Yöntem iki parametre alır. İlk parametre özel durum nesnesidir. İkinci parametre, hatanın kaynağını tanımak için kullanılan bir dizedir.

### <a name="inspecting-the-error-logging-information"></a>Hata günlüğü bilgileri inceleniyor

Daha önce belirtildiği gibi, uygulamanızda ilk olarak hangi hataların düzeltilceğini öğrenmek için hata günlüğünü kullanabilirsiniz. Tabii ki yalnızca, yakalanan ve hata günlüğüne yazılan hatalar kaydedilir.

1. **Çözüm Gezgini**' de, *\_uygulama verileri* klasöründeki *hata günlüğü. txt* dosyasını bulun ve açın.   
 *Hata günlüğü. txt* dosyasını görmek için, **Çözüm Gezgini** en üstünden "**tüm dosyaları göster**" seçeneğini veya "**Yenile**" seçeneğini belirlemeniz gerekebilir.
2. Visual Studio 'da görünen hata günlüğünü gözden geçirin: 

    ![ASP.NET hata Işleme-hata günlüğü. txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>Güvenli hata Iletileri

Uygulamanız hata iletileri görüntülediğinde, kötü niyetli bir kullanıcının uygulamanıza saldırmaya yardımcı olabilecek bilgiler **vermediğine dikkat edin** . Örneğin, uygulamanız bir veritabanına yazma girişiminde bulunursa, kullanmakta olduğu Kullanıcı adını içeren bir hata iletisi görüntülememelidir. Bu nedenle, kullanıcıya kırmızı renkte genel bir hata iletisi görüntülenir. Tüm ek hata ayrıntıları yalnızca yerel makinedeki geliştiriciye görüntülenir.

## <a name="using-elmah"></a>ELMAH kullanma

ELMAH (hata günlüğü modülleri ve Işleyiciler), ASP.NET uygulamanıza bir NuGet paketi olarak taktığınız bir hata günlüğü tesisdir. ELMAH aşağıdaki özellikleri sağlar:

- İşlenmemiş özel durumların günlüğü.
- İşlenmemiş özel durumların tamamına ait günlüğün tamamını görüntülemek için bir Web sayfası.
- Günlüğe kaydedilen her özel durumun tüm ayrıntılarını görüntülemek için bir Web sayfası.
- Her hatanın gerçekleştiği sırada bir e-posta bildirimi.
- Günlükteki son 15 hatanın RSS akışı.

ELMAH ile çalışabilmeniz için önce onu yüklemelisiniz. Bu, *NuGet* paket yükleyicisi kullanılarak kolay bir işlemdir. Bu öğretici serisinde daha önce bahsedildiği gibi, NuGet, Visual Studio 'da açık kaynak kitaplıklarını ve araçları yüklemeyi ve güncelleştirmeyi kolaylaştıran bir Visual Studio uzantısıdır.

1. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi** > **çözüm için NuGet Paketlerini Yönet**' i seçin. 

    ![ASP.NET hata Işleme-çözüm için NuGet paketlerini yönetme](aspnet-error-handling/_static/image6.png)
2. **NuGet Paketlerini Yönet** Iletişim kutusu Visual Studio içinde görüntülenir.
3. **NuGet Paketlerini Yönet** iletişim kutusunda, sol taraftaki **çevrimiçi** ' i genişletin ve ardından **NuGet.org**' ı seçin. Daha sonra, kullanılabilir paketler listesinden **ELMAH** paketini bulun ve çevrimiçi olarak yeniden yükler. 

    ![ASP.NET hata Işleme-ELMA NuGet paketi](aspnet-error-handling/_static/image7.png)
4. Paketi indirmek için bir internet bağlantınızın olması gerekir.
5. **Projeleri Seç** Iletişim kutusunda **wingtiptoys** seçiminin seçili olduğundan emin olun ve ardından **Tamam**' a tıklayın. 

    ![ASP.NET hata Işleme-proje Seç Iletişim kutusu](aspnet-error-handling/_static/image8.png)
6. Gerekirse **NuGet Paketlerini Yönet** Iletişim kutusunda **Kapat** ' a tıklayın.
7. Visual Studio herhangi bir açık dosyayı yeniden yükledikten sonra "**Tümüne Evet**" i seçin.
8. ELMAH paketi, projenizin kökündeki *Web. config* dosyasında kendisi için girdiler ekler. Visual Studio, değiştirilen *Web. config* dosyasını yeniden yüklemek isteyip istemediğinizi ısterse, **Evet**' e tıklayın.

ELMAH artık oluşan işlenmemiş hataları depolamaya hazırdır.

### <a name="viewing-the-elmah-log"></a>ELMAH günlüğünü görüntüleme

ELMAH günlüğünü görüntüleme kolaydır, ancak ilk olarak ELMAH günlüğünde kaydedilecek işlenmemiş bir özel durum oluşturacaksınız.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **CTRL + F5** tuşlarına basın.
2. ELMAH günlüğüne işlenmeyen bir özel durum yazmak için tarayıcınızda aşağıdaki URL 'ye gidin (bağlantı noktası numaranızı kullanarak):  
    `https://localhost:44300/NoPage.aspx`Hata sayfası görüntülenir.
3. ELMAH günlüğünü göstermek için tarayıcınızda aşağıdaki URL 'ye gidin (bağlantı noktası numaranızı kullanarak):  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET hata Işleme-ELMAH hata günlüğü](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>Özet

Bu öğreticide, uygulama düzeyinde, sayfa düzeyinde ve kod düzeyinde hataları işleme hakkında bilgi edindiniz. Ayrıca, daha sonra gözden geçirmek üzere işlenmiş ve işlenmemiş hataların nasıl günlüğe alınacağını da öğrendiniz. NuGet kullanarak uygulamanıza özel durum günlüğü ve bildirim sağlamak için ELMAH yardımcı programını eklediniz. Ayrıca, güvenli hata iletilerinin önemini öğrendiniz.

## <a name="tutorial-series-conclusion"></a>Öğretici serisi sonuç

Takip ederiz. Bu öğretici kümesini, ASP.NET Web Forms hakkında daha tanıdık gelmemize yardımcı olacak şekilde umuyoruz. ASP.NET 4,5 ve Visual Studio 2013 Web Forms özellikler hakkında daha fazla bilgiye ihtiyacınız varsa [Visual Studio 2013 Sürüm notları için ASP.NET and Web Tools](../../../../visual-studio/overview/2013/release-notes.md)bakın. Ayrıca, **sonraki adımlar** bölümünde bahsedilen öğreticiye göz atın ve [ücretsiz Azure](https://azure.microsoft.com/pricing/free-trial/)denemesini inceleyin.

![Teşekkürler-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>Sonraki Adımlar

Web uygulamanızı Microsoft Azure dağıtma hakkında daha fazla bilgi için bkz. [Membership, OAuth ve SQL veritabanı Ile güvenli bir ASP.NET Web Forms uygulamasını Azure Web sitesine](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)dağıtma.

## <a name="free-trial"></a>Ücretsiz deneme

[Microsoft Azure Ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)  
 Web sitenizin Microsoft Azure için yayımlanması zaman, bakım ve harcama tasarrufu sağlar. Web uygulamanızı Azure 'a dağıtmak için hızlı bir işlemdir. Web uygulamanızı korumanız ve izlemeniz gerektiğinde, Azure çeşitli araçlar ve hizmetler sunar. Azure 'da verileri, trafiği, kimliği, yedeklemeleri, mesajlaşma, medyayı ve performansı yönetin. Ve tüm bunlar, çok maliyetli bir yaklaşımda sunulmaktadır.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET sistem durumu Izleme ile hata ayrıntılarını günlüğe kaydetme](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>Bildirimler

Bu öğretici serisinin içeriğine önemli bir katkı yapan kişiler için teşekkür ederiz:

- [Alberto Poblacion, MVP &amp; MCT, İspanya](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex thissen, Hollanda](http://blog.alexthissen.nl/) (Twitter: [@alexthissen](http://twitter.com/alexthissen))
- [Andre Tournier, USA](http://andret503.wordpress.com/)
- Apurva Joshi, Microsoft
- [Bojan Vrhovnik, Slovenya](http://twitter.com/bvrhovnik)
- [Bruno Sonnino, Brezilya](http://msmvps.com/blogs/bsonnino) (Twitter: [@bsonnino](http://twitter.com/bsonnino))
- [Carlos dos Santos, Brezilya](http://www.carloscds.net/)
- [Pave kaven Bell, ABD](http://www.wynapse.com/) (Twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))
- [Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (Twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Michael parçaları, ABD](http://www.930solutions.com/) (Twitter: [@mrsharps](http://twitter.com/mrsharps))
- Mike Pope
- [Mitchel satıcıları, ABD](http://www.mitchelsellers.com/) (Twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))
- [Paul Cociuba, Microsoft](http://linqto.me/Links/pcociuba)
- [Paulo Morgado, Portekiz](http://paulomorgado.net/)
- [Pranav Oystogi, Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann, Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra, Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>Topluluk katkıları

- Grahemendick ([@grahammendick](http://twitter.com/grahammendick))  
  MSDN 'de Visual Studio 2012 ile ilgili kod örneği: [Gezinti Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  MSDN 'de Visual Studio 2012 ile ilgili kod örneği: [ASP.NET 4,5 Web Forms öğretici serisi Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft Teknik Kitleci katılımcısı (Twitter @driazevedo:)  
  Visual Studio 2012 çevirisi: [Iniciando com ASP.NET Web Forms 4,5-parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [Önceki](url-routing.md)
