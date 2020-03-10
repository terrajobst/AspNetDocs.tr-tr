---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 bağımlılığı ekleme | Microsoft Docs
author: rick-anderson
description: 'Note: Bu uygulamalı laboratuvar, ASP.NET MVC ve ASP.NET MVC 4 filtrelerinin temel bilgisine sahip olduğunuzu varsayar. Daha önce ASP.NET MVC 4 filtrelerini kullanmadıysanız rec...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560615"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 Bağımlılık Ekleme

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

Bu uygulamalı laboratuvar, **ASP.NET MVC** ve **ASP.NET MVC 4 filtrelerinin**temel bilgisine sahip olduğunuzu varsayar. Daha önce **ASP.NET MVC 4 filtrelerini** kullanmadıysanız, **ASP.NET MVC özel eylem filtreleri** uygulamalı laboratuvarına gitmeniz önerilir.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 bağımlılığı ekleme](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)adresinde bulunabilir.

**Nesne yönelimli programlama** paradigması 'nda nesneler, katkıda bulunanlar ve tüketiciler bulunan bir işbirliği modelinde birlikte çalışır. Doğal olarak, bu iletişim modeli nesneler ve bileşenler arasında bağımlılıklar oluşturur ve karmaşıklık arttıkça yönetilmesi zor hale gelir.

![Sınıf bağımlılıkları ve model karmaşıklığı](aspnet-mvc-4-dependency-injection/_static/image1.png "Sınıf bağımlılıkları ve model karmaşıklığı")

*Sınıf bağımlılıkları ve model karmaşıklığı*

Büyük olasılıkla, istemci nesnelerinin genellikle hizmet konumundan sorumlu olduğu, **fabrika modelini** ve arabirim ile uygulama arasındaki ayrımı hakkında bilgi sahibi olabilirsiniz.

Bağımlılık ekleme deseninin, denetimin Inversion öğesinin belirli bir uygulamasıdır. **Denetimin INVERSION (IOC)** , nesnelerin işlerini yapmak için kullandıkları başka nesneler oluşturmayacağı anlamına gelir. Bunun yerine, bir dış kaynaktan (örneğin, bir XML yapılandırma dosyası) ihtiyaç duydukları nesneleri alırlar.

**Bağımlılık ekleme (dı)** , bu, genellikle Oluşturucu parametrelerini geçiren ve özellikleri ayarlanmış bir çerçeve bileşeni tarafından nesne müdahalesi olmadan yapıldığı anlamına gelir.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>Bağımlılık ekleme (dı) tasarım deseninin

Yüksek düzeyde, bağımlılık ekleme 'nin amacı, bir istemci sınıfının (örneğin *, golfçü*) bir arabirim (ör. *Iclub*) karşılayan bir şeye ihtiyaç duymaktır. Somut türün ne olduğunu (ör. *Woodclub, ıronkulüler, Dilimgeclub* veya *putterkulüler*), başka birinin (örneğin, iyi bir *Caddy*) işlemesini istiyor. ASP.NET MVC 'deki bağımlılık Çözümleyicisi, başka bir yere (ör. bir kapsayıcı veya *sinek torbası*) bağımlılık mantığınızı kaydetmenize izin verebilir.

![Bağımlılık ekleme diyagramı](aspnet-mvc-4-dependency-injection/_static/image2.png "Bağımlılık ekleme çizimi")

*Bağımlılık ekleme-Golf benzerleme vurguladı*

Bağımlılık ekleme deseninin ve denetimin Inversion kullanmanın avantajları şunlardır:

- Sınıf bağlantısını azaltır
- Kodu yeniden kullanma artırır
- Kod bakımumu geliştirir
- Uygulama testini geliştirir

> [!NOTE]
> Bağımlılık ekleme bazen soyut fabrika tasarım düzeniyle karşılaştırılır, ancak her iki yaklaşım arasında hafif bir farklılık vardır. Dı, fabrikaları ve kayıtlı Hizmetleri çağırarak bağımlılıkları çözümlemek için arka planda çalışan bir çerçevedir.

Bağımlılık ekleme modelini anladığınıza göre, bu laboratuvarın tamamında ASP.NET MVC 4 ' te nasıl uygulanacağını öğreneceksiniz. Bir veritabanı erişim hizmeti eklemek için **denetleyicilerde** bağımlılık ekleme 'yi kullanmaya başlayacaksınız. Daha sonra, bir hizmeti kullanmak ve bilgileri göstermek için **görünümlere** bağımlılık ekleme işlemini uygulayacaksınız. Son olarak, ASP.NET MVC 4 filtrelerinden bir özel eylem filtresi ekleme.

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- NuGet paketlerini kullanarak bağımlılık ekleme için Unity ile ASP.NET MVC 4 ' ü tümleştirin
- ASP.NET MVC denetleyicisi içinde bağımlılık ekleme kullanma
- ASP.NET MVC görünümü içinde bağımlılık ekleme kullanma
- Bağımlılık ekleme Işlemini bir ASP.NET MVC eylem filtresi içinde kullanma

> [!NOTE]
> Bu laboratuvar, bağımlılık çözümlemesi için Unity. Mvc3 NuGet paketini kullanıyor, ancak herhangi bir bağımlılık ekleme çerçevesini ASP.NET MVC 4 ile çalışacak şekilde uyarlamak mümkündür.

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

**Kod parçacıklarını yükleme**

Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır. Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek B: kod parçacıkları&quot;kullanarak](#AppendixB) bu belgedeki eke başvurabilirsiniz &quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:

1. [Alıştırma 1: ekleme a Controller](#Exercise1)
2. [Alıştırma 2: ekleme a View](#Exercise2)
3. [Alıştırma 3: ekleme filtreleri](#Exercise3)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>Alıştırma 1: ekleme a Controller

Bu alıştırmada, bir NuGet paketi kullanarak Unity 'yi tümleştirerek ASP.NET MVC denetleyicilerindeki bağımlılık ekleme işlemini nasıl kullanacağınızı öğreneceksiniz. Bu nedenle, verileri veri erişiminden ayırmak için MvcMusicStore denetleyicilerinize hizmetleri dahil edersiniz. Hizmetler, **Unity**'Nin yardımıyla bağımlılık ekleme kullanılarak çözülecektir, denetleyici oluşturucuda yeni bir bağımlılık oluşturur.

Bu yaklaşım, daha esnek ve bakım ve test etme işlemlerini daha kolay olan, daha az bağlanmış uygulamalar oluşturmayı gösterir. Ayrıca, ASP.NET MVC 'nin Unity ile nasıl tümleştirileceğini öğreneceksiniz.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>StoreManager hizmeti hakkında

Başlangıç çözümünde belirtilen MVC müzik deposu artık **StoreService**adlı depolama denetleyicisi verilerini yöneten bir hizmet içeriyor. Mağaza hizmeti uygulamasını aşağıda bulabilirsiniz. Tüm yöntemlerin model varlıkları döndürdüğüne unutmayın.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

Başlangıç çözümünden **Storecontroller** artık **StoreService**kullanıyor. Tüm veri başvuruları **Storecontroller**'dan kaldırılmıştır ve artık **StoreService**kullanan herhangi bir yöntemi değiştirmeden geçerli veri erişim sağlayıcısını değiştirmek mümkün değildir.

**Storecontroller** uygulamasının sınıf oluşturucusunun Içinde **StoreService** 'e bağımlılığı olduğunu aşağıda bulabilirsiniz.

> [!NOTE]
> Bu alıştırmada tanıtılan bağımlılık, **denetimin INVERSION** (IOC) ile ilgilidir.
> 
> **Storecontroller** sınıf oluşturucusu, sınıfının içinden hizmet çağrıları gerçekleştirmek için gerekli olan bir **ıtoreservice** tür parametresi alır. Ancak **Storecontroller** , ASP.NET MVC ile çalışmak için herhangi bir denetleyicinin olması gereken varsayılan oluşturucuyu (parametresiz) uygulamaz.
> 
> Bağımlılığı çözümlemek için, denetleyicinin bir soyut fabrika tarafından oluşturulması gerekir (belirtilen türde herhangi bir nesne döndüren bir sınıf).

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> Parametresiz bir Oluşturucu bildirildiği için, sınıf, hizmet nesnesini göndermeden StoreController oluşturmayı denediğinde bir hata alacaksınız.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>Görev 1-uygulamayı çalıştırma

Bu görevde, uygulama mantığındaki veri erişimini ayıran mağaza denetleyicisine hizmeti içeren BEGIN uygulamasını çalıştıracaksınız.

Uygulamayı çalıştırırken, denetleyici hizmeti varsayılan olarak bir parametre olarak geçirilmediğinden bir özel durum alırsınız:

1. **Source\Ex01-Injecting Controller\Begin**dizininde bulunan **Başlangıç** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Uygulamayı hata ayıklamadan çalıştırmak için **CTRL + F5** tuşlarına basın. **Bu nesne için tanımlı olmayan &quot;oluşturucu**&quot;hata iletisini alırsınız:

    ![ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu")

    *ASP.NET MVC başlangıç uygulaması çalıştırılırken hata oluştu*
3. Tarayıcıyı kapatın.

Aşağıdaki adımlarda, bu denetleyiciye gereken bağımlılığı eklemek için müzik deposu çözümünde çalışacaksınız.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>2\. görev-MvcMusicStore çözümüne Unity dahil

Bu görevde, çözüme **Unity. Mvc3** NuGet paketini dahil edersiniz.

> [!NOTE]
> Unity. Mvc3 paketi ASP.NET MVC 3 için tasarlandı, ancak ASP.NET MVC 4 ile tamamen uyumludur.
> 
> Unity, örnek ve tür saklama için isteğe bağlı desteği olan hafif, genişletilebilir bir bağımlılık ekleme kapsayıcısıdır. Bu, herhangi bir tür .NET uygulamasında kullanmak için genel amaçlı bir kapsayıcıdır. Bağımlılık ekleme mekanizmalarda bulunan tüm ortak özellikleri sağlar: nesne oluşturma, gereksinimlerin soyutlaması, çalışma zamanında bağımlılıkları belirterek ve esneklik, kapsayıcıya bileşen yapılandırmasını erteleyerek.

1. **Mvcmusicstore** projesinde **Unity. Mvc3** NuGet paketini yükler. Bunu yapmak için, **diğer Windows** | **Görünüm** ' den **Paket Yöneticisi konsolunu** açın.
2. Şu komutu çalıştırın.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Unity. Mvc3 NuGet paketi yükleniyor](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity. Mvc3 NuGet paketi yükleniyor")

    *Unity. Mvc3 NuGet paketi yükleniyor*
3. **Unity. Mvc3** paketi yüklendikten sonra Unity yapılandırmasını basitleştirmek için otomatik olarak eklediği dosya ve klasörleri keşfedebilirsiniz.

    ![Unity. Mvc3 paketi yüklendi](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity. Mvc3 paketi yüklendi")

    *Unity. Mvc3 paketi yüklendi*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>Görev 3-Global.asax.cs uygulamasında Unity kaydetme\_başlangıç

Bu görevde, **Global.asax.cs** ' de bulunan **uygulama\_start** metodunu, Unity önyükleyici başlatıcısını çağırmak için güncelleştiğini ve sonra bağımlılık ekleme Için kullanacağınız hizmet ve denetleyiciyi kaydeden önyükleyici dosyasını güncelleştirirsiniz.

1. Şimdi, Unity kapsayıcısını ve bağımlılık çözümleyici 'yi Başlatan dosya olan önyükleyici 'yi yedektacaksınız. Bunu yapmak için **Global.asax.cs** açın ve **uygulama\_start** yöntemine aşağıdaki vurgulanmış kodu ekleyin.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-Unity 'Yi Başlat*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. **Bootstrapper.cs** dosyasını açın.
3. Şu ad alanlarını ekleyin: **Mvcmusicstore. Services** ve **MusicStore. Controllers**.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-önyükleyici ekleme ad alanı*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. **Buildunitycontainer** yönteminin Içeriğini, depo denetleyicisi ve mağaza hizmetini kaydeden aşağıdaki kodla değiştirin.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex01-kayıt depolama denetleyicisi ve hizmeti*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, şimdi Unity 'yi dahil ettikten sonra yüklenebildiğini doğrulamak için uygulamayı çalıştıracaksınız.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın, uygulamanın artık herhangi bir hata iletisi görüntülenmeden yüklenmesi gerekir.

    ![Uygulama bağımlılık ekleme ile çalıştırılıyor](aspnet-mvc-4-dependency-injection/_static/image6.png "Uygulama bağımlılık ekleme ile çalıştırılıyor")

    *Uygulama bağımlılık ekleme ile çalıştırılıyor*
2. **/Store**'a gidin. Bu işlem, artık **Unity**kullanılarak oluşturulan **storecontroller**'ı çağırır.

    ![MVC müzik deposu](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC müzik deposu")

    *MVC müzik deposu*
3. Tarayıcıyı kapatın.

Aşağıdaki alıştırmalarda, bağımlılık ekleme kapsamının ASP.NET MVC görünümleri ve eylem filtreleri içinde kullanmak için nasıl uzatılacağınızı öğreneceksiniz.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>Alıştırma 2: ekleme a View

Bu alıştırmada, Unity tümleştirmesi için ASP.NET MVC 4 ' ün yeni özelliklerine sahip bir görünümde bağımlılık ekleme işlemini nasıl kullanacağınızı öğreneceksiniz. Bunu yapmak için mağaza tarama görünümü içinde bir ileti ve aşağıda bir görüntü gösteren özel bir hizmet çağıracaksınız.

Ardından, projeyi Unity ile tümleştirecaksınız ve bağımlılıkları eklemek için özel bir bağımlılık Çözümleyicisi oluşturacaksınız.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>Görev 1-bir hizmeti tüketen bir görünüm oluşturma

Bu görevde, yeni bir bağımlılık oluşturmak için hizmet çağrısı gerçekleştiren bir görünüm oluşturacaksınız. Hizmet, bu çözüme dahil olan basit bir mesajlaşma hizmeti ile oluşur.

1. **Source\Ex02-Injecting View\Begin** klasöründe bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
      > 
      > Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. **/Services**içindeki **kaynak \varlıklar** klasöründe bulunan **MessageService.cs** ve **IMessageService.cs** sınıflarını dahil edin. Bunu yapmak için, **Hizmetler** klasörü öğesine sağ tıklayın ve **Varolan öğe Ekle**' yi seçin. Dosyaların konumuna gidin ve bunları dahil edin.

    ![Ileti hizmeti ve hizmet arabirimi ekleniyor](aspnet-mvc-4-dependency-injection/_static/image8.png "Ileti hizmeti ve hizmet arabirimi ekleniyor")

    *Ileti hizmeti ve hizmet arabirimi ekleniyor*

    > [!NOTE]
    > **Imessageservice** arabirimi, **MessageService** sınıfı tarafından uygulanan iki özelliği tanımlar. Bu özellikler-**ileti** ve **ImageUrl**-ileti ve görüntülenecek görüntünün URL 'sini depolar.
3. Projenin kök klasöründe **/Pages** klasörünü oluşturun ve sonra **MyBasePage.cs** sınıfını **source\varlıklarından**ekleyin. İçinden kalıtımla alacak temel sayfa aşağıdaki yapıya sahiptir.

    ![Sayfalar klasörü](aspnet-mvc-4-dependency-injection/_static/image9.png "Sayfalar klasörü")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. **/Views/Store** klasöründen **gözataal. cshtml** görünümünü açın ve **MyBasePage.cs**adresinden devralma yapın.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. Bir görüntü ve hizmet tarafından alınan bir ileti görüntülemek için, **Gözden** geçirme görünümünde **MessageService** 'e bir çağrı ekleyin.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>Görev 2-özel bir bağımlılık Çözümleyicisi ve özel bir görünüm sayfası Etkinleştirici dahil

Önceki görevde, içinde bir hizmet çağrısı gerçekleştirmek için bir görünümün içine yeni bir bağımlılık eklendi. Şimdi, ASP.NET MVC bağımlılık ekleme arabirimlerini **ıviewpageetkinleştirici** ve **ıdependencyresolver**uygulayarak bu bağımlılığı çöztecaksınız. Çözümdeki bir **ıdependencyresolver** uygulaması, Unity kullanarak hizmet alımı ile ilgilenecektir. Daha sonra, görünümlerin oluşturulmasını çözecek bir **ıviewpagesemblyınterface** özel uygulaması dahil edersiniz.

> [!NOTE]
> ASP.NET MVC 3 ' den itibaren, bağımlılık ekleme için uygulama, Hizmetleri kaydetme arabirimlerini basitleştirdi. **Idependencyresolver** ve **ıviewpageetkinleştirici** , bağımlılık ekleme için ASP.NET MVC 3 özelliklerinin bir parçasıdır.
> 
> **-Idependencyresolver** arabirimi önceki ımvcservicelocator 'un yerini almıştır. Idependencyresolver 'ın uygulayıcıları, hizmet veya hizmet koleksiyonunun bir örneğini döndürmelidir.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-Iviewpageetkinleştirici** arabirimi, görünüm sayfalarının bağımlılık ekleme yoluyla nasıl örneklendiği konusunda daha ayrıntılı denetim sağlar. **Iviewpageetkinleştirici** arabirimini uygulayan sınıflar, bağlam bilgilerini kullanarak görünüm örnekleri oluşturabilir.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. Projenin kök klasöründe/**Factory** klasörünü oluşturun.
2. **/Sources/Assets/** to **factory** klasöründen çözümünüze **CustomViewPageActivator.cs** ekleyin. Bunu yapmak için **/Factory** klasörüne sağ tıklayın, Ekle ' yi seçin.  **Mevcut öğe** ve ardından **CustomViewPageActivator.cs**' ı seçin. Bu sınıf, Unity kapsayıcısını tutmak için **ıviewpageetkinleştirici** arabirimini uygular.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **Customviewpageetkinleştirici** , bir Unity kapsayıcısı kullanarak bir görünümün oluşturulmasını yönetmekten sorumludur.
3. **/Sources/varlıklarından** **/factory** klasöründen **UnityDependencyResolver.cs** dosyasını ekleyin. Bunu yapmak için **/Factory** klasörüne sağ tıklayın, Ekle ' yi seçin.  **Varolan öğe** ve ardından **UnityDependencyResolver.cs** dosyası ' nı seçin.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **Unitydependencyresolver** sınıfı, Unity için özel bir dependencyresolver. Unity kapsayıcısı içinde bir hizmet bulunamazsa, taban çözümleyici gönderilir.

Aşağıdaki görevde her iki uygulama da modelin hizmetlerin ve görünümlerin konumunu bilmesini sağlamak için kaydedilir.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>Görev 3-Unity kapsayıcısı içinde bağımlılık ekleme için kaydetme

Bu görevde, bağımlılık ekleme işini yapmak için önceki tüm şeyleri bir araya getirebilirsiniz.

Çözümünüz Şu anda aşağıdaki öğelere sahiptir:

- **MyBaseClass** 'tan devralan ve **MessageService**'i tüketen bir **tarama** görünümü.
- Hizmet arabirimi için belirtilen bağımlılık eklenmesine sahip olan bir ara sınıf-**MyBaseClass**.
- Hizmet- **MessageService** ve arabirimi **ımessageservice**.
- Unity- **Unitydependencyresolver** için özel bir bağımlılık Çözümleyicisi; hizmet alımı ile ilgilidir.
- Sayfayı oluşturan bir görünüm sayfası Etkinleştirici- **Customviewpageetkinleştirici** .

**Gezinme** görünümü eklemek Için şimdi Unity kapsayıcısına özel bağımlılık çözümleyici 'yi kaydetmelisiniz.

1. **Bootstrapper.cs** dosyasını açın.
2. Hizmeti başlatmak için bir **MessageService** örneğini Unity kapsayıcısına kaydedin:

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Register Ileti hizmeti*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. **Mvcmusicstore. Factory** ad alanına bir başvuru ekleyin.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Factory ad alanı*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. **Customviewpageetkinleştirici** öğesini Unity kapsayıcısına bir görünüm sayfası Etkinleştirici olarak Kaydet:

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-Register Customviewpageetkinleştirici*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 varsayılan bağımlılık çözümleyicisini **Unitydependencyresolver**örneğiyle değiştirin. Bunu yapmak için, **Initialize** Yöntemi içeriğini aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex02-güncelleştirme bağımlılık Çözümleyicisi*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC varsayılan bağımlılık çözümleyici sınıfı sağlar. Unity için oluşturduğumuz özel bağımlılık çözümleyicilerine göre çalışmak için, bu çözümleyici değiştirilmelidir.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, mağaza tarayıcısının hizmeti tükettiğini ve görüntüyü ve alınan iletiyi gösterdiğini doğrulamak için uygulamayı çalıştıracaksınız:

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. Tarzlar menüsünde **rock** ' e tıklayın ve **MessageService** 'in görünüme nasıl eklendiğini ve hoş geldiniz iletisini ve görüntüsünü nasıl yüklei görün. Bu örnekte, &quot;**Rock**&quot;:

    ![MVC müzik deposu-görünüm ekleme](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC müzik deposu-görünüm ekleme")

    *MVC müzik deposu-görünüm ekleme*
3. Tarayıcıyı kapatın.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>Alıştırma 3: ekleme eylem filtreleri

Önceki uygulamalı laboratuvar **özel eylem filtrelerinde** , filtre özelleştirme ve ekleme ile çalıştık. Bu alıştırmada, Unity kapsayıcısını kullanarak bağımlılık ekleme ile filtrelerin nasıl ekleneceğini öğreneceksiniz. Bunu yapmak için, müzik deposu çözümüne, sitenin etkinliğini izleyen özel bir eylem filtresi ekleyebilirsiniz.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>Görev 1-çözüm içindeki Izleme Filtresi dahil

Bu görevde,, olayları izlemek için özel bir eylem filtresi olan müzik deposuna dahil edersiniz. Özel eylem filtresi kavramları zaten önceki laboratuvarda&quot;&quot;özel eylem filtrelerinde değerlendirildiğinden, filtre sınıfını bu laboratuvarın varlıklar klasöründen dahil eder ve ardından Unity için bir filtre sağlayıcısı oluşturursunuz:

1. **Source\ex03-ekleme Action Filter\begın** Folder konumundaki **Begin** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
      > 
      > Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. **/Sources/varlıklarından** **/filters** klasöründen **TraceActionFilter.cs** dosyasını ekleyin.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > Bu özel eylem filtresi ASP.NET izlemeyi gerçekleştirir. Daha fazla başvuru için &quot;ASP.NET MVC 4 yerel ve dinamik eylem filtrelerini&quot; Laboratuvarı kontrol edebilirsiniz.
3. **FilterProvider.cs** boş sınıfını **/Filters.** klasörüne ekleyin.
4. **FilterProvider.cs**içinde **System. Web. Mvc** ve **Microsoft. Yöntemler. Unity** ad alanlarını ekleyin.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı ad alanları ekleme*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. Sınıfın **IFilterProvider** arabiriminden devralmasını sağlayın.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. **FilterProvider** sınıfına bir **ıunitycontainer** özelliği ekleyin ve kapsayıcıyı atamak için bir sınıf Oluşturucu oluşturun.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı Oluşturucusu*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > Filtre sağlayıcısı sınıf Oluşturucusu içinde **Yeni** bir nesne oluşturmamıyor. Kapsayıcı bir parametre olarak geçirilir ve bağımlılık Unity tarafından çözülür.
7. **FilterProvider** sınıfında, **IFilterProvider** arabiriminden **GetFilters** yöntemini uygulayın.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-filtre sağlayıcısı GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>Görev 2-filtreyi kaydetme ve etkinleştirme

Bu görevde site izlemeyi etkinleştirecektir. Bunu yapmak için, izlemeye başlamak için filtreyi **Bootstrapper.cs BuildUnityContainer** yöntemine kaydedersiniz:

1. Proje kökünde bulunan **Web. config** dosyasını açın ve System. Web grubunda izleme izlemeyi etkinleştirin.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. Proje kökünde **Bootstrapper.cs** öğesini açın.
3. **Mvcmusicstore. Filters** ad alanına bir başvuru ekleyin.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-önyükleyici ekleme ad alanı*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. **Buildunitycontainer** yöntemini seçin ve filtreyi Unity kapsayıcısına kaydedin. Filtre sağlayıcısını ve eylem filtresini kaydetmeniz gerekir.

    (Kod parçacığı- *ASP.net bağımlılığı ekleme Laboratuvarı-Ex03-Register FilterProvider ve ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, uygulamayı çalıştıracaksınız ve özel eylem filtresinin etkinliğin izlenmesini test edersiniz:

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. Tarzlar menüsünde **rock** ' e tıklayın. İsterseniz daha fazla tarzya gidebilirsiniz.

    ![Müzik Deposu](aspnet-mvc-4-dependency-injection/_static/image11.png "Müzik Deposu")

    *Müzik Deposu*
3. Uygulama Izleme sayfasını görmek için **/Trace.exe** öğesine gidin ve **Ayrıntıları görüntüle**' ye tıklayın.

    ![Uygulama Izleme günlüğü](aspnet-mvc-4-dependency-injection/_static/image12.png "Uygulama Izleme günlüğü")

    *Uygulama Izleme günlüğü*

    ![Uygulama Izleme-Istek ayrıntıları](aspnet-mvc-4-dependency-injection/_static/image13.png "Uygulama Izleme-Istek ayrıntıları")

    *Uygulama Izleme-Istek ayrıntıları*
4. Tarayıcıyı kapatın.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak, bir NuGet paketi kullanarak Unity 'yi tümleştirerek ASP.NET MVC 4 ' te bağımlılık ekleme 'nin nasıl kullanılacağını öğrendiniz. Bunu başarmak için, denetleyiciler, görünümler ve eylem filtreleri içinde bağımlılık ekleme 'yi kullandınız.

Aşağıdaki kavramlar ele alınmıştır:

- ASP.NET MVC 4 bağımlılığı ekleme özellikleri
- Unity. Mvc3 NuGet paketini kullanarak Unity tümleştirmesi
- Denetleyicilere bağımlılık ekleme
- Görünümlerde bağımlılık ekleme
- Eylem filtrelerinin bağımlılık ekleme

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Ek B: kod parçacıklarını kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-dependency-injection/_static/image19.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-dependency-injection/_static/image20.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-dependency-injection/_static/image21.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-dependency-injection/_static/image22.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-dependency-injection/_static/image23.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-dependency-injection/_static/image24.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
