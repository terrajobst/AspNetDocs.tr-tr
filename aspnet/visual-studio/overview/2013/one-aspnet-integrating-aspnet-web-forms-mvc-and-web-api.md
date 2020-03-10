---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: "Uygulamalı laboratuvar: One ASP.NET: ASP.NET Web Forms, MVC ve Web API 'sini tümleştirme | Microsoft Docs"
author: rick-anderson
description: ASP.NET, MVC, Web API 'SI ve diğerleri gibi özel teknolojiler kullanarak Web siteleri, uygulamalar ve hizmetler oluşturmaya yönelik bir çerçevedir. Genişletme ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623202"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>Uygulamalı Laboratuvar: Tek ASP.NET: ASP.NET Web Forms, MVC ve Web API’yi Tümleştirme

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

> ASP.NET, MVC, Web API 'SI ve diğerleri gibi özel teknolojiler kullanarak Web siteleri, uygulamalar ve hizmetler oluşturmaya yönelik bir çerçevedir. Genişletme ASP.NET, oluşturulduktan ve bu teknolojilerin tümleşik olması gerektiğinden, **bir ASP.net**üzerinde çalışan son çalışmalar vardır.
> 
> Visual Studio 2013, bir uygulama oluşturmanıza ve tüm ASP.NET teknolojilerini tek bir projede kullanmanıza imkan tanıyan yeni bir birleştirilmiş proje sistemi kullanıma sunuyor. Bu özellik projenin başlangıcında bir teknoloji seçme gereksinimini ortadan kaldırır ve bunun yerine birden çok ASP.NET Framework 'ün bir proje içinde kullanımını teşvik eder.
> 
> Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Overview"></a>
## <a name="overview"></a>Genel bakış

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- **Bir ASP.net** proje türünü temel alan bir Web sitesi oluşturma
- **MVC** ve **Web apı** gibi farklı **ASP.net** çerçeveleri aynı projede kullanın
- Bir **ASP.net** uygulamasının ana bileşenlerini tanımla
- Model sınıflarınıza göre CRUD işlemleri gerçekleştirmek üzere otomatik olarak denetleyiciler ve görünümler oluşturmak için **ASP.net Scafkatlama** çerçevesinden yararlanın
- Her iş için doğru aracı kullanarak makine ve insanlarca okunabilir biçimlerde aynı bilgi kümesini kullanıma sunun

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [Visual Studio 2013 Güncelleştirme 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.

1. Windows Gezgini 'ni açın ve laboratuvarın **kaynak** klasörüne gidin.
2. Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.
3. Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.

> [!NOTE]
> Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Kod parçacıklarını kullanma

Laboratuvar belgesi boyunca kod blokları eklemeniz istenir. Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.

> [!NOTE]
> Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür. Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun. Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız. Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Yeni bir Web Forms projesi oluşturma](#Exercise1)
2. [Yapı Iskelesi kullanarak MVC denetleyicisi oluşturma](#Exercise2)
3. [Yapı Iskelesi kullanarak Web API denetleyicisi oluşturma](#Exercise3)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**

> [!NOTE]
> Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir. Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler. Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır. Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>Alıştırma 1: yeni bir Web Forms projesi oluşturma

Bu alıştırmada, aynı uygulamadaki Web Forms, MVC ve Web API bileşenlerini kolayca tümleştirmenize olanak tanıyan **ASP.net** Birleşik proje deneyimini kullanarak Visual Studio 2013 yeni bir Web Forms sitesi oluşturacaksınız. Sonra oluşturulan çözümü keşfedebilir ve parçalarını tanımlayabilir, son olarak Web sitesini çalışır durumda görürsünüz.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>Görev 1 – bir ASP.NET deneyimini kullanarak yeni bir site oluşturma

Bu görevde, Visual Studio 'da **bir ASP.net** proje türüne göre yeni bir Web sitesi oluşturmaya başlayacaksınız. **Bir ASP.net** tüm ASP.NET teknolojilerini birleştirir ve bunları istediğiniz gibi karıştırma ve eşleştirme seçeneği sunar. Daha sonra uygulamanız içinde yan yana Web Forms, MVC ve Web API 'sinin farklı bileşenlerini tanıyacaksınız.

1. **Web için Visual Studio Express 2013** ' i açın ve dosya ' yı seçin **| Yeni proje...** Yeni bir çözüm başlatmak için.

    ![Yeni proje oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *Yeni bir proje oluşturma*
2. **Yeni proje** iletişim kutusunda, görsel  **C# altında ASP.NET Web uygulaması ' nı seçin | Web** sekmesine ve **.NET Framework 4,5** ' nin seçildiğinden emin olun. Projeyi *Myhybridsite*olarak adlandırın, bir **konum** seçin ve **Tamam 'a**tıklayın.

    ![Yeni ASP.NET Web uygulaması projesi](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *Yeni bir ASP.NET Web uygulaması projesi oluşturma*
3. **Yeni ASP.NET projesi** iletişim kutusunda **Web Forms** şablonunu seçin ve **MVC** ve **Web API 'si** seçeneklerini belirleyin. Ayrıca, **kimlik doğrulama** seçeneğinin **bireysel kullanıcı hesapları**olarak ayarlandığından emin olun. Devam etmek için **Tamam** 'a tıklayın.

    ![Web API ve MVC bileşenleri dahil Web Forms şablonuyla yeni bir proje oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Web API ve MVC bileşenleri dahil Web Forms şablonuyla yeni bir proje oluşturma*
4. Artık oluşturulan çözümün yapısını inceleyebilirsiniz.

    ![Oluşturulan çözümü keşfetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *Oluşturulan çözümü keşfetme*

    1. **Hesap:** Bu klasör, kaydedilecek Web formu sayfalarını içerir, oturum açın ve uygulamanın kullanıcı hesaplarını yönetir. Bu klasör, Web Forms projesi şablonunun yapılandırması sırasında **bireysel kullanıcı hesapları** kimlik doğrulaması seçeneği belirlendiğinde eklenir.
    2. **Modeller:** Bu klasör, uygulama verilerinizi temsil eden sınıfları içerir.
    3. **Denetleyiciler** ve **Görünümler**: Bu klasörler **ASP.NET MVC** ve **ASP.NET Web API** bileşenleri için gereklidir. MVC ve Web API teknolojilerini bir sonraki alıştırmada keşfedecektir.
    4. **Default. aspx**, **Contact. aspx** ve **About. aspx** dosyaları, uygulamanıza özgü sayfaları oluşturmak için başlangıç noktaları olarak kullanabileceğiniz önceden tanımlanmış Web formu sayfalarıdır. Bu dosyaların programlama mantığı, bir &quot;. aspx. vb&quot; veya &quot;. aspx.cs&quot; uzantısına (kullanılan dile bağlı olarak) sahip &quot;arka plan kod&quot; dosyası olarak adlandırılan ayrı bir dosyada yer alır. Arka plan kod mantığı sunucuda çalışır ve sayfanız için HTML çıktısını dinamik olarak oluşturur.
    5. **Site. Master** ve **site. Mobile. Master** sayfaları, uygulamadaki tüm sayfaların görünüm ve yapısını ve standart davranışını tanımlar.
5. Sayfanın içeriğini araştırmak için **default. aspx** dosyasına çift tıklayın.

    ![Default. aspx sayfasını keşfetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Default. aspx sayfasını keşfetme*

    > [!NOTE]
    > Dosyanın en üstündeki **sayfa** yönergesi Web Forms sayfasının özniteliklerini tanımlar. Örneğin, **MasterPageFile** özniteliği ana sayfanın yolunu belirtir-bu durumda, *site. Master* sayfası ve **Inherits** özniteliği, sayfanın devralması için arka plan kod sınıfını tanımlar. Bu sınıf, **codebehind** özniteliği tarafından belirlenen dosyada bulunur.
    > 
    > **ASP: Content** Control, sayfanın gerçek içeriğini (metin, biçimlendirme ve denetimler) tutar ve ana sayfada bir **ASP: ContentPlaceHolder** denetimiyle eşlenir. Bu durumda, sayfa içeriği *site. Master* sayfasında tanımlanan *mainContent* denetimi içinde işlenir.
6. **Uygulama\_Başlat** klasörünü genişletin ve **WebApiConfig.cs** dosyasına dikkat edin. Visual Studio, projenizi bir ASP.NET şablonuyla yapılandırırken Web API 'SI eklemiş olduğunuzdan, bu dosyayı oluşturulan çözümde içeriyordu.
7. **WebApiConfig.cs** dosyasını açın. *WebApiConfig* SıNıFıNDA, http YOLLARıNı **Web API DENETLEYICILERIYLE**eşleyen Web API 'siyle ilişkili yapılandırmayı bulacaksınız.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. **RouteConfig.cs** dosyasını açın. *RegisterRoutes* yönteminin IÇINDE, http yollarını **MVC denetleyicileriyle**eşleyen MVC ile ilişkili yapılandırmayı bulacaksınız.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>Görev 2 – çözümü çalıştırma

Bu görevde, oluşturulan çözümü çalıştıracak, uygulamanın URL yeniden yazma ve yerleşik kimlik doğrulama gibi bazı özelliklerini keşfedecektir.

1. Çözümü çalıştırmak için **F5** tuşuna basın veya araç çubuğunda bulunan **Başlat** düğmesine tıklayın. Uygulama giriş sayfası tarayıcıda açılmalıdır.

    ![Çözümü çalıştırma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Web Forms sayfalarının çağrıldığından emin olun. Bunu yapmak için, adres çubuğundaki URL 'ye **/Contact.aspx** ekleyin ve **ENTER**'a basın.

    ![Kolay URL’ler](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *Kolay URL 'Ler*

    > [!NOTE]
    > Gördüğünüz gibi URL, **/Contact**olarak değişir. **ASP.NET 4**' ten başlayarak, URL yönlendirme özellikleri Web Forms eklendi, bu nedenle *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* yerine *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* gibi URL 'leri yazabilirsiniz. Daha fazla bilgi için [URL yönlendirmeye](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)bakın.
3. Artık uygulamayla tümleştirilmiş kimlik doğrulama akışını araştıracaktır. Bunu yapmak için sayfanın sağ üst köşesindeki **Kaydet** ' e tıklayın.

    ![Yeni Kullanıcı kaydetme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *Yeni Kullanıcı kaydetme*
4. **Kaydet** sayfasında, bir **Kullanıcı adı** ve **parola**girin ve ardından **Kaydet**' e tıklayın.

    ![Kayıt sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *Kayıt sayfası*
5. Uygulama yeni hesabı kaydeder ve kullanıcının kimliği doğrulanır.

    ![Kullanıcının kimliği doğrulandı](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *Kullanıcının kimliği doğrulandı*
6. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>Alıştırma 2: yapı Iskelesi kullanarak MVC denetleyicisi oluşturma

Bu alıştırmada, tek bir kod satırı yazmadan CRUD işlemleri gerçekleştirmeye yönelik eylemlerle ve Razor görünümleriyle ASP.NET MVC 5 denetleyicisi oluşturmak için Visual Studio tarafından sunulan ASP.NET Scafkatlama çerçevesinden faydalanabilirsiniz. Yapı iskelesi işlemi, SQL veritabanında veri bağlamını ve veritabanı şemasını oluşturmak için Entity Framework Code First kullanacaktır.

**Entity Framework Code First hakkında**

Entity Framework (EF), ilişkisel bir depolama şemasını kullanarak doğrudan programlama yerine kavramsal bir uygulama modeliyle programlama yoluyla veri erişimi uygulamaları oluşturmanıza olanak sağlayan bir nesne ilişkisel Eşleyici 'dir (ORM).

Entity Framework Code First modelleme iş akışı, sorgu, değişiklik izleme ve güncelleştirme işlevlerini gerçekleştirirken EF 'in kullandığı modeli göstermek için kendi etki alanı sınıflarınızı kullanmanıza olanak sağlar. Code First geliştirme iş akışını kullanarak, bir veritabanı oluşturarak veya bir şema belirterek uygulamanıza başlamanız gerekmez. Bunun yerine, uygulamanız için en uygun etki alanı modeli nesnelerini tanımlayan standart .NET sınıfları yazabilir ve Entity Framework veritabanı sizin için oluşturulur.

> [!NOTE]
> [Buradan](../../../entity-framework.md)Entity Framework hakkında daha fazla bilgi edinebilirsiniz.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>Görev 1 – yeni model oluşturma

Artık, MVC denetleyicisi ve görünümleri oluşturmak için yapı iskelesi işlemi tarafından kullanılan model olacak bir **kişi** sınıfı tanımlayacaksınız. Bir **kişi** modeli sınıfı oluşturarak başlayacaksınız ve DENETLEYICIDEKI CRUD işlemleri, yapı iskelesi özellikleri kullanılarak otomatik olarak oluşturulur.

1. **Web için Visual Studio Express 2013** ve **kaynak/EX2-Mvcscafkat/başlangıç** klasöründe bulunan **myhybridsite. sln** çözümünü açın. Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.
2. **Çözüm Gezgini**, **Myhybridsite** projesinin **modeller** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf.** ...

    ![Kişi modeli sınıfı ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Kişi modeli sınıfı ekleme*
3. **Yeni öğe Ekle** iletişim kutusunda dosyayı *Person.cs* olarak adlandırın ve **Ekle**' ye tıklayın.

    ![Kişi modeli sınıfı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Kişi modeli sınıfı oluşturma*
4. **Person.cs** dosyasının içeriğini aşağıdaki kodla değiştirin. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.

    (Kod parçacığı- *BringingTogetherOneAspNet-EX2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. **Çözüm Gezgini**, **Myhybridsite** projesine sağ tıklayın ve **Oluştur**' u seçin ya da projeyi derlemek için **CTRL + SHIFT + B** tuşlarına basın.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>Görev 2 – MVC denetleyicisi oluşturma

Artık **kişi** modeli oluşturduğumuzdan, **kışı**için CRUD denetleyicisi eylemlerini ve görünümlerini oluşturmak üzere Entity Framework ile ASP.NET MVC scafkatlaması kullanacaksınız.

1. **Çözüm Gezgini**, **Myhybridsite** projesinin **denetleyiciler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni yapı Iskelesi öğesi...** .

    ![Yeni bir scafkatlanmış denetleyici oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *Yeni bir Scafkatlanmış denetleyici oluşturma*
2. **Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici '** yi seçin ve ardından Ekle ' ye tıklayın **.**

    ![Görünümler ve Entity Framework MVC 5 denetleyicisi seçiliyor](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *Görünümler ve Entity Framework MVC 5 denetleyicisi seçiliyor*
3. *Mvcpersoncontroller* 'ı **Denetleyici adı**olarak ayarlayın, **zaman uyumsuz denetleyici eylemleri kullan** seçeneğini belirleyin ve **model sınıfı**olarak **Person (myhybridsite. modeller)** öğesini seçin.

    ![Yapı iskelesi ile MVC denetleyicisi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *Yapı iskelesi ile MVC denetleyicisi ekleme*
4. **Veri bağlamı sınıfı**altında **Yeni veri bağlamı...** öğesine tıklayın.

    ![Yeni bir veri bağlamı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *Yeni bir veri bağlamı oluşturma*
5. **Yeni veri bağlamı** iletişim kutusunda yeni veri *bağlamı ' nı adlandırın ve* **Ekle**' ye tıklayın.

    ![Yeni Personbu bağlamı oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *Yeni Personya bağlamı türü oluşturuluyor*
6. Yeni denetleyiciyi yapı iskelesi içeren bir **kişiye** oluşturmak için **Ekle** ' ye tıklayın. Daha sonra, Visual Studio denetleyici eylemlerini, kişi veri bağlamını ve Razor görünümlerini oluşturacaktır.

    ![Yapı iskelesi ile MVC denetleyicisi oluşturduktan sonra](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *Yapı iskelesi ile MVC denetleyicisi oluşturduktan sonra*
7. **MvcPersonController.cs** dosyasını **denetleyiciler** klasöründe açın. CRUD eylem yöntemlerinin otomatik olarak oluşturulduğuna dikkat edin.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > Önceki adımlarda bulunan scafkatlama seçeneklerinde **zaman uyumsuz denetleyici eylemleri kullan** onay kutusunu seçerek, Visual Studio kişi veri bağlamına erişimi olan tüm eylemler için zaman uyumsuz eylem yöntemleri oluşturur. İstek işlenirken Web sunucusunun iş gerçekleştirmesini engellemeyi önlemek için uzun süre çalışan, CPU olmayan istekler için zaman uyumsuz eylem yöntemleri kullanmanız önerilir.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>Görev 3 – çözümü çalıştırma

Bu görevde, **kişi** görünümlerinin beklendiği gibi çalıştığını doğrulamak için çözümü yeniden çalıştıracaksınız. Veritabanına başarıyla kaydedildiğini doğrulamak için yeni bir kişi ekleyeceksiniz.

1. Çözümü çalıştırmak için **F5** tuşuna basın.
2. **/Mvcperson**'a gidin. Kişilerin listesini gösteren yapı iskelesi görünümü.
3. Yeni bir kişi eklemek için **Yeni oluştur** ' a tıklayın.

    ![Scafkatlanmış MVC görünümlerine gitme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *Scafkatlanmış MVC görünümlerine gitme*
4. **Oluştur** görünümünde, kişi Için bir **ad** ve **yaş** girin ve **Oluştur**' a tıklayın.

    ![Yeni bir kişi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *Yeni bir kişi ekleme*
5. Yeni kişi listeye eklenir. Öğe listesinde, **Ayrıntılar** ' a tıklayarak kişinin Ayrıntılar görünümünü görüntüleyin. Ardından, **Ayrıntılar** görünümünde liste görünümüne geri dönmek Için **listeye geri dön** ' e tıklayın.

    ![Kişinin Ayrıntılar görünümü](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *Kişinin Ayrıntılar görünümü*
6. Kişiyi silmek için **Sil** bağlantısına tıklayın. İşlemi doğrulamak için **Sil** görünümünde **Sil** ' e tıklayın.

    ![Bir kişiyi silme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *Bir kişiyi silme*
7. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>Alıştırma 3: yapı Iskelesi kullanarak Web API denetleyicisi oluşturma

Web API çerçevesi, ASP.NET yığınının bir parçasıdır ve HTTP hizmetlerini uygulamayı daha kolay hale getirmek, genel olarak JSON veya XML biçimli veriler gönderip almak için tasarlanmıştır.

Bu alıştırmada, bir Web API denetleyicisi oluşturmak için ASP.NET Scafkatmayı yeniden kullanacaksınız. Aynı kişi verilerini JSON biçiminde sağlamak için önceki alıştırmada aynı **kişiyi** ve **personcontext** sınıflarını kullanacaksınız. Aynı kaynakları aynı ASP.NET uygulamasının farklı şekillerde nasıl kullanıma sunabileceğiniz hakkında bilgi alırsınız.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>Görev 1 – Web API denetleyicisi oluşturma

Bu görevde, kişi verilerini JSON gibi makine tüketilebilir bir biçimde kullanıma sunmayacak yeni bir **Web API denetleyicisi** oluşturacaksınız.

1. Zaten açık değilse, **Web için Visual Studio Express 2013** ' i açın ve **kaynak/Ex3-WebAPI/BEGIN** klasöründe bulunan **myhybridsite. sln** çözümünü açın. Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.

    > [!NOTE]
    > Alıştırma 3 ' ten başla çözümüyle başlarsanız, çözümü derlemek için **CTRL + SHIFT + B** tuşlarına basın.
2. **Çözüm Gezgini**, **Myhybridsite** projesinin **denetleyiciler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni yapı Iskelesi öğesi...** .

    ![Yeni bir scafkatlanmış denetleyici oluşturma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *Yeni bir scafkatlanmış denetleyici oluşturma*
3. **Yapı Iskelesi Ekle** iletişim kutusunda sol bölmedeki **Web API 'si** ' ni, sonra da **Eylemler ile Web API 2 denetleyicisi '** ni, orta bölmedeki Entity Framework kullanarak ve ardından Ekle ' yi seçin **.**

    ![Eylemler ve Entity Framework Web API 2 denetleyicisi seçme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Eylemler ve Entity Framework Web API 2 denetleyicisi seçme")

    *Eylemler ve Entity Framework Web API 2 denetleyicisi seçme*
4. *Apipersoncontroller* 'ı **Denetleyici adı**olarak ayarlayın, **zaman uyumsuz denetleyici eylemleri kullan** seçeneğini belirleyin ve sırasıyla **model** ve **veri bağlamı** sınıfları olarak **Person (MyHybridSite. modeller** ) ve **personcontext (myhybridsite. modeller)** seçeneğini belirleyin. Daha sonra **Ekle**'ye tıklayın.

    ![Yapı iskelesi ile Web API denetleyicisi ekleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Yapı iskelesi ile Web API denetleyicisi ekleme")

    *Yapı iskelesi ile Web API denetleyicisi ekleme*
5. Daha sonra Visual Studio, verileriniz ile çalışmak için dört CRUD eylemleriyle **Apipersoncontroller** sınıfını oluşturur.

    ![Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra")

    *Web API denetleyicisini yapı iskelesi ile oluşturduktan sonra*
6. **ApiPersonController.cs** dosyasını açın ve *getkişiler* eylem yöntemini inceleyin. Bu yöntem, kişi verilerini almak için **Personcontext** türünün DB alanını sorgular.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. Şimdi yöntem tanımının üzerindeki açıklamaya dikkat edin. Bir sonraki görevde kullanacağınız bu eylemi sunan URI 'yi sağlar.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > Varsayılan olarak, Web API 'si, MVC denetleyicileriyle çakışmaları önlemek için */API* yoluna sorguları yakalamak üzere yapılandırılmıştır. Bu ayarı değiştirmeniz gerekiyorsa, [ASP.NET Web API 'de yönlendirme](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)' ye başvurun.

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>Görev 2 – çözümü çalıştırma

Bu görevde, Web API denetleyicisinden tam yanıtı incelemek için Internet Explorer **F12 geliştirici araçları** ' nı kullanacaksınız. Uygulama verilerinize ilişkin daha fazla bilgi almak için ağ trafiğini nasıl yakalayabileceğiniz hakkında bilgi alacaksınız.

> [!NOTE]
> Visual Studio araç çubuğunda bulunan **Başlat** düğmesinde **Internet Explorer** 'ın seçili olduğundan emin olun.
> 
> ![Internet Explorer seçeneği](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 geliştirici araçları** , bu uygulamalı laboratuvarda kapsanmayan geniş bir işlevsellik kümesine sahiptir. Hakkında daha fazla bilgi edinmek istiyorsanız, [F12 geliştirici araçlarını kullanma](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))bölümüne bakın.

1. Çözümü çalıştırmak için **F5** tuşuna basın.

    > [!NOTE]
    > Bu görevi doğru bir şekilde takip edebilmek için uygulamanızın verileri olması gerekir. Veritabanınız boşsa, çalışma 2 ' de görev 3 ' e geri dönerek MVC görünümlerini kullanarak yeni bir kişi oluşturma hakkındaki adımları izleyebilirsiniz.
2. Tarayıcıda, **Geliştirici Araçları** panelini açmak için **F12** tuşuna basın. **CTRL** + **4** ' e basın veya **ağ** simgesine tıklayın ve sonra ağ trafiğini yakalamaya başlamak için yeşil ok düğmesine tıklayın.

    ![Web API ağı yakalama başlatılıyor](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API ağı yakalama başlatılıyor")

    *Web API ağı yakalama başlatılıyor*
3. Tarayıcı adres çubuğundaki URL 'ye **API/ApiPerson** ekleyin. Şimdi **Apipersoncontroller**'dan Yanıtın ayrıntılarını inceleyebilirsiniz.

    ![Web API aracılığıyla kişi verilerini alma](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API aracılığıyla kişi verilerini alma")

    *Web API aracılığıyla kişi verilerini alma*

    > [!NOTE]
    > İndirme işlemi tamamlandıktan sonra indirilen dosyayla bir eylem yapmanız istenir. Geliştirici araç penceresi aracılığıyla yanıt içeriğini izleyebilmek için iletişim kutusunu açık bırakın.
4. Şimdi yanıtın gövdesini inceleyeceksiniz. Bunu yapmak için **Ayrıntılar** sekmesine tıklayın ve ardından **yanıt gövdesi**' ne tıklayın. İndirilen verilerin, **kişi** sınıfına karşılık gelen özellik **kimliği**, **ad** ve **yaşa** sahip bir nesne listesi olup olmadığını kontrol edebilirsiniz.

    ![Web API yanıt gövdesini görüntüleme](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API yanıt gövdesini görüntüleme")

    *Web API yanıt gövdesini görüntüleme*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>Görev 3 – Web API Yardım sayfaları ekleme

Bir Web API 'SI oluşturduğunuzda, diğer geliştiricilerin API 'nizi nasıl çağırabileceğini bilmesi için bir yardım sayfası oluşturmak yararlı olacaktır. Belge sayfalarını el ile oluşturup güncelleştirebilirsiniz, ancak bakım işleri yapmak zorunda kalmamak için bunları otomatik oluşturmak daha iyidir. Bu görevde, çözüme otomatik olarak Web API Yardım sayfaları oluşturmak için bir NuGet paketi kullanacaksınız.

1. Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' na tıklayın.
2. **Paket Yöneticisi konsolu** penceresinde aşağıdaki komutu yürütün:

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft. Aspnet. WebApi. helppage** paketi gerekli derlemeleri yüklüyor ve **Areas/helppage** klasörü altındakı yardım sayfaları için MVC görünümleri ekliyor.

    ![HelpPage alanı](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage alanı")

    *HelpPage alanı*
3. Varsayılan olarak, yardım sayfalarında belgeler için yer tutucu dizeleri vardır. Belgeleri oluşturmak için XML belge açıklamalarını kullanabilirsiniz. Bu özelliği etkinleştirmek için, **Areas/yardım sayfası/uygulama\_başlangıç** klasöründe bulunan **HelpPageConfig.cs** dosyasını açın ve aşağıdaki satırın açıklamasını kaldırın:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. **Çözüm Gezgini**, **Myhybridsite**projesine sağ tıklayın, **Özellikler** ' i seçin ve **derleme** sekmesine tıklayın.

    ![Derleme sekmesi](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Derleme bölümü")

    *Derleme sekmesi*
5. **Çıkış**' ın altında, **XML belge dosyası**' nı seçin. Düzenle kutusunda **App\_Data/XmlDocument. xml**yazın.

    ![Derleme sekmesindeki çıkış bölümü](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Derleme sekmesindeki çıkış bölümü")

    *Derleme sekmesindeki çıkış bölümü*
6. Değişiklikleri kaydetmek için **CTRL** + **S** tuşlarına basın.
7. **ApiPersonController.cs** dosyasını **denetleyiciler** klasöründen açın.
8. *GetPerson* yöntemi imzası ile *//Al API/apiperson* açıklaması arasına yeni bir satır girin ve ardından üç eğik çizgi yazın.

    > [!NOTE]
    > Visual Studio, yöntem belgelerini tanımlayan XML öğelerini otomatik olarak ekler.
9. *Getkişilerim* yöntemi için bir Özet metni ve dönüş değeri ekleyin. Aşağıdaki gibi görünmelidir.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. Çözümü çalıştırmak için **F5** tuşuna basın.
11. Yardım sayfasına gitmek için, adres çubuğundaki URL 'ye **/help** ekleyin.

    ![ASP.NET Web API Yardım sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Yardım sayfası")

    *ASP.NET Web API Yardım sayfası*

    > [!NOTE]
    > Sayfanın ana içeriği, denetleyiciye göre gruplandırılan bir API tablosudur. Tablo girdileri, **IApiExplorer** arabirimi kullanılarak dinamik olarak oluşturulur. Bir API denetleyicisi ekler veya güncelleştirirseniz, uygulamayı bir sonraki derişinizde tablo otomatik olarak güncelleştirilir.
    > 
    > API sütunu, HTTP yöntemini ve göreli URI **'yi** listeler. **Açıklama** sütunu, yöntemin belgelerinden ayıklanmış olan bilgileri içerir.
12. Yöntem tanımının üstüne eklediğiniz açıklamanın Açıklama sütununda görüntülendiğini unutmayın.

    ![API yöntemi açıklaması](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API yöntemi açıklaması")

    *API yöntemi açıklaması*
13. Örnek yanıt gövdeleri dahil olmak üzere daha ayrıntılı bilgiler içeren bir sayfaya gitmek için API yöntemlerinden birine tıklayın.

    ![Ayrıntı bilgileri sayfası](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Ayrıntı bilgileri sayfası")

    *Ayrıntılı bilgi sayfası*

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak şu şekilde nasıl yapılacağını öğrendiniz:

- Visual Studio 2013 bir ASP.NET deneyimini kullanarak yeni bir Web uygulaması oluşturun
- Birden çok ASP.NET teknolojilerini tek bir projede tümleştirme
- ASP.NET Scafkatlaması kullanarak model sınıflarınızda MVC denetleyicileri ve görünümleri oluşturma
- Entity Framework aracılığıyla zaman uyumsuz programlama ve veri erişimi gibi özellikleri kullanan Web API denetleyicileri oluşturun
- Denetleyicileriniz için otomatik olarak Web API Yardım sayfaları oluşturma
