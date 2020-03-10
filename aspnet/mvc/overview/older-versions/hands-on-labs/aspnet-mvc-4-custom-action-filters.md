---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 özel eylem filtreleri | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC, bir eylem yöntemi çağrılmadan önce veya sonra filtreleme mantığını yürütmek için eylem filtreleri sağlar. Eylem filtreleri özel öznitelikler Tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579697"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 Özel Eylem Filtreleri

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

ASP.NET MVC, bir eylem yöntemi çağrılmadan önce veya sonra filtreleme mantığını yürütmek için eylem filtreleri sağlar. Eylem filtreleri, denetleyicinin eylem yöntemlerine eylem öncesi ve eylem sonrası davranışı eklemek için bildirim sağlayan özel özniteliklerdir.

Bu uygulamalı laboratuvarda, yük denetleyicisi isteklerini yakalamak ve bir sitenin etkinliğini bir veritabanı tablosuna kaydetmek için MvcMusicStore çözümüne özel bir eylem filtresi özniteliği oluşturacaksınız. Herhangi bir denetleyiciye veya eyleme ekleyerek günlüğe kaydetme filtrenizi ekleyebileceksiniz. Son olarak, ziyaretçilerin listesini gösteren günlük görünümünü görürsünüz.

Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar. Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC 4 temel** uygulamalı laboratuvarına gitmeniz önerilir.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 özel eylem filtrelerinde](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)bulunabilir.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Filtreleme yeteneklerini genişletmek için özel eylem filtresi özniteliği oluşturma
- Belirli bir düzeye ekleme yaparak özel filtre özniteliği uygulama
- Özel eylem filtrelerini küresel olarak kaydetme

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

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:

1. [Alıştırma 1: günlük eylemleri](#Exercise1)
2. [Alıştırma 2: birden çok eylem filtresini yönetme](#Exercise2)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**.

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>Alıştırma 1: günlük eylemleri

Bu alıştırmada, ASP.NET MVC 4 filtre sağlayıcılarını kullanarak özel bir eylem günlüğü filtresi oluşturmayı öğreneceksiniz. Bu amaçla, MusicStore sitesinde seçili denetleyicilere tüm etkinlikleri kaydedecek bir günlüğe kaydetme filtresi uygulayacaksınız.

Filtre **ActionFilterAttributeclass** öğesini genişletir ve her isteği yakalamak ve sonra günlüğe kaydetme eylemlerini gerçekleştirmek Için **OnActionExecuting** metodunu geçersiz kılar. HTTP istekleri, çalıştırılan Yöntemler, sonuçlar ve parametreler hakkındaki bağlam bilgileri ASP.NET MVC **ActionExecutingContext** sınıfı tarafından sağlanacaktır **.**

> [!NOTE]
> ASP.NET MVC 4 ' te özel bir filtre oluşturmadan kullanabileceğiniz varsayılan filtre sağlayıcıları da vardır. ASP.NET MVC 4, aşağıdaki filtre türlerini sağlar:
> 
> - **Yetkilendirme** filtresi, kimlik doğrulaması gerçekleştirme veya isteğin özelliklerini doğrulama gibi bir eylem yönteminin yürütülüp yürütülmeyeceğini belirten güvenlik kararları verir.
> - Eylem yöntemi yürütmesini sarmalayan **eylem** filtresi. Bu filtre, eylem yöntemine ek veri sağlama, dönüş değerini İnceleme veya eylem yönteminin yürütülmesini iptal etme gibi ek işlemler gerçekleştirebilir.
> - ActionResult nesnesinin yürütülmesini sarmalayan **sonuç** filtresi. Bu filtre, HTTP yanıtını değiştirme gibi sonucun ek işlemesini gerçekleştirebilir.
> - Yetkilendirme filtreleriyle başlayıp sonuç yürütülene kadar, eylem yönteminde bir yerde oluşturulan işlenmeyen bir özel durum varsa yürütülen **özel durum** filtresi. Özel durum filtreleri, günlüğe kaydetme veya hata sayfası görüntüleme gibi görevler için kullanılabilir.
> 
> Filtreler sağlayıcıları hakkında daha fazla bilgi için lütfen şu MSDN bağlantısını ziyaret edin: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>MVC müzik deposu Uygulama günlüğü özelliği hakkında

Bu müzik deposu çözümünde, Şu alanlarla, **ActionLog**adlı site günlüğü için yeni bir veri modeli tablosu vardır: bir isteği alan denetleyicinin adı, eylem, istemci IP 'Si ve zaman damgası.

![Veri modeli. ActionLog tablosu.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Veri modeli. ActionLog tablosu.")

*Veri modeli-ActionLog tablosu*

Çözüm, **Mvcmusicmağazalarında/görünümlerde/ActionLog**dizininde bulunan eylem günlüğü için BIR ASP.NET MVC görünümü sağlar:

![Eylem günlüğü görünümü](aspnet-mvc-4-custom-action-filters/_static/image2.png "Eylem günlüğü görünümü")

*Eylem günlüğü görünümü*

Bu yapı söz konusu olduğunda, tüm işler denetleyicinin isteğini kesintiye uğratma ve özel filtreleme kullanılarak günlüğe kaydetme işlemlerini gerçekleştirmeyecektir.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>Görev 1-bir denetleyicinin Isteğini yakalamak için özel bir filtre oluşturma

Bu görevde, günlüğe kaydetme mantığını içerecek bir özel filtre öznitelik sınıfı oluşturacaksınız. Bu amaçla, ASP.NET MVC **ActionFilterAttribute** sınıfını genişletecektir ve **IActionFilter**arabirimini uygulamalısınız.

> [!NOTE]
> **ActionFilterAttribute** tüm öznitelik filtrelerinin taban sınıfıdır. Bu, denetleyici eyleminin yürütmeden sonra ve öncesinde belirli bir mantığı yürütmek için aşağıdaki yöntemleri sağlar:
> 
> - **OnActionExecuting**(ActionExecutingContext filtercontext): eylem yöntemi çağrılmadan hemen önce.
> - **Onactionyürütüldü**(ActionExecutedContext filtercontext): eylem yöntemi çağrıldıktan sonra ve sonuç yürütülmeden önce (oluşturma tamamlanmadan önce).
> - **OnResultExecuting**(ResultExecutingContext filtercontext): sonuç yürütülmeden hemen önce (görüntü işleme öncesi).
> - **OnResultExecuted**(ResultExecutedContext filtercontext): sonuç yürütüldükten sonra (görünüm işlendiğinde).
> 
> Bu yöntemlerin herhangi birini türetilmiş bir sınıfa geçersiz kılarak kendi filtreleme kodunuzu çalıştırabilirsiniz.

1. **\Source\ex01-loggingactions\begin** klasöründe bulunan **BEGIN** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
      > 
      > Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Filtreler klasörüne yeni C# bir sınıf ekleyin ve *CustomActionFilter.cs*olarak adlandırın. Bu klasör tüm özel filtreleri depolayacaktır.
3. **CustomActionFilter.cs** açın ve **System. Web. Mvc** ve **Mvcmusicstore. model** ad alanlarına bir başvuru ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-Ex1-CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. **ActionFilterAttribute** ' dan **CustomActionFilter** sınıfını devralma ve **CustomActionFilter** sınıfını **IActionFilter** arabirimini uygulamasına getirme.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. **CustomActionFilter** sınıfının, **OnActionExecuting** metodunu geçersiz kılmasını ve filtrenin yürütmesini günlüğe kaydetmek için gerekli mantığı eklemesini sağlayın. Bunu yapmak için, aşağıdaki vurgulanmış kodu **CustomActionFilter** sınıfına ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-Ex1-LoggingActions*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **OnActionExecuting** yöntemi yeni bir ActionLog kaydı eklemek için **Entity Framework** kullanıyor. Bu, **filtre bağlamından**bağlam bilgileriyle yeni bir varlık örneği oluşturur ve doldurur.
    > 
    > [MSDN](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)'de **ControllerContext** sınıfı hakkında daha fazla bilgi edinebilirsiniz.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>Görev 2-mağaza denetleyicisi sınıfına bir kod yakalayıcısı ekleme

Bu görevde, ekleme bu özel filtreyi, günlüğe kaydedilecek tüm denetleyici sınıfları ve denetleyici eylemlerine göre ekleyeceksiniz. Bu alıştırmanın amacına yönelik olarak, mağaza denetleyicisi sınıfının günlüğü olacaktır.

**Actionlogfilterattribute** özel filtresinden **yürütülen onactionthe** yöntemi, eklenen bir öğe çağrıldığında çalışır.

Belirli bir denetleyici yöntemini ele almak da mümkündür.

1. **Mvcmusicstore\controllers** konumundaki **storecontroller** ' i açın ve **Filtreler** ad alanına bir başvuru ekleyin:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. Sınıf bildiriminden önce **[CustomActionFilter]** özniteliğini ekleyerek özel filtre **CustomActionFilter** ' yi **storecontroller** sınıfına ekleyin.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > Bir filtre bir denetleyici sınıfına eklendiğinde, tüm eylemleri de eklenir. Filtreyi yalnızca bir eylemler kümesi için uygulamak istiyorsanız, her birine **[CustomActionFilter]** ekleme yapmanız gerekir:
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, günlüğe kaydetme filtresinin çalıştığını test edersiniz. Uygulamayı başlatacak ve mağazayı ziyaret edecek ve sonra günlüğe kaydedilen etkinlikleri kontrol edersiniz.

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. Günlük görünümü başlangıç durumunu görmek için **/ActionLog** adresine gidin:

    ![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image3.png "Sayfa etkinlikten önce günlük izleyici durumu")

    *Sayfa etkinlikten önce günlük izleyici durumu*

   > [!NOTE]
   > Varsayılan olarak, menü için mevcut tarzlar alınırken oluşturulan bir öğeyi her zaman gösterir.
   > 
   > Kolaylık sağlamak için, uygulama her çalıştırıldığında **ActionLog** tablosunu temizliyoruz, böylece yalnızca belirli bir görevin doğrulamasının günlükleri gösterilir.
   > 
   > Mağaza denetleyicisi içinde yürütülen tüm eylemler için bir geçmiş günlüğü kaydetmek üzere **oturum\_start** yönteminden ( **Global. asax** sınıfında) aşağıdaki kodu kaldırmanız gerekebilir.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.
4. **/ActionLog** ' a gidin ve günlük boşsa, sayfayı yenilemek için **F5** tuşuna basın. Ziyaretlerinizin izlendiğinden emin olun:

    ![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image4.png "Etkinlik günlüğe kaydedilen eylem günlüğü")

    *Etkinlik günlüğe kaydedilen eylem günlüğü*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>Alıştırma 2: birden çok eylem filtresini yönetme

Bu alıştırmada, StoreController sınıfına ikinci bir özel eylem filtresi ekleyecek ve her iki filtrenin de gerçekleştirileceği belirli bir sırayı tanımlayacaksınız. Daha sonra, filtreyi Global olarak kaydetmek için kodu güncelleşolursunuz.

Filtrelerin yürütme sırası tanımlanırken dikkate almanız gereken farklı seçenekler vardır. Örneğin, Order özelliği ve filtrelerin kapsam:

Filtrelerin her biri için bir **kapsam** tanımlayabilirsiniz, örneğin, **Denetleyici kapsamında**çalıştırmak için tüm eylem filtrelerini ve **genel kapsamda**çalıştırılacak tüm yetkilendirme filtrelerini kapsam yapabilirsiniz. Kapsamların tanımlı bir yürütme sırası vardır.

Ayrıca, her eylem filtresinin, filtrenin kapsamındaki yürütme sırasını belirlemede kullanılan bir Order özelliği vardır.

Özel eylem filtreleri yürütme sırası hakkında daha fazla bilgi için lütfen şu MSDN makalesini ziyaret edin: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>Görev 1: yeni bir özel eylem filtresi oluşturma

Bu görevde, StoreController sınıfına eklenecek yeni bir özel eylem filtresi oluşturacaksınız ve filtrelerin yürütme sırasının nasıl yönetileceğini öğrenirsiniz.

1. **\Source\Ex02-ManagingMultipleActionFilters\Begin** klasöründe bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

    1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
    2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
    3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

        > [!NOTE]
        > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
        > 
        > Daha fazla bilgi için şu makaleye bakın: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Filtreler klasörüne yeni C# bir sınıf ekleyin ve *MyNewCustomActionFilter.cs* olarak adlandırın
3. **MyNewCustomActionFilter.cs** açın ve **System. Web. Mvc** ve **Mvcmusicstore. modeller** ad alanına bir başvuru ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-EX2-MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. Varsayılan sınıf bildirimini aşağıdaki kodla değiştirin.

    (Kod parçacığı- *ASP.NET MVC 4 özel eylem filtreleri-EX2-MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > Bu özel eylem filtresi, bir önceki alıştırmada oluşturduğdan neredeyse aynıdır. Ana fark, hangi filtrenin günlüğe kaydedildiğini belirlemek için bu yeni sınıf ' adı ile güncelleştirilmiş *&quot;&quot;özniteliği tarafından kaydedilen* sahip olabilir.

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>2\. görev: StoreController sınıfına yeni bir kod yakalayıcısı ekleme

Bu görevde, StoreController sınıfına yeni bir özel filtre ekleyecek ve iki filtrenin birlikte nasıl çalıştığını doğrulamak için çözümü çalıştıracaksınız.

1. **Mvcmusicstore\controllers** dizininde bulunan **storecontroller** sınıfını açın ve aşağıdaki kodda gösterildiği gibi yeni özel filtre MyNewCustomActionFilter **storecontroller** sınıfına ekleyin.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. Şimdi, bu iki özel eylem filtrelerinin nasıl çalıştığını görmek için uygulamayı çalıştırın. Bunu yapmak için **F5** tuşuna basın ve uygulama başlatılana kadar bekleyin.
3. Günlük görünümü başlangıç durumunu görmek için **/ActionLog** ' a gidin.

    ![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image5.png "Sayfa etkinlikten önce günlük izleyici durumu")

    *Sayfa etkinlikten önce günlük izleyici durumu*
4. Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.
5. Bu süreyi denetleyin; ziyaretleriniz iki kez izleniyor: **Storagecontroller** sınıfına eklediğiniz her bir özel eylem filtresi için bir kez.

    ![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image6.png "Etkinlik günlüğe kaydedilen eylem günlüğü")

    *Etkinlik günlüğe kaydedilen eylem günlüğü*
6. Tarayıcıyı kapatın.

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>Görev 3: filtre sıralamasını yönetme

Bu görevde, Order özelliğini kullanarak filtrelerin yürütme sırasını yönetmeyi öğreneceksiniz.

1. **Mvcmusicstore\controllers** yolunda bulunan **storecontroller** sınıfını açın ve **Order** özelliğini aşağıda gösterildiği gibi her iki filtrede de belirtin.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. Şimdi, Order özelliğinin değerine bağlı olarak filtrelerin nasıl yürütüleceğini doğrulayın. En küçük sıra değeri (**CustomActionFilter**) ile filtrenin yürütülen ilk bir değer olduğunu göreceksiniz. **F5** tuşuna basın ve uygulama başlatılana kadar bekleyin.
3. Günlük görünümü başlangıç durumunu görmek için **/ActionLog** ' a gidin.

    ![Sayfa etkinlikten önce günlük izleyici durumu](aspnet-mvc-4-custom-action-filters/_static/image7.png "Sayfa etkinlikten önce günlük izleyici durumu")

    *Sayfa etkinlikten önce günlük izleyici durumu*
4. Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.
5. Bu zamanın, ilk olarak filtrelerin ' Order value: **CustomActionFilter** logs ' filtreleri tarafından sıralanmış olarak izlendiğini kontrol edin.

    ![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image8.png "Etkinlik günlüğe kaydedilen eylem günlüğü")

    *Etkinlik günlüğe kaydedilen eylem günlüğü*
6. Şimdi, filtrelerin sıra değerini güncelleyerek günlüğe kaydetme sırasının nasıl değiştiğini doğrulayacaksınız. **Storecontroller** sınıfında, aşağıda gösterildiği gibi filtrelerin sıra değerini güncelleştirin.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. **F5**tuşuna basarak uygulamayı yeniden çalıştırın.
8. Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.
9. Bu zamanın, **MyNewCustomActionFilter** filtresi tarafından oluşturulan günlüklerin önce göründüğünü kontrol edin.

    ![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image9.png "Etkinlik günlüğe kaydedilen eylem günlüğü")

    *Etkinlik günlüğe kaydedilen eylem günlüğü*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>Görev 4: filtreleri küresel olarak kaydetme

Bu görevde, yeni filtreyi (**MyNewCustomActionFilter**) genel bir filtre olarak kaydetmek için çözümü güncelleşolursunuz. Bunu yaptığınızda, uygulama yalnızca önceki görevde olduğu gibi, yalnızca StoreController içinde değil, uygulamada gerçekleştirilen tüm eylemler tarafından tetiklenir.

1. **Storecontroller** sınıfında [ **MyNewCustomActionFilter]** özniteliğini ve Order özelliğini **[CustomActionFilter]** öğesinden kaldırın. Aşağıdaki gibi görünmelidir:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. **Global. asax** dosyasını açın ve **uygulama\_start** metodunu bulun. Uygulamanın her başladığı her seferinde, **Filterconfig** sınıfında **registerglobalfilters** metodunu çağırarak genel filtrelerin kaydedildiğine dikkat edin.

    ![Global. asax içinde genel filtreleri kaydetme](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global. asax içinde genel filtreleri kaydetme")

    *Global. asax içinde genel filtreleri kaydetme*
3. **FilterConfig.cs** dosyasını **uygulama\_başlangıç** klasörü içinde açın.
4. System. Web. Mvc kullanarak bir başvuru ekleyin MvcMusicStore. Filters; kullanma uzayına.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. Özel filtrenizi ekleyerek **Registerglobalfilters** metodunu güncelleştirin. Bunu yapmak için vurgulanan kodu ekleyin:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. **F5**tuşuna basarak uygulamayı çalıştırın.
7. Menüdeki **tarzlardan** birine tıklayın ve kullanılabilir albüme göz atmak gibi bazı eylemler gerçekleştirin.
8. Artık **[MyNewCustomActionFilter]** ' ın HomeController ve ActionLogController 'e de eklenmiş olduğunu denetleyin.

    ![Etkinlik günlüğe kaydedilen eylem günlüğü](aspnet-mvc-4-custom-action-filters/_static/image11.png "Etkinlik günlüğe kaydedilen eylem günlüğü")

    *Genel etkinlik günlüğe kaydedilen eylem günlüğü*

> [!NOTE]
> Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak özel eylemleri yürütmek için bir eylem filtresinin nasıl genişletileceğini öğrendiniz. Ayrıca, sayfa denetleyicilerinize herhangi bir filtrenin nasıl ekleneceğini öğrendiniz. Aşağıdaki kavramlar kullanıldı:

- ASP.NET MVC ActionFilterAttribute sınıfıyla özel eylem filtreleri oluşturma
- ASP.NET MVC denetleyicilerine filtre ekleme
- Order özelliğini kullanarak filtre sıralamasını yönetme
- Filtreleri küresel olarak kaydetme

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma

1. [Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure portal oturum açın")

    *Windows Azure 'da oturum açma Yönetim Portalı*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-custom-action-filters/_static/image18.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-custom-action-filters/_static/image19.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](aspnet-mvc-4-custom-action-filters/_static/image20.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-custom-action-filters/_static/image22.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.

    ![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-custom-action-filters/_static/image23.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-custom-action-filters/_static/image24.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-custom-action-filters/_static/image26.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *Değişiklikleri Onayla*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](aspnet-mvc-4-custom-action-filters/_static/image29.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](aspnet-mvc-4-custom-action-filters/_static/image30.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](aspnet-mvc-4-custom-action-filters/_static/image31.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın.

     ![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-custom-action-filters/_static/image33.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](aspnet-mvc-4-custom-action-filters/_static/image34.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](aspnet-mvc-4-custom-action-filters/_static/image36.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Ek C: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-custom-action-filters/_static/image37.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-custom-action-filters/_static/image38.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-custom-action-filters/_static/image39.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-custom-action-filters/_static/image40.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-custom-action-filters/_static/image41.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-custom-action-filters/_static/image42.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
