---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 temelleri | Microsoft Docs
author: rick-anderson
description: Bu uygulamalı laboratuvar, ASP.NET MV 'ın nasıl kullanılacağı hakkında adım adım bir öğretici uygulama olan MVC (model görünüm denetleyicisi) müzik mağazasını temel alır.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598821"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 Temelleri

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

Bu uygulamalı laboratuvar, ASP.NET MVC ve Visual Studio 'Nun nasıl kullanılacağını anlatan bir öğretici uygulaması olan MVC (model görünüm denetleyicisi) müzik mağazasını temel alır. Laboratuvarın tamamında, bu teknolojilerin birlikte kullanılması basitlik, ancak gücünü öğrenirsiniz. Basit bir uygulamayla başlayacaksınız ve tamamen işlevsel bir ASP.NET MVC 4 Web uygulamasına sahip olana kadar bu uygulamayı oluşturacaksınız.

Bu laboratuvar ASP.NET MVC 4 ile birlikte kullanılabilir.

Öğretici uygulamasının ASP.NET MVC 3 sürümünü araştırmak isterseniz, bunu [MVC-müzik-Store](https://github.com/evilDave/MVC-Music-Store)' da bulabilirsiniz.

Bu uygulamalı laboratuvar, geliştiricinin HTML ve JavaScript gibi web geliştirme teknolojilerinde deneyimle karşılaşdığını varsayar.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 temelleri](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)adresinde bulunabilir.

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>Müzik Mağazası uygulaması

Bu laboratuvarda oluşturulacak müzik deposu Web uygulaması üç ana bölümden oluşur: alışveriş, kullanıma alma ve yönetim. Ziyaretçiler, albümlere göre Albümler 'e göz atabilir, sepetlerine Albümler ekleyebilir, bunların seçimini gözden geçirebilir ve son olarak oturum açmaya ve siparişi tamamlamaya devam edebilir. Ayrıca, mağaza yöneticileri, kullanılabilir albümleri ve bunların ana özelliklerini yönetebilecektir.

![Müzik Mağazası ekranları](aspnet-mvc-4-fundamentals/_static/image1.png "Müzik Mağazası ekranları")

*Müzik Mağazası ekranları*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

Müzik deposu uygulaması, bir uygulamayı üç ana bileşene ayıran mimari bir **model olan model görünüm denetleyicisi (MVC)** kullanılarak oluşturulur:

- **Modeller**: model nesneleri, uygulamanın etki alanı mantığını uygulayan parçalarından oluşur. Genellikle model nesneleri ayrıca bir veritabanında model durumunu alır ve depolar.
- **Görünümler:** Görünümler, uygulamanın kullanıcı arabirimini (UI) görüntüleyen bileşenlerdir. Bu UI, genellikle model verilerinden oluşturulur. Bir örnek, bir albüm nesnesinin geçerli durumuna bağlı olarak metin kutularını ve bir açılan listeyi görüntüleyen Albümler düzenleme görünümüdür.
- **Denetleyiciler:** Denetleyiciler kullanıcı etkileşimini işleyen, modeli düzenleyen ve son olarak Kullanıcı arabirimini işlemek için bir görünüm seçtiğiniz bileşenlerdir. Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici ise kullanıcı girişini ve etkileşimini işler ve bunlara yanıt verir.

MVC deseninin uygulamanın farklı yönlerini (Giriş mantığı, iş mantığı ve Kullanıcı arabirimi mantığı) ayıran uygulamalar oluşturmanıza yardımcı olur. bu öğeler arasında gevşek bir bağlantısı sağlanır. Bu ayrım, uygulamanın her seferinde bir kısmına odaklanmanıza olanak verdiğinden, bir uygulama oluşturduğunuzda karmaşıklığı yönetmenize yardımcı olur. Ayrıca, MVC deseninin uygulamaları test etmek için test odaklı geliştirme (TDD) kullanımını teşvik ve ayrıca uygulamaları test etmek kolaylaşır.

**ASP.NET MVC** framework, ASP.NET MVC tabanlı Web uygulamaları oluşturmak için ASP.NET Web Forms düzenine bir alternatif sağlar. **ASP.NET MVC** Framework, çekirdek .NET Framework 'ün tüm gücünden yararlanmak için ana sayfalar ve üyelik tabanlı kimlik doğrulama gibi mevcut ASP.NET özellikleriyle tümleşik olan hafif ve yüksek düzeyde bir sunum çerçevesidir. Zaten kullandığınız tüm kitaplıklar ASP.NET MVC 4 ' te de kullanılabildiğinden, ASP.NET Web Forms zaten biliyorsanız, bu faydalıdır.

Ayrıca, bir MVC uygulamasının üç ana bileşeni arasında gevşek bir dağıtım paralel geliştirmeyi de yükseltir. Örneğin, bir geliştirici görünümde çalışırken, ikinci bir geliştirici denetleyici mantığı üzerinde çalışabilir ve üçüncü bir geliştirici modeldeki iş mantığına odaklanabilir.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Müzik Mağazası uygulaması öğreticisini temel alarak sıfırdan bir ASP.NET MVC uygulaması oluşturma
- URL 'Leri işlemek için sitenin ana sayfasına ve ana işlevselliğine göz atmak üzere denetleyiciler ekleyin
- Stili ile birlikte görüntülenecek içeriği özelleştirmek için bir görünüm ekleyin
- Veri ve etki alanı mantığını içerecek ve yönetecek model sınıfları ekleme
- Denetleyici eylemlerden görünüm şablonlarına bilgi geçirmek için model görüntüleme modelini kullanın
- Internet uygulamaları için ASP.NET MVC 4 yeni şablonunu keşfet

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web Için Visual Studio 2012 Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

**Kod parçacıklarını yükleme**

Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır. Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:

1. [Alıştırma 1: MusicStore ASP.NET MVC web uygulaması projesi oluşturma](#Exercise1)
2. [Alıştırma 2: denetleyici oluşturma](#Exercise2)
3. [Alıştırma 3: bir denetleyiciye parametre geçirme](#Exercise3)
4. [Alıştırma 4: görünüm oluşturma](#Exercise4)
5. [Alıştırma 5: bir görünüm modeli oluşturma](#Exercise5)
6. [Alıştırma 6: görünümdeki parametreleri kullanma](#Exercise6)
7. [Alıştırma 7: ASP.NET MVC 4 yeni şablonu etrafında bir lap](#Exercise7)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>Alıştırma 1: MusicStore ASP.NET MVC web uygulaması projesi oluşturma

Bu alıştırmada, Web için Visual Studio 2012 Express ve ana klasör kuruluşunun yanı sıra bir ASP.NET MVC uygulaması oluşturmayı öğreneceksiniz. Ayrıca, yeni bir denetleyici eklemeyi ve uygulamanın giriş sayfasında basit bir dize görüntülemeyi öğreneceksiniz.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>Görev 1-ASP.NET MVC web uygulaması projesi oluşturma

1. Bu görevde, MVC Visual Studio şablonunu kullanarak boş bir ASP.NET MVC uygulama projesi oluşturacaksınız. **Web için vs Express**başlatın.
2. **Dosya** menüsünde **Yeni proje**' ye tıklayın.
3. **Yeni proje** iletişim kutusunda, **Visual C#,** **Web** Template List altında bulunan **ASP.NET MVC 4 Web uygulaması** proje türünü seçin.
4. **Adı** *Mvcmusicstore*olarak değiştirin.
5. Çözümün konumunu, bu alıştırmanın kaynak klasöründeki yeni bir **Başlangıç** klasörü içinde ayarlayın, örneğin **[-hol-Path] \Source\ex01-creatingmusicstoreproject\begın**. **Tamam**’a tıklayın.

    ![Yeni proje oluştur Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image2.png "Yeni proje oluştur Iletişim kutusu")

    *Yeni proje oluştur Iletişim kutusu*
6. **Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **temel** şablonu seçin ve **Görünüm altyapısının** **seçili olduğundan emin olun.** **Tamam**’a tıklayın.

    ![Yeni ASP.NET MVC 4 projesi Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image3.png "Yeni ASP.NET MVC 4 projesi Iletişim kutusu")

    *Yeni ASP.NET MVC 4 projesi Iletişim kutusu*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>Görev 2-çözüm yapısını keşfetme

ASP.NET MVC Framework, MVC modelini destekleyen Web uygulamaları oluşturmanıza yardımcı olan bir Visual Studio proje şablonu içerir. Bu şablon, gerekli klasörler, öğe şablonları ve yapılandırma dosyası girişleriyle yeni bir ASP.NET MVC web uygulaması oluşturur.

Bu görevde, ilgili öğeleri ve bunların ilişkilerini anlamak için çözüm yapısını inceleyeceksiniz. ASP.NET MVC çerçevesi varsayılan olarak yapılandırma&quot; yaklaşımına &quot;bir kural kullandığından ve klasör adlandırma kurallarına göre bazı varsayılan varsayımlar yaptığından, aşağıdaki klasörler tüm ASP.NET MVC uygulamasına dahil edilmiştir.

1. Proje oluşturulduktan sonra, sağ taraftaki Çözüm Gezgini oluşturulan klasör yapısını gözden geçirin:

    ![Çözüm Gezgini MVC klasör yapısı ASP.NET](aspnet-mvc-4-fundamentals/_static/image4.png "Çözüm Gezgini MVC klasör yapısı ASP.NET")

    *Çözüm Gezgini MVC klasör yapısı ASP.NET*

   1. **Denetleyici**. Bu klasör denetleyici sınıflarını içerir. MVC tabanlı bir uygulamada, denetleyiciler son kullanıcı etkileşimini işlemekten, modeli işlemeye ve sonunda Kullanıcı arabirimini işlemek için bir görünüm seçmeye sorumludur.

       > [!NOTE]
       > MVC çerçevesi, tüm denetleyicilerin adlarının &quot;denetleyicisi&quot;(örneğin, HomeController, LoginController veya ProductController) bitmesini gerektirir.
   2. **Modeller**. Bu klasör, MVC web uygulaması için uygulama modelini temsil eden sınıflar için sağlanır. Bu genellikle nesneleri tanımlayan kodu ve veri deposuyla etkileşim kurma mantığını içerir. Genellikle, gerçek model nesneleri ayrı sınıf kitaplıklarında olacaktır. Ancak, yeni bir uygulama oluşturduğunuzda, sınıfları dahil edebilir ve ardından bunları geliştirme döngüsünün sonraki bir noktasında ayrı sınıf kitaplıklarına taşıyabilirsiniz.
   3. **Görünümler**. Bu klasör, uygulamanın kullanıcı arabirimini görüntülemekten sorumlu olan görünümler için önerilen konumdur. Görünümler, işleme görünümleriyle ilgili diğer dosyalara ek olarak. aspx,. ascx,. cshtml ve. Master dosyalarını kullanır. Görünümler klasörü her denetleyici için bir klasör içerir; klasör, denetleyici adı ön eki ile adlandırılır. Örneğin, **HomeController**adlı bir denetleyiciniz varsa, görünümler klasörü Home adlı bir klasör içerir. Varsayılan olarak, ASP.NET MVC çerçevesi bir görünüm yüklediğinde, Views\controllerName klasöründe istenen görünüm adına sahip bir. aspx dosyası arar (**Görünümler [ControllerName] [action]. aspx**) veya Razor görünümleri Için (**Görünümler [ControllerName] [action]. cshtml**).

      > [!NOTE]
      > Daha önce listelenen klasörlere ek olarak, MVC web uygulaması genel URL yönlendirme varsayılanlarını ayarlamak için **Global. asax** dosyasını kullanır ve uygulamayı yapılandırmak için **Web. config** dosyasını kullanır.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>Görev 3-HomeController ekleme

MVC çerçevesini kullanmayan ASP.NET uygulamalarında, Kullanıcı etkileşimi sayfalar etrafında düzenlenir ve bu sayfalardaki olayları oluşturma ve işleme. Buna karşılık, ASP.NET MVC uygulamalarıyla Kullanıcı etkileşimi denetleyiciler ve eylem yöntemleri etrafında düzenlenmiştir.

Diğer taraftan, ASP.NET MVC çerçevesi, denetleyicileri olarak adlandırılan sınıflarla URL 'Leri eşler. Denetleyiciler gelen istekleri işler, Kullanıcı giriş ve etkileşimlerini işler, uygun uygulama mantığını yürütür ve istemciye geri gönderme (HTML görüntüleme, bir dosyayı indirme, farklı bir URL 'ye yönlendirme vb.) yanıtını belirleme. HTML görüntüleme durumunda, bir denetleyici sınıfı genellikle istek için HTML biçimlendirmesi oluşturmak üzere ayrı bir görünüm bileşeni çağırır. Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici ise kullanıcı girişini ve etkileşimini işler ve bunlara yanıt verir.

Bu görevde, müzik deposu sitesinin giriş sayfasına URL 'Leri işleyecek bir denetleyici sınıfı ekleyeceksiniz.

1. Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutu ' nı seçin:

    ![Denetleyici komutu ekleme](aspnet-mvc-4-fundamentals/_static/image5.png "Denetleyici komutu ekleme")

    *Denetleyici komutu Ekle*
2. **Denetleyici Ekle** iletişim kutusu görünür. Denetleyiciyi *HomeController* olarak adlandırın ve **Ekle**tuşuna basın.

    ![Denetleyici Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image6.png "Denetleyici Ekle Iletişim kutusu")

    *Denetleyici Ekle Iletişim kutusu*
3. **HomeController.cs** dosyası **denetleyiciler** klasöründe oluşturulur. **HomeController** 'ın Dizin eyleminde bir dize döndürmesini sağlamak Için, **index** metodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex1 HomeController dizini*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, uygulamayı bir Web tarayıcısında deneyirsiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın. Proje derlenir ve yerel IIS Web sunucusu başlatılır. Yerel IIS Web sunucusu, Web sunucusunun URL 'sini işaret eden bir Web tarayıcısını otomatik olarak açar.

    ![Web tarayıcısında çalışan uygulama](aspnet-mvc-4-fundamentals/_static/image7.png "Web tarayıcısında çalışan uygulama")

    *Web tarayıcısında çalışan uygulama*

    > [!NOTE]
    > Yerel IIS Web sunucusu, bir rastgele boş bağlantı noktası numarasında Web sitesini çalıştırır. Yukarıdaki şekilde, site `http://localhost:50103/`çalışıyor, bu nedenle 50103 numaralı bağlantı noktasını kullanıyor. Bağlantı noktası numaranız farklılık gösterebilir.
2. Tarayıcıyı kapatın.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>Alıştırma 2: denetleyici oluşturma

Bu alıştırmada, müzik Mağazası uygulamasının basit işlevlerini uygulamak için denetleyiciyi nasıl güncelleştireceğinizi öğreneceksiniz. Bu denetleyici, aşağıdaki belirli isteklerin her birini işlemek için eylem yöntemleri tanımlayacaktır:

- Müzik deposundaki müzik tarzlarındaki bir listeleme sayfası
- Belirli bir tarz için tüm müzik albümlerini listeleyen bir tarayıcı sayfası
- Belirli bir müzik albümünden ilgili bilgileri gösteren Ayrıntılar sayfası

Bu alıştırma kapsamında, bu eylemler şimdi yalnızca bir dize döndürür.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>Görev 1-yeni bir StoreController sınıfı ekleme

Bu görevde yeni bir denetleyici ekleyeceksiniz.

1. Zaten açık değilse **2012 Web için vs Express**başlatın.
2. **Dosya** menüsünde **Proje Aç**' ı seçin. Proje Aç iletişim kutusunda **Source\ex02-creatingacontroller\begin**öğesine göz atın, **Başlat. sln** ' yi seçin ve **Aç**' a tıklayın. Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. Yeni denetleyiciyi ekleyin. Bunu yapmak için Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutunu seçin. **Denetleyici adını** *storecontroller*olarak değiştirin ve **Ekle**' ye tıklayın.

    ![Denetleyici Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image8.png "Denetleyici Ekle Iletişim kutusu")

    *Denetleyici Ekle Iletişim kutusu*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>Görev 2-StoreController 'ın eylemlerini değiştirme

Bu görevde, **Eylemler**olarak adlandırılan denetleyici yöntemlerini değiştirirsiniz. Eylemler, URL isteklerini işlemekten ve tarayıcıya geri gönderilmesi gereken içeriği veya URL 'YI çağıran kullanıcıya göre belirlenir.

1. **Storecontroller** sınıfının bir **Dizin** yöntemi zaten var. Müzik mağazasının tüm tarzını listeleyen sayfayı uygulamak için bu laboratuvarın ilerleyen kısımlarında kullanacaksınız. Şimdilik, **index** metodunu Store. Index ()&quot;bir dize &quot;döndüren aşağıdaki kodla değiştirin.

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-EX2 StoreController dizini*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. **Gezinme** ve **ayrıntı** yöntemleri ekleyin. Bunu yapmak için **Storecontroller**öğesine aşağıdaki kodu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-EX2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, uygulamayı bir Web tarayıcısında deneyirsiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje **giriş** sayfasında başlar. Her eylemin uygulamasını doğrulamak için URL 'YI değiştirin.

    1. **/Store**. **Store. Index ()&quot;'dan&quot;Merhaba** görürsünüz.
    2. **/Store/zat**. **Store. Gözatacaksınız&quot;Merhaba. ()&quot;** görürsünüz.
    3. **/Store/details**. **Store&quot;Hello. Details ()&quot;** görürsünüz.

        ![Storegözatmaya göz atma](aspnet-mvc-4-fundamentals/_static/image9.png "Storegözatmaya göz atma")

        *Tarama/Store/zat*
3. Tarayıcıyı kapatın.

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>Alıştırma 3: bir denetleyiciye parametre geçirme

Bu aşamada, denetleyicilerden sabit dizeler döndürmüştür. Bu alıştırmada, URL 'yi ve QueryString 'yi kullanarak bir denetleyiciye parametreleri nasıl geçitireceğinizi öğrenirsiniz ve sonra Yöntem eylemlerinin bir metinle tarayıcıya yanıt vermesini sağlayabilirsiniz.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>Görev 1-StoreController 'a tarz parametresi ekleniyor

Bu görevde, **Storecontroller**Içindeki **gözatam** eylemi yöntemine parametreleri göndermek için **QueryString** kullanacaksınız.

1. Zaten açık değilse, **Web için vs Express**başlatın.
2. **Dosya** menüsünde **Proje Aç**' ı seçin. Proje Aç iletişim kutusunda **Source\ex03-passingparameterstoacontroller\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın. Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. **Storecontroller** sınıfını açın. Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.
4. Belirli bir tarz için istek için bir dize parametresi ekleyerek, **gözatıcı** yöntemini değiştirin. ASP.NET MVC, çağrıldığında otomatik olarak herhangi bir QueryString veya form post parametrelerini bu eylem yöntemine iletir. Bunu yapmak için, aşağıdaki kodla birlikte, **Gözatılacak** yöntemi değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> Kullanıcıların JavaScript 'i/Store/gözatmaya benzer bir bağlantıyla ekleme almasını engelleyecek şekilde **HttpUtility. HtmlEncode** yardımcı programı yöntemini kullanıyorsunuz **musunuz? Tarz =&lt;betiği&gt;Window. Location = '[http://hackersite.com](http://hackersite.com)'&lt;/scrıpt&gt;** .
> 
> Daha fazla açıklama için lütfen [Bu MSDN makalesini](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)ziyaret edin.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Görev 2-uygulamayı çalıştırma

Bu görevde, uygulamayı bir Web tarayıcısında dener ve **tarz** parametresini kullanacaksınız.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje **giriş** sayfasında başlar. URL 'YI */Store/zat değiştirin mi? Tarzı = disco* , eylemin tarz parametresini aldığını doğrular.

    ![Göz atma StoreBrowseGenre = disco](aspnet-mvc-4-fundamentals/_static/image10.png "Göz atma StoreBrowseGenre = disco")

    */Store/zat Gözatılıyor musunuz? Tarz = disco*
3. Tarayıcıyı kapatın.

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>Görev 3-URL 'ye gömülü bir ID parametresi ekleme

Bu görevde, **Storecontroller**'ın **Ayrıntılar** eylem yöntemine bir **ID** parametresi geçirmek için **URL 'yi** kullanacaksınız. ASP.NET MVC 'nin varsayılan yönlendirme kuralı, eylem yöntemi adından sonra, **ID**adlı bir parametre olarak bir URL 'nin segmentini değerlendirmek için kullanılır. Eylem yönteminizin ID adlı parametresi varsa, ASP.NET MVC URL segmentini otomatik olarak parametre olarak size iletir. URL **deposu/Ayrıntılar/5**' de, **kimlik** **5**olarak yorumlanacaktır.

1. **Storecontroller**öğesinin **Details** metodunu, **ID**adlı bir **int** parametresi ekleyerek değiştirin. Bunu yapmak için, **Details** yöntemini aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex3 StoreController ayrıntıları yöntemi*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, uygulamayı bir Web tarayıcısında deney, **kimlik** parametresini kullanacaksınız.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje **giriş** sayfasında başlar. İşlemin ID parametresini aldığını doğrulamak için URL 'YI */Store/details/5* olarak değiştirin.

    ![StoreDetails5 gözatma](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 gözatma")

    *Tarama/Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>Alıştırma 4: görünüm oluşturma

Şimdiye kadar, denetleyici eylemlerinden dizeler döndürmüştür. Bu, denetleyicilerin nasıl çalıştığını anlamak için kullanışlı bir yoldur, ancak gerçek Web uygulamalarınızın nasıl derlendiğini değildir. Görünümler, şablon dosyaları kullanımıyla tarayıcıya geri HTML oluşturmaya yönelik daha iyi bir yaklaşım sağlayan bileşenlerdir.

Bu alıştırmada, genel HTML içeriği için bir şablon kurmak üzere bir düzen ana sayfası eklemeyi öğrenirsiniz, sitenin görünümünü ve hisyi iyileştirmek için bir stil sayfası ve son olarak HomeController 'ın HTML döndürmesini sağlayan bir görünüm şablonu.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>Görev 1-\_Layout. cshtml dosyasını değiştirme

**~/Views/Shared/\_Layout. cshtml** dosyası, Web sitesinin tamamında kullanılacak ortak HTML için bir şablon ayarlamanıza olanak sağlar. Bu görevde, ana sayfa ve depolama alanı bağlantılarıyla ortak bir üst bilgiyle bir düzen ana sayfası ekleyeceksiniz.

1. Zaten açık değilse, **Web için vs Express**başlatın.
2. **Dosya** menüsünde **Proje Aç**' ı seçin. Proje Aç iletişim kutusunda **Source\ex04-creatingaview\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın. Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. <strong>\_Layout. cshtml</strong> dosyası sitedeki tüm sayfalar için HTML kapsayıcı düzeni içerir. HTML yanıtı için <strong>&lt;html&gt;</strong> öğesini ve <strong>&lt;baş&gt;</strong> ve <strong>&lt;gövde&gt;</strong> öğelerini içerir. HTML gövdesi içindeki <strong>@RenderBody()</strong> , şablonları görüntüleme, Dinamik içerikle doldurabilebilecekler bölgelerini belirler.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. Sitedeki tüm sayfalarda giriş sayfası ve depolama alanı bağlantılarıyla ortak bir üst bilgi ekleyin. Bunu yapmak için, aşağıdaki kodu gövde&gt; deyimin altına ekleyin &lt;.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. Her sayfanın gövde bölümünü işlemek için bir div ekleyin. <strong>@RenderBody()</strong> şu vurgulanmış kodla değiştirin: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > Emin misiniz? Visual Studio 2012, yaygın olarak kullanılan kodu HTML, kod dosyaları ve daha fazlasını eklemenizi kolaylaştıran kod parçacıkları içerir! **&lt;div&gt;** yazarak deneyin ve tüm **div** etiketi eklemek için **Tab** tuşuna iki kez basın.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>Görev 2-CSS stil sayfası ekleme

Boş proje şablonu, yalnızca temel formları ve doğrulama iletilerini göstermek için kullanılan stilleri içeren çok kolay bir CSS dosyası içerir. Sitenin görünüm ve hisde gelişmesini sağlamak için ek CSS ve görüntüler (büyük olasılıkla tasarımcı tarafından sağlanıyor) kullanacaksınız.

Bu görevde, sitenin stillerini tanımlamak için bir CSS stil sayfası ekleyeceksiniz.

1. CSS dosyası ve görüntüleri, bu laboratuvarın **Source\assets\content** klasörüne dahildir. Bunları uygulamaya eklemek için, bir **Windows Gezgini** penceresinden içeriğini aşağıda gösterildiği gibi Web için Visual Studio Express **Çözüm Gezgini** sürükleyin:

    ![Stil içeriğini sürükleme](aspnet-mvc-4-fundamentals/_static/image12.png "Stil içeriğini sürükleme")

    *Stil içeriğini sürükleme*
2. **Site. css** dosyasını ve var olan bazı görüntüleri değiştirmeyi onaylamanız istenir bir uyarı iletişim kutusu görüntülenir. **Tüm öğelere Uygula** ' yı Işaretleyin ve **Evet**' e tıklayın.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>Görev 3-görünüm şablonu ekleme

Bu görevde, Bu alıştırmada eklenen düzen ana sayfasını ve CSS 'yi kullanacak HTML yanıtı oluşturmak için bir görünüm şablonu ekleyeceksiniz.

1. Sitenin giriş sayfasına göz atarken bir görünüm şablonu kullanmak için önce bir dize döndürmek yerine, **HomeController Dizin** yönteminin bir **Görünüm**döndürdüğünü belirtmeniz gerekir. **HomeController** sınıfını açın ve bir **ActionResult**döndürecek şekilde **Dizin** metodunu değiştirin ve **() görünümünü**geri döndürün.

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-EX4 HomeController dizini*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. Şimdi uygun bir görünüm şablonu eklemeniz gerekiyor. Bunu yapmak için, **Dizin** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle** **' yi** seçin. Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.

    ![Dizin yönteminin içinden bir görünüm ekleme](aspnet-mvc-4-fundamentals/_static/image13.png "Dizin yönteminin içinden bir görünüm ekleme")

    *Dizin yönteminin içinden bir görünüm ekleme*
3. Görünüm **Ekle** iletişim kutusu bir görünüm şablonu dosyası oluşturacak şekilde görünür. Varsayılan olarak, bu iletişim kutusu şablonu kullanacak eylem yöntemiyle eşleşecek şekilde görünüm şablonunun adını önceden doldurur. HomeController içindeki **Dizin** eylemi yöntemi Içinde **Görünüm Ekle** bağlam menüsünü kullandığınız için, **Görünüm Ekle** Iletişim kutusunun varsayılan görünüm adı olarak dizini vardır. **Ekle**'yi tıklatın.

    ![Görünüm Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image14.png "Görünüm Ekle Iletişim kutusu")

    *Görünüm Ekle Iletişim kutusu*
4. Visual Studio, **Views\home** klasörünün Içinde bir **Index. cshtml** görünüm şablonu oluşturur ve ardından açar.

    ![Ana Dizin görünümü oluşturuldu](aspnet-mvc-4-fundamentals/_static/image15.png "Ana Dizin görünümü oluşturuldu")

    *Ana Dizin görünümü oluşturuldu*

    > [!NOTE]
    > **Index. cshtml** dosyasının adı ve konumu geçerlidir ve varsayılan ASP.NET MVC adlandırma kurallarına uyar.
    > 
    > \Views\**Home** klasörü, denetleyici adıyla (**giriş** denetleyicisi) eşleşir. Görünüm şablonu adı (**Dizin**), görünümü görüntüleyen denetleyici eylemi yöntemiyle eşleşir.
    > 
    > Bu şekilde, ASP.NET MVC bir görünüm döndürmek için bu adlandırma kuralını kullanırken bir görünüm şablonunun adını veya konumunu açıkça belirtmek zorunda kalmaktan kaçınır.
5. Oluşturulan görünüm şablonu, daha önce tanımlanan **\_Layout. cshtml** şablonunu temel alır. ViewBag. title özelliğini **Home**olarak güncelleştirin ve ana içeriği aşağıdaki kodda gösterildiği gibi **giriş sayfası**olacak şekilde değiştirin:

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. Çözüm Gezgini **Mvcmusicstore** projesini seçin ve **F5** tuşuna basarak uygulamayı çalıştırın.

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>Görev 4: doğrulama

Önceki alıştırmada bulunan tüm adımları doğru bir şekilde gerçekleştirdiğinizi doğrulamak için aşağıdaki gibi ilerleyin:

Uygulama bir tarayıcıda açıldığında şunları unutmayın:

1. HomeController 'ın Dizin eylemi yöntemi, görünüm şablonu standart adlandırma kuralına uyduğundan, ' ın **Return View ()** olarak adlandırılan kod olsa da **\Views\home\ındex.cshtml** görünüm şablonunu buldu ve görüntülendi.
2. Giriş sayfasında **\Views\home\ındex.cshtml** görünüm şablonu içinde tanımlanan hoş geldiniz iletisi görüntülenir.
3. Giriş sayfası **\_Layout. cshtml** şablonunu kullanıyor ve bu nedenle hoş geldiniz iletisi standart site HTML düzeni içinde yer alır.

    ![Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü](aspnet-mvc-4-fundamentals/_static/image16.png "Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü")

    *Tanımlı LayoutPage ve Style kullanarak giriş dizini görünümü*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>Alıştırma 5: bir görünüm modeli oluşturma

Şimdiye kadar, görünümleriniz, sabit kodlanmış HTML 'yi görüntülemelidir, ancak dinamik Web uygulamaları oluşturmak için, görünüm şablonu denetleyiciden bilgi almalıdır. Bu amaç için kullanılan yaygın bir teknik, denetleyicinin uygun HTML yanıtını oluşturmak için gereken tüm bilgileri paketetmesine olanak tanıyan **ViewModel** deseninin yer aldığı bir yöntemdir.

Bu alıştırmada, ViewModel sınıfı oluşturmayı ve gerekli özellikleri eklemeyi öğreneceksiniz: depodaki tür tarzların sayısı ve bu tarzların listesi. Ayrıca, StoreController 'ı oluşturulan ViewModel kullanacak şekilde güncelleyebilir ve son olarak, sayfada bahsedilen özellikleri görüntüleyecek yeni bir görünüm şablonu oluşturacaksınız.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>Görev 1-ViewModel sınıfı oluşturma

Bu görevde, Depo tarzı listeleme senaryosunu uygulayacak bir ViewModel sınıfı oluşturacaksınız.

1. Zaten açık değilse, **Web için vs Express**başlatın.
2. **Dosya** menüsünde **Proje Aç**' ı seçin. Proje Aç iletişim kutusunda **Source\ex05-creatingaviewmodel\begın**konumuna gidin, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın. Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. ViewModel tutmak için **Viewmodeller** klasörü oluşturun. Bunu yapmak için, en üst düzey **Mvcmusicstore** projesine sağ tıklayın, **Ekle** ve **Yeni klasör**' i seçin.

    ![Yeni klasör ekleme](aspnet-mvc-4-fundamentals/_static/image17.png "Yeni klasör ekleme")

    *Yeni klasör ekleme*
4. Klasör *Viewmodellerini*adlandırın.

    ![Çözüm Gezgini Viewmodeller klasörü](aspnet-mvc-4-fundamentals/_static/image18.png "Çözüm Gezgini Viewmodeller klasörü")

    *Çözüm Gezgini Viewmodeller klasörü*
5. **ViewModel** sınıfı oluşturun. Bunu yapmak için, kısa süre önce oluşturulan **Viewmodeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe**' yi seçin. **Kod**altında, **sınıf** öğesini seçin ve dosyayı *StoreIndexViewModel.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.

    ![Yeni sınıf ekleme](aspnet-mvc-4-fundamentals/_static/image19.png "Yeni sınıf ekleme")

    *Yeni sınıf ekleme*

    ![Storeındexviewmodel sınıfı oluşturuluyor](aspnet-mvc-4-fundamentals/_static/image20.png "Storeındexviewmodel sınıfı oluşturuluyor")

    *Storeındexviewmodel sınıfı oluşturuluyor*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>Görev 2-ViewModel sınıfına özellikler ekleme

Beklenen HTML yanıtını oluşturmak için StoreController 'dan görünüm şablonuna geçirilecek iki parametre vardır: depodaki tür tarzların sayısı ve bu tarzların bir listesi.

Bu görevde, bu 2 özellikleri **Storeındexviewmodel** sınıfına ekleyeceksiniz: **numberoftarzlar** (bir tamsayı) ve **tarzlar** (dizeler listesi).

1. **Storeındexviewmodel** sınıfına **numberoftarzlar** ve **tarzlar** özellikleri ekleyin. Bunu yapmak için, aşağıdaki 2 satırı sınıf tanımına ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 Storeındexviewmodel özellikleri*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; set;}** gösterimi, otomatik olarak C#uygulanan özellikler özelliğini kullanır. Bir destek alanı bildirmek zorunda kalmadan özelliğin avantajlarını sağlar.

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>Görev 3-StoreController 'ı Storeındexviewmodel kullanacak şekilde güncelleştirme

**Storeındexviewmodel** sınıfı, bir yanıt oluşturmak Için **Storecontroller**'ın **Dizin** yönteminden bir görünüm şablonuna geçmesi gereken bilgileri saklar.

Bu görevde **Storecontroller** 'ı **Storeındexviewmodel**kullanacak şekilde güncelleşolursunuz.

1. **Storecontroller** sınıfını açın.

    ![StoreController sınıfı açılıyor](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController sınıfı açılıyor")

    *StoreController sınıfı açılıyor*
2. **Storecontroller**'Dan **Storeındexviewmodel** sınıfını kullanmak için **storecontroller** kodunun en üstüne aşağıdaki ad alanını ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 Storeındexviewmodel Viewmodeller kullanarak*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. **Storecontroller**'ın **Dizin** eylemi yöntemini, bir **storeındexviewmodel** nesnesi oluşturacak ve doldurabilmesi ve sonra bir HTML yanıtı oluşturacak şekilde bir görünüm şablonuna geçirmek üzere değiştirin.

    > [!NOTE]
    > Laboratuvar &quot;ASP.NET MVC modellerini ve veri erişimi&quot; bir veritabanından mağaza tarzları listesini alan kodu yazarsınız. Aşağıdaki kodda **Storeındexviewmodel**' i doldurmayacak bir kukla veri tarzı **listesi** oluşturacaksınız.
    > 
    > **Storeındexviewmodel** nesnesini oluşturup ayarladıktan sonra, **görüntüleme** yöntemine bir bağımsız değişken olarak geçirilir. Bu, görünüm şablonunun bir HTML yanıtı oluşturmak için bu nesneyi kullanacağını gösterir.
4. **Index** metodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-eX5 StoreController Dizin yöntemi*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> Hakkında bilginiz varsa C#, **bunu kullanmanın,** **ViewModel** değişkeninin geç bağlantılı olduğunu varsayabilirsiniz. Doğru değil- C# derleyici, **ViewModel** 'In **storeındexviewmodel**türünde olduğunu belirlemek için değişkene ne atacağınızı temel alarak tür çıkarımı kullanmaktır. Ayrıca, yerel **ViewModel** değişkenini bir **storeındexviewmodel** türü olarak derlerken derleme zamanı denetimi ve Visual Studio kod Düzenleyicisi desteği alırsınız.

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>Görev 4-Storeındexviewmodel kullanan bir görünüm şablonu oluşturma

Bu görevde, bir tür listesi görüntülemek için denetleyiciden geçirilen bir Storeındexviewmodel nesnesi kullanacak bir görünüm şablonu oluşturacaksınız.

1. Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle Iletişim kutusu** **Storeındexviewmodel** sınıfı hakkında bilgi sahibi olacak şekilde projeyi derlim. **Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.

    ![Projeyi oluşturma](aspnet-mvc-4-fundamentals/_static/image22.png "Projeyi oluşturma")

    *Projeyi oluşturma*
2. Yeni bir görünüm şablonu oluşturun. Bunu yapmak için, **Dizin** yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.

    ![Görünüm Ekleme](aspnet-mvc-4-fundamentals/_static/image23.png "Görünüm Ekleme")

    *Görünüm Ekleme*
3. Dosya **Ekle Iletişim kutusu** **storecontroller**'dan çağrıldığı için, bir **\Views\store\ındex.cshtml** dosyasında görünüm şablonunu varsayılan olarak ekler. Kesin olarak **yazılmış görünüm oluştur** onay kutusunu işaretleyin ve ardından **model sınıfı**olarak **storeındexviewmodel** ' i seçin. Ayrıca, seçilen görünüm altyapısının **Razor**olduğundan emin olun. **Ekle**'yi tıklatın.

    ![Görünüm Ekle Iletişim kutusu](aspnet-mvc-4-fundamentals/_static/image24.png "Görünüm Ekle Iletişim kutusu")

    *Görünüm Ekle Iletişim kutusu*

    **\Views\store\ındex.cshtml** görünüm şablonu dosyası oluşturulup açılır. Son adımda **Görünüm Ekle** iletişim kutusuna sunulan bilgilere bağlı olarak, görünüm şablonu, bir HTML yanıtı oluşturmak için kullanılacak veriler olarak bir **Storeındexviewmodel** örneği bekler. Şablonun ' de C#bir `ViewPage<musicstore.viewmodels.storeindexviewmodel>` devraldığını fark edeceksiniz.

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>Görev 5-görünüm şablonunu güncelleştirme

Bu görevde, sayfa içindeki sıra sayısını ve bunların adlarını almak için son görevde oluşturulan görünüm şablonunu güncelleşolursunuz.

> [!NOTE]
> Görünüm şablonu içinde kodu yürütmek için @ söz dizimini (genellikle &quot;kodu nugal&quot;olarak adlandırılır) kullanacaksınız.

1. **Index. cshtml** dosyasında, **Mağaza** klasörü içinde, kodunu aşağıdaki kodla değiştirin:

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. **Storeındexviewmodel** içinde tarz listesinin üzerinde döngü yapın ve **foreach** döngüsü kullanarak bir HTML **&lt;ul&gt;** listesi oluşturun.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. **F5** tuşuna basarak uygulamayı çalıştırın ve **/Store**'a gidin. **Storeındexviewmodel** nesnesine **storecontroller** ' dan görünüm şablonuna geçirilen tarzlar listesini görürsünüz.

    ![Tarzın bir listesini görüntülemeyi görüntüle](aspnet-mvc-4-fundamentals/_static/image26.png "Tarzın bir listesini görüntülemeyi görüntüle")

    *Tarzın bir listesini görüntülemeyi görüntüle*
4. Tarayıcıyı kapatın.

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>Alıştırma 6: görünümdeki parametreleri kullanma

Alıştırma 3 ' te, parametreleri denetleyiciye geçirme hakkında daha fazla öğrendiniz. Bu alıştırmada, bu parametreleri görünüm şablonunda nasıl kullanacağınızı öğreneceksiniz. Bu amaçla, ilk olarak verilerinizi ve etki alanı mantığınızı yönetmenize yardımcı olacak sınıfların model olarak tanıtılcaksınız. Ayrıca, URL yolları kodlaması gibi şeyleri endişelenmeden ASP.NET MVC uygulamasının içindeki sayfalara bağlantılar oluşturmayı öğreneceksiniz.

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>Görev 1-model sınıfları ekleme

Denetleyiciden görünüme bilgi geçirmek için oluşturulan ViewModel aksine, model sınıfları veri ve etki alanı mantığını içerecek ve yönetecek şekilde oluşturulmuştur. Bu görevde, şu kavramları temsil eden iki model sınıfı ekleyeceksiniz: **tarz** ve **Albüm**.

1. Zaten açık değilse, **Web için vs Express** başlatın
2. **Dosya** menüsünde **Proje Aç**' ı seçin. Proje Aç iletişim kutusunda **Source\ex06-usingparametersinview\begin**öğesine göz atın, **BEGIN. sln** ' yi seçin ve **Aç**' a tıklayın. Alternatif olarak, önceki Alıştırmayı tamamladıktan sonra elde ettiğiniz çözüme devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. Bir **tarz** model sınıfı ekleyin. Bunu yapmak için **Çözüm Gezgini** **modeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin. **Kod**altında, **sınıf** öğesini seçin ve dosyayı *genre.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.

    ![Sınıf ekleme](aspnet-mvc-4-fundamentals/_static/image27.png "Sınıf ekleme")

    *Yeni öğe ekleme*

    ![Tarz model sınıfı Ekle](aspnet-mvc-4-fundamentals/_static/image28.png "Tarz model sınıfı Ekle")

    *Tarz model sınıfı Ekle*
4. Tarz sınıfına bir **Name** özelliği ekleyin. Bunu yapmak için aşağıdaki kodu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 tarzı*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. Önceki yordamın aynısını takip eden bir **Albüm** sınıfı ekleyin. Bunu yapmak için **Çözüm Gezgini** **modeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin. **Kod**altında, **sınıf** öğesini seçin ve dosyayı *Album.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.
6. Albüm sınıfına iki özellik ekleyin: **tarz** ve **başlık**. Bunu yapmak için aşağıdaki kodu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 albüm*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>Görev 2-StoreBrowseViewModel ekleme

Bu görevde bir **StoreBrowseViewModel** , seçilen bir tarz Ile eşleşen albümleri göstermek için kullanılacaktır. Bu görevde, bu sınıfı oluşturacak ve ardından **tarzını** ve **albümün**listesini işlemek için iki özellik ekleyeceksiniz.

1. Bir **StoreBrowseViewModel** sınıfı ekleyin. Bunu yapmak için **Çözüm Gezgini** **viewmodeller** klasörüne sağ tıklayın, **Ekle** ' yi ve ardından **Yeni öğe** seçeneğini belirleyin. **Kod**altında, **sınıf** öğesini seçin ve dosyayı *StoreBrowseViewModel.cs*olarak adlandırın, ardından **Ekle**' ye tıklayın.
2. **StoreBrowseViewModel** sınıfındaki modellere bir başvuru ekleyin. Bunu yapmak için şu ad alanını kullanarak şunu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. **StoreBrowseViewModel** sınıfına iki özellik ekleyin: **tarz** ve **Albümler**. Bunu yapmak için aşağıdaki kodu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> **Liste&lt;albüm&gt;** nedir?: Bu tanım, bu **listedeki** öğelerin ait olduğu türü **(veya** alt öğelerinden herhangi biri **) kısıtlayan t** **&gt;türü&lt;** kullanılır.
> 
> Sınıf veya yöntem bildirilmeden ve istemci kodu tarafından örneklendirilene kadar bir veya daha fazla türün belirtimini erteleme sınıfları ve yöntemleri tasarlayabilme özelliği, C# **Genel türler**adlı dilin bir özelliğidir.
> 
> **Liste&lt;t&gt;** , **ArrayList** türünün genel eşdeğeridir ve **System. Collections. Generic** ad alanında kullanılabilir. **Genel türleri** kullanmanın avantajlarından biri, tür belirtilmesinden bu yana, bir **ArrayList**Ile yaptığınız gibi öğeleri **albüme** atama gibi tür denetleme işlemlerine gerek duymamak zorunda değilsiniz.

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>Görev 3-StoreController 'da yeni ViewModel kullanma

Bu görevde, yeni **StoreBrowseViewModel**kullanmak Için **Storecontroller**'ın **gezinme** ve **Ayrıntılar** eylem yöntemlerini değiştirirsiniz.

1. **Storecontroller** sınıfındaki modeller klasörüne bir başvuru ekleyin. Bunu yapmak için, **Çözüm Gezgini** **denetleyiciler** klasörünü genişletin ve **storecontroller** sınıfını açın. Ardından aşağıdaki kodu ekleyin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. **StoreViewBrowseController** sınıfını kullanmak Için, **gezinme** eylemi yöntemini değiştirin. Kukla verilerle bir tarz ve iki yeni albümler nesnesi oluşturacaksınız (bir sonraki uygulamalı laboratuvarda bir veritabanından gerçek veriler kullanacaksınız). Bunu yapmak için, aşağıdaki kodla birlikte, **Gözatılacak** yöntemi değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. **Ayrıntılar** eylem yöntemini **StoreViewBrowseController** sınıfını kullanacak şekilde değiştirin. **Görünüme**döndürülecek yeni bir **Albüm** nesnesi oluşturacaksınız. Bunu yapmak için, **Details** yöntemini aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 temelleri-Ex6 Ayrıntılar yöntemi*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>Görev 4-bir tarayıcı görünümü şablonu ekleme

Bu görevde, belirli bir tarz için bulunan albümleri göstermek üzere bir **tarama** görünümü ekleyeceksiniz.

1. Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle** iletişim kutusunun kullanılacak **ViewModel** sınıfını bilmesi için projeyi derlemeniz gerekir. **Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.
2. Bir **tarama** görünümü ekleyin. Bunu yapmak için **Storecontroller** 'ın **gözatmaya** yönelik eylem yöntemine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.
3. **Görünüm Ekle** Iletişim kutusunda görünüm adının **gözatmasını**doğrulayın. **Türü kesin belirlenmiş görünüm oluştur** onay kutusunu Işaretleyin ve **model sınıfı** açılan listesinden **StoreBrowseViewModel** öğesini seçin. Diğer alanları varsayılan değerlerine bırakın. Daha sonra **Ekle**'ye tıklayın.

    ![Bir tarama görünümü ekleme](aspnet-mvc-4-fundamentals/_static/image29.png "Bir tarama görünümü ekleme")

    *Bir tarama görünümü ekleme*
4. Görünüm şablonuna geçirilen **StoreBrowseViewModel** nesnesine erişmek için, denetimin bilgilerini görüntülemek üzere **Gözat. cshtml** 'yi değiştirin. Bunu yapmak için içeriği şu şekilde değiştirin: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde **, Gezinme yönteminin** Albümler **'e gözatamıyorum** eylemini alacağını test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Store/zat değiştirin mi? Tarz = disco** , eylemin Iki albüm döndürdüğünden emin olmak için.

    ![Store disco albümlerine göz atma](aspnet-mvc-4-fundamentals/_static/image30.png "Store disco albümlerine göz atma")

    *Store disco albümlerine göz atma*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>Görev 6-belirli bir albüm hakkındaki bilgileri görüntüleme

Bu görevde, belirli bir albüm hakkındaki bilgileri görüntülemek için **Mağaza/Ayrıntılar** görünümünü uygulayacaksınız. Bu uygulamalı laboratuvarda, albüm hakkında görüntülenecek her şey zaten **Görünüm** şablonunda yer alıyor. Bu nedenle, bir **storebir ViewModel** sınıfı oluşturmak yerine, albümü kendisine geçirerek geçerli **StoreBrowseViewModel** şablonunu kullanacaksınız.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. **Storecontroller**'ın **Ayrıntılar** eylem yöntemi için yeni bir **Ayrıntılar** görünümü ekleyin. Bunu yapmak için **Storecontroller** sınıfında **Details** yöntemine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.
2. **Görünüm Ekle** Iletişim kutusunda **görünüm adının** **Ayrıntılar**olduğunu doğrulayın. **Türü kesin belirlenmiş görünüm oluştur** onay kutusunu Işaretleyin ve **model sınıfı** açılır listesinden **Albüm** ' yi seçin. Diğer alanları varsayılan değerlerine bırakın. Daha sonra **Ekle**'ye tıklayın. Bu, **\Views\store\details.cshtml** dosyasını oluşturur ve açar.

    ![Ayrıntı görünümü ekleme](aspnet-mvc-4-fundamentals/_static/image31.png "Ayrıntı görünümü ekleme")

    *Ayrıntı görünümü ekleme*
3. View şablonuna geçirilen **Albüm** nesnesine erişerek albümün bilgilerini görüntülemek için **details. cshtml** dosyasını değiştirin. Bunu yapmak için içeriği şu şekilde değiştirin: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>Görev 7-uygulamayı çalıştırma

Bu **görevde, Ayrıntılar görünümünün,** **Ayrıntılar eylem** yönteminden albümün bilgilerini alacağını test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje **giriş** sayfasında başlar. Albümün bilgilerini doğrulamak için URL 'YI **/Store/details/5** olarak değiştirin.

    ![Albümler 'e göz atma ayrıntısı](aspnet-mvc-4-fundamentals/_static/image32.png "Albümler 'e göz atma ayrıntısı")

    *Albümün ayrıntısına göz atma*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>Görev 8-sayfalar arasında bağlantı ekleme

Bu görevde, her tarz adında uygun **/Store/gözatam** URL 'sine bağlantı sağlamak Için mağaza görünümünde bir bağlantı ekleyeceksiniz. Bu şekilde, bir tarz üzerine tıkladığınızda, **disco**örneği için **/Store/gözatmaya? tarzı = disco** URL 'sine gidebilirsiniz.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. **Tarayıcı** sayfasına bir bağlantı eklemek için **Dizin** sayfasını güncelleştirin. Bunu yapmak için, **Çözüm Gezgini** **Görünümler** klasörünü ve ardından **Mağaza** klasörünü genişletin ve **Index. cshtml** sayfasına çift tıklayın.
2. Seçili tarzın seçili olduğunu gösteren bir tarayıcı görünümüne bağlantı ekleyin. Bunu yapmak için, **&lt;li&gt;** etiketleri içinde aşağıdaki vurgulanmış kodu değiştirin: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > başka bir yaklaşım, aşağıdaki gibi bir kod ile doğrudan sayfaya bağlanıyor:
   > 
   > &lt;a href =&quot;/Store/gözatmaya? tarzı =@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > Bu yaklaşım işe yarar olsa da, sabit kodlanmış bir dizeye bağlıdır. Denetleyiciyi daha sonra yeniden adlandırırsanız, bu yönergeyi el ile değiştirmeniz gerekir. Daha iyi bir alternatif, bir **HTML yardımcı** yöntemi kullanmaktır. ASP.NET MVC, bu gibi görevler için kullanılabilen bir HTML yardımcı yöntemi içerir. **HTML. ActionLink ()** yardımcı YÖNTEMI, URL yollarının düzgün şekilde URL kodlamalı olduğundan emin olmak için html **&lt;&gt;** bağlantıları oluşturmayı kolaylaştırır.
   > 
   > HTML. ActionLink çeşitli aşırı yüklemeleri vardır. Bu alıştırmada, üç parametre alan bir tane kullanacaksınız:
   > 
   > 1. Bağlantı metni, bu tarz adı görüntülenecektir
   > 2. Denetleyici eylem adı (**tarama**)
   > 3. Ad (**tarz**) ve değer (**tarzı adı**) belirterek rota parametre değerleri

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>Görev 9-uygulamayı çalıştırma

Bu görevde, her bir tarzı uygun **/Store/gözatam** URL 'sine yönelik bir bağlantıyla birlikte görüntülendiğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. Her bir tarzı uygun **/Store/gözam** URL 'sine bağlabildiğini doğrulamak için **/Store** URL 'sini değiştirin.

    ![Göz atma sayfası bağlantıları ile tarzlara göz atma](aspnet-mvc-4-fundamentals/_static/image33.png "Göz atma sayfası bağlantıları ile tarzlara göz atma")

    *Göz atma sayfası bağlantıları ile tarzlara göz atma*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>Görev 10-değerleri geçirmek için dinamik ViewModel koleksiyonu kullanma

Bu görevde, modelde değişiklik yapmadan denetleyiciyi ve görünümü arasında değerleri geçirmek için basit ve güçlü bir yöntem öğreneceksiniz. ASP.NET MVC 4, herhangi bir dinamik değere atanabilecek ve denetleyicilerin ve görünümlerin içinde erişilebilen &quot;ViewModel&quot;koleksiyonu sağlar.

Artık, denetleyiciden görünüme&quot; &quot;**starred tarzları** listesini geçirmek Için ViewBag dinamik toplamayı kullanacaksınız. Mağaza dizini görünümü **ViewModel** 'e erişir ve bilgileri görüntüler.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. ViewModel koleksiyonunda yıldızlı tarzının bir listesini oluşturmak için **StoreController.cs** ve **dizini** Değiştir metodunu açın:

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > Özelliklere erişmek için **ViewBag [&quot;starred&quot;]** sözdizimini de kullanabilirsiniz.
2. &quot;, bu laboratuvarın **Source\assets\ımages** klasörüne **startred. png&quot;** yıldız simgesi dahildir. Uygulamayı uygulamaya eklemek için, **Windows Gezgini** penceresinden içeriğini aşağıda gösterildiği gibi Visual Web Developer Express içindeki **Çözüm Gezgini** sürükleyin:

    ![Çözüme yıldızlı resim ekleme](aspnet-mvc-4-fundamentals/_static/image34.png "Çözüme yıldızlı resim ekleme")

    *Çözüme yıldızlı resim ekleme*
3. **Store/Index. cshtml** görünümünü açın ve içeriği değiştirin. **ViewBag** koleksiyonundaki &quot;yıldızlı&quot; özelliğini okuyacaksınız ve geçerli tarz adının listede olup olmadığını sorabilirsiniz. Bu durumda, tarz bağlantısına doğrudan bir yıldız simgesi gösterilir.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>Görev 11-uygulamayı çalıştırma

Bu görevde, yıldızlı tarzının bir yıldız simgesi göstermesini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje **giriş** sayfasında başlar. Tüm öne çıkan tarzın daha önce bir etiket içerdiğini doğrulamak için URL 'YI **/Store** olarak değiştirin:

    ![Yıldızlı öğeleriyle tarzlara göz atma](aspnet-mvc-4-fundamentals/_static/image35.png "Yıldızlı öğeleriyle tarzlara göz atma")

    *Yıldızlı öğeleriyle tarzlara göz atma*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>Alıştırma 7: ASP.NET MVC 4 yeni şablonu etrafında bir lap

Bu alıştırmada, yeni şablonun en ilgili özelliklerine göz önünde bulundurularak ASP.NET MVC 4 proje şablonlarındaki geliştirmeleri araştıracaktır.

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>Görev 1: ASP.NET MVC 4 Internet uygulaması şablonunu keşfetme

1. Zaten açık değilse, **Web için vs Express** başlatın
2. Dosyayı seçin **| Yeni | Proje** menü komutu. **Yeni proje** Iletişim kutusunda **görseli C#seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulamasını**seçin. Projeyi *MusicStore* olarak **adlandırın** ve *başlamak*için **çözüm adını** güncelleştirin, ardından bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın.

    ![Yeni bir ASP.NET MVC 4 projesi oluşturma](aspnet-mvc-4-fundamentals/_static/image36.png "Yeni bir ASP.NET MVC 4 projesi oluşturma")

    *Yeni bir ASP.NET MVC 4 projesi oluşturma*
3. **Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın. Görünüm altyapısı olarak Razor veya ASPX seçeneklerinden birini belirleyebilirsiniz.

    ![Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma](aspnet-mvc-4-fundamentals/_static/image37.png "Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma")

    *Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma*

    > [!NOTE]
    > Razor söz dizimi, ASP.NET MVC 3 ' te tanıtılmıştır. Amacı, bir dosyada gereken karakter ve tuş vuruşlarının sayısını en aza indirmektir ve hızlı ve akıcı bir kodlama iş akışını etkinleştirir. Razor, mevcut C#/vb (veya diğer) dil becerilerini kullanır ve harıka bir HTML oluşturma iş akışı sağlayan bir şablon biçimlendirme sözdizimi sunar.
4. **F5** tuşuna basarak çözümü çalıştırın ve yenilenen şablonu görüntüleyin. Aşağıdaki özelliklere bakabilirsiniz:

    1. **Modern stil şablonları**

        Şablonlar, daha modern görünümlü daha fazla stil sunarak yenilendi.

        ![ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar")

        *ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar*
    2. **Uyarlamalı Işleme**

        Tarayıcı penceresini yeniden boyutlandırın ve sayfa düzeninin yeni pencere boyutuna dinamik olarak nasıl uyum sağlayadığına dikkat edin. Bu şablonlar, hiçbir özelleştirme yapmadan hem masaüstü hem de mobil platformlarda düzgün şekilde işlemek için uyarlamalı işleme tekniğini kullanır.

        ![Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu](aspnet-mvc-4-fundamentals/_static/image39.png "Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu")

        *Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu*
5. Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.
6. Artık çözümü keşfedebiliyor ve proje şablonunda ASP.NET MVC 4 tarafından tanıtılan yeni özelliklerden bazılarını kullanıma sunabileceksiniz.

    ![ASP.NET MVC4-Internet-uygulama-proje-şablon](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 Internet uygulaması proje şablonu")

    *ASP.NET MVC 4 Internet uygulaması proje şablonu*

   1. **HTML5 işaretleme**

       Yeni Tema işaretlemesini öğrenmek için şablon görünümlerine gözatıp. Örneğin, **giriş** klasörü içinde **. cshtml** görünümünü açın.

       ![Razor ve HTML5 işaretlemesini kullanarak yeni şablon](aspnet-mvc-4-fundamentals/_static/image41.png "Razor ve HTML5 işaretlemesini kullanarak yeni şablon")

       *Razor ve HTML5 işaretlemesini kullanarak yeni şablon*
   2. **JavaScript kitaplıkları dahil**

      1. **jQuery**: jQuery, HTML belgesi geçiş, olay işleme, animasyon uygulama ve Ajax etkileşimlerini basitleştirir.
      2. **jQuery kullanıcı arabirimi**: Bu kitaplık, jQuery JavaScript kitaplığının üzerine inşa olan alt düzey etkileşim ve animasyon, gelişmiş etkiler ve ayrılabilir pencere öğeleri için soyutlamalar sağlar.

         > [!NOTE]
         > [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)' de jQuery ve jQuery kullanıcı arabirimi hakkında bilgi edinebilirsiniz.
      3. **Altını gizleme koutjs**: ASP.NET MVC 4 varsayılan şablonu artık JAVASCRIPT ve HTML kullanarak zengin ve yüksek oranda yanıt veren Web uygulamaları oluşturmanıza olanak tanıyan bir JavaScript MVVM çerçevesi olan **altını gizleme**özelliği içerir. ASP.NET MVC 3 gibi, jQuery ve jQuery kullanıcı arabirimi kitaplıkları da ASP.NET MVC 4 ' te de bulunur.

          > [!NOTE]
          > Bu bağlantıdaki altını gizleme ( [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)) kitaplığı hakkında daha fazla bilgi edinebilirsiniz.
      4. **Modernizr**: Bu kitaplık otomatik olarak ÇALıŞARAK, HTML5 ve CSS3 teknolojilerini kullanırken sitenizi eski tarayıcılarla uyumlu hale getirir.

          > [!NOTE]
          > Bu bağlantıda Modernizr Kitaplığı hakkında daha fazla bilgi edinebilirsiniz: [http://www.modernizr.com/](http://www.modernizr.com/).
   3. **Çözüme dahil SimpleMembership**

       SimpleMembership, önceki ASP.NET rolü ve üyelik sağlayıcısı sisteminin yerini alacak şekilde tasarlanmıştır. Geliştiricinin web sayfalarını daha esnek bir şekilde güvenli hale getirmeye daha kolay bir şekilde bir çok yeni özelliği vardır.

       Internet şablonu, SimpleMembership tümleştirmeye yönelik birkaç şey ayarlamış. Örneğin, AccountController OAuthWebSecurity 'yi (OAuth hesabı kaydı, oturum açma, yönetim, vs.) ve web güvenliği 'ni kullanmaya hazırlanır.

       ![Çözüme dahil SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "Çözüme dahil SimpleMembership")

       *Çözüme dahil SimpleMembership*

       > [!NOTE]
       > MSDN 'de [Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) hakkında daha fazla bilgi edinin.

> [!NOTE]
> Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak ASP.NET MVC 'nin temellerini öğrendiniz:

- MVC uygulamasının temel öğeleri ve bunların nasıl etkileşimde bulunduğu
- ASP.NET MVC uygulaması oluşturma
- URL ve QueryString aracılığıyla geçirilen parametreleri işlemek için denetleyicileri ekleme ve yapılandırma
- Genel HTML içeriği için şablon ayarlamak üzere bir düzen ana sayfası ekleme, HTML içeriğini görüntülemek için görünüm ve görüntüleme şablonunu iyileştirmek üzere bir stil sayfası.
- Dinamik bilgileri görüntülemek için görünüm şablonuna Özellikler geçirmek için ViewModel deseninin nasıl kullanılacağı
- Görünüm şablonunda denetleyicilere geçirilen parametreleri kullanma
- ASP.NET MVC uygulamasının içindeki sayfalara bağlantı ekleme
- Bir görünümde dinamik özellikler ekleme ve kullanma
- ASP.NET MVC 4 proje şablonlarındaki geliştirmeler

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-fundamentals/_static/image44.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-fundamentals/_static/image45.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-fundamentals/_static/image46.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-fundamentals/_static/image47.png)

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

    ![Windows Azure portal oturum açın](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure portal oturum açın")

    *Windows Azure 'da oturum açma Yönetim Portalı*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-fundamentals/_static/image49.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-fundamentals/_static/image50.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](aspnet-mvc-4-fundamentals/_static/image51.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](aspnet-mvc-4-fundamentals/_static/image52.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-fundamentals/_static/image53.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.

    ![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-fundamentals/_static/image54.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-fundamentals/_static/image55.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](aspnet-mvc-4-fundamentals/_static/image56.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-fundamentals/_static/image57.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-fundamentals/_static/image58.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](aspnet-mvc-4-fundamentals/_static/image59.png)

    *Değişiklikleri Onayla*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](aspnet-mvc-4-fundamentals/_static/image60.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](aspnet-mvc-4-fundamentals/_static/image61.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](aspnet-mvc-4-fundamentals/_static/image62.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](aspnet-mvc-4-fundamentals/_static/image63.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.

     ![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-fundamentals/_static/image64.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](aspnet-mvc-4-fundamentals/_static/image65.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-fundamentals/_static/image66.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](aspnet-mvc-4-fundamentals/_static/image67.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

    ![Windows Azure 'da yayımlanan uygulama](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure 'da yayımlanan uygulama")

    *Windows Azure 'da yayımlanan uygulama*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Ek C: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-fundamentals/_static/image69.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-fundamentals/_static/image70.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-fundamentals/_static/image71.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-fundamentals/_static/image72.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-fundamentals/_static/image73.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-fundamentals/_static/image74.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
