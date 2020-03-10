---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: ASP.NET MVC ile 15 dakika içinde bir film veritabanı uygulaması oluşturma (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther, başlangıçtan sona kadar tüm veritabanı odaklı ASP.NET MVC uygulamasını oluşturur. Bu öğretici, yeni t kullanıcıları için harika bir giriştir...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 1be5d135a44feb27626dd26a544b64cfb57b18a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541995"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a>ASP.NET MVC ile 15 Dakika İçinde Bir Film Veritabanı Uygulaması Oluşturma (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

[Kodu indir](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> Stephen Walther, başlangıçtan sona kadar tüm veritabanı odaklı ASP.NET MVC uygulamasını oluşturur. Bu öğreticide, ASP.NET MVC çerçevesine yeni eklenen ve ASP.NET MVC uygulaması oluşturma sürecini anlamaya yönelik harika bir giriş yer alır.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması oluşturmak için size "beğenme" konusunda size fikir vermektir. Bu öğreticide, başlangıçtan sonuna ASP.NET MVC uygulamasının tamamını oluşturmayı tamamlıyorum. Veritabanı kayıtlarını listeleme, oluşturma ve düzenleme işlemlerinin nasıl yapılacağını gösteren basit bir veritabanı tabanlı uygulama oluşturmayı göstereceğiz.

Uygulamamızı oluşturma işlemini basitleştirmek için, Visual Studio 2008 ' nin yapı iskelesi özelliklerinden faydalanacağız. Visual Studio 'Nun denetleyicilerimiz, modellerimiz ve görünümlerimiz için ilk kodu ve içeriği oluşturmasına izin vereceğiz.

Active Server Pages veya ASP.NET ile çalıştıysanız, ASP.NET MVC 'yi çok tanıdık bulmalısınız. ASP.NET MVC görünümleri Active Server Pages uygulamasındaki sayfalara çok benzer. Ve geleneksel bir ASP.NET Web Forms uygulamasında olduğu gibi, ASP.NET MVC, .NET Framework tarafından sağlanan zengin dil ve sınıf kümesine tam erişim sağlar.

Umarım bu öğreticide, bir ASP.NET MVC uygulaması oluşturma deneyiminin, Active Server sayfaları veya ASP.NET Web Forms uygulaması oluşturma deneyiminden nasıl benzediğinden ve farklılık gösteren bir fikir sunacaktır.

## <a name="overview-of-the-movie-database-application"></a>Film veritabanı uygulamasına genel bakış

Amacınız, şeyleri basit tutmaya yönelik olduğundan çok basit bir film veritabanı uygulaması oluşturacağız. Basit film veritabanı uygulamamız üç şey yapmamızı sağlayacak:

1. Film veritabanı kayıtlarının bir kümesini listeleyin
2. Yeni bir film veritabanı kaydı oluştur
3. Varolan bir film veritabanı kaydını düzenleme

Yine de şeyleri basit tutmak istediğimizden, uygulamamızı derlemek için gerekli olan ASP.NET MVC çerçevesinin en düşük Özellik sayısından faydalanabilir. Örneğin, test odaklı geliştirmeden yararlanmayacağız.

Uygulamamızı oluşturmak için aşağıdaki adımlardan her birini tamamlamamız gerekir:

1. ASP.NET MVC web uygulaması projesi oluşturma
2. Veritabanını oluşturma
3. Veritabanı modelini oluşturma
4. ASP.NET MVC denetleyicisini oluşturma
5. ASP.NET MVC görünümlerini oluşturma

## <a name="preliminaries"></a>Başlangıç bilgileri

ASP.NET MVC uygulaması derlemek için Visual Studio 2008 ya da Visual Web Developer 2008 Express gerekir. Ayrıca, ASP.NET MVC çerçevesini de indirmeniz gerekir.

Visual Studio 2008 sürümüne sahip değilseniz, Visual Studio 2008 ' nin 90 gün deneme sürümünü bu Web sitesinden indirebilirsiniz:

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

Alternatif olarak, Visual Web Developer Express 2008 ile ASP.NET MVC uygulamaları da oluşturabilirsiniz. Visual Web Developer Express 'i kullanmaya karar verirseniz, hizmet paketi 1 ' ın yüklü olması gerekir. Bu Web sitesinden Visual Web Developer 2008 Express Service Pack 1 ' i indirebilirsiniz:

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Visual Studio 2008 ya da Visual Web Developer 2008 yükledikten sonra, ASP.NET MVC çerçevesini yüklemeniz gerekir. ASP.NET MVC çerçevesini aşağıdaki Web sitesinden indirebilirsiniz:

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> ASP.NET çerçevesini ve ASP.NET MVC çerçevesini ayrı ayrı indirmek yerine Web Platformu Yükleyicisinden yararlanabilirsiniz. Web Platformu Yükleyicisi, bilgisayarınızda yüklü uygulamaları kolayca yönetmenizi sağlayan bir uygulamadır:
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>ASP.NET MVC web uygulaması projesi oluşturma

Visual Studio 2008 ' de yeni bir ASP.NET MVC web uygulaması projesi oluşturarak başlayalım. **Yeni proje** menü seçenek dosyasını seçin ve yeni proje Iletişim kutusunu Şekil 1 ' de görürsünüz. Programlama C# dili olarak öğesini seçin ve ASP.NET MVC web uygulaması proje şablonunu seçin. Projenize MovieApp adını verin ve Tamam düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)

**Şekil 01**: yeni proje iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))

Yeni proje iletişim kutusunun en üstündeki açılan listeden .NET Framework 3,5 ' yi seçtiğinizden emin olun veya ASP.NET MVC web uygulaması proje şablonu görünmez.

Her yeni bir MVC web uygulaması projesi oluşturduğunuzda, Visual Studio size ayrı bir birim testi projesi oluşturmanızı ister. Şekil 2 ' deki iletişim kutusu görünür. Bu öğreticide zaman kısıtlamaları nedeniyle test oluşturmadığımızda (ve, Evet, bunun hakkında biraz fikir veriyoruz) **Hayır** seçeneğini belirleyip **Tamam** düğmesine tıklayın.

> [!NOTE] 
> 
> Visual Web Developer test projelerini desteklemez.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)

**Şekil 02**: birim testi projesi oluştur iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))

Bir ASP.NET MVC uygulamasının standart klasörler kümesi vardır: modeller, görünümler ve denetleyiciler klasörü. Bu standart klasör kümesini Çözüm Gezgini penceresinde görebilirsiniz. Film veritabanı uygulamamızı derlemek için modeller, görünümler ve denetleyiciler klasörlerinin her birine dosya eklememiz gerekir.

Visual Studio ile yeni bir MVC uygulaması oluşturduğunuzda, örnek bir uygulama alırsınız. Sıfırdan başlamak istiyoruz, bu örnek uygulamanın içeriğini silmemiz gerekiyor. Aşağıdaki dosyayı ve aşağıdaki klasörü silmeniz gerekir:

- Controllers\HomeController.cs
- Görünümler/giriş

## <a name="creating-the-database"></a>Veritabanı oluşturma

Film veritabanı kayıtlarınızı barındıracak bir veritabanı oluşturmamız gerekiyor. Luckily, Visual Studio SQL Server Express adlı ücretsiz bir veritabanı içerir. Veritabanını oluşturmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresindeki uygulama\_veri klasörüne sağ tıklayın ve **Ekle, yeni öğe**menü seçeneğini belirleyin.
2. **Veri** kategorisini seçin ve **SQL Server veritabanı** şablonunu seçin (bkz. Şekil 3).
3. Yeni veritabanınızı *MoviesDB. mdf* olarak adlandırın ve **Ekle** düğmesine tıklayın.

Veritabanınızı oluşturduktan sonra, App\_Data klasöründe bulunan MoviesDB. mdf dosyasını çift tıklayarak veritabanına bağlanabilirsiniz. MoviesDB. mdf dosyasına çift tıklamak Sunucu Gezgini penceresini açar.

> [!NOTE] 
> 
> Sunucu Gezgini pencere, Visual Web Developer durumunda Veritabanı Gezgini pencere olarak adlandırılır.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)

**Şekil 03**: Microsoft SQL Server veritabanı oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))

Sonra, yeni bir veritabanı tablosu oluşturuyoruz. Sunucu Gezgini penceresinin içinden Tablolar klasörünü sağ tıklatın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin. Bu menü seçeneği belirlendiğinde veritabanı tablosu Tasarımcısı açılır. Aşağıdaki veritabanı sütunlarını oluşturun:

<a id="0.1_table01"></a>

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar (100) | False |
| Direktörü | Nvarchar (100) | False |
| Davterekiralık | DateTime | False |

İlk sütunda, kimlik sütununda iki özel özellik bulunur. İlk olarak, ID sütununu birincil anahtar sütunu olarak işaretlemeniz gerekir. Kimlik sütununu seçtikten sonra, **birincil anahtar ayarla** düğmesine tıklayın (anahtar gibi görünen simgedir). İkinci olarak, kimlik sütununu kimlik sütunu olarak işaretlemeniz gerekir. Özellikler penceresi sütununda, kimlik belirtimi bölümüne gidin ve genişletin. **Identity Identity** özelliğini **Yes**değerine değiştirin. İşiniz bittiğinde tablo şekil 4 gibi görünmelidir.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)

**Şekil 04**: Filmler veritabanı tablosu ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))

Son adım yeni tabloyu kaydetmadır. Kaydet düğmesine (disketin simgesine) tıklayın ve yeni tabloya film adı verin.

Tablo oluşturmayı tamamladıktan sonra tabloya bazı film kayıtları ekleyin. Sunucu Gezgini penceresinde film tablosuna sağ tıklayın ve **tablo verilerini göster**menü seçeneğini belirleyin. En sevdiğiniz filmlerin bir listesini girin (bkz. Şekil 5).

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)

**Şekil 05**: film kayıtlarını girme ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))

## <a name="creating-the-model"></a>Model oluşturma

Daha sonra, veritabanınızı temsil eden bir sınıf kümesi oluşturulması gerekir. Bir veritabanı modeli oluşturuyoruz. Veritabanı modelinize yönelik sınıfları otomatik olarak oluşturmak için Microsoft Entity Framework avantajlarından faydalanacağız.

> [!NOTE] 
> 
> ASP.NET MVC Framework, Microsoft Entity Framework bağlı değildir. LINQ to SQL, Subsonic ve Nbekletme dahil olmak üzere çeşitli nesne Ilişkisel eşleme (veya/a) araçlarından yararlanarak veritabanı modeli sınıflarınızı oluşturabilirsiniz.

Varlık Veri Modeli sihirbazını başlatmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresinde modeller klasörüne sağ tıklayın ve menü seçeneğini belirleyin **, yeni öğe**' yi seçin.
2. **Veri** kategorisini seçin ve **ADO.net varlık veri modeli** şablonunu seçin.
3. Veri modelinize *MoviesDBModel. edmx* adını verin ve **Ekle** düğmesine tıklayın.

Ekle düğmesine tıkladıktan sonra Varlık Veri Modeli Sihirbazı görüntülenir (bkz. Şekil 6). Sihirbazı tamamladıktan sonra aşağıdaki adımları izleyin:

1. **Model Içeriğini seçin** adımında, **veritabanından oluştur** seçeneğini belirleyin.
2. **Veri bağlantınızı seçin** adımında, bağlantı ayarları için *MoviesDB. mdf* veri bağlantısını ve *MoviesDBEntities* adını kullanın. **İleri** düğmesine tıklayın.
3. **Veritabanı nesnelerinizi seçin** adımında, tablolar düğümünü genişletin, filmler tablosunu seçin. *Movieapp. modellerini* ad alanını girip **son** düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)

**Şekil 06**: varlık veri modeli sihirbazıyla bir veritabanı modeli oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))

Varlık Veri Modeli Sihirbazı 'nı tamamladıktan sonra, Varlık Veri Modeli Tasarımcısı açılır. Tasarımcı, filmler veritabanı tablosunu görüntülemelidir (bkz. Şekil 7).

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)

**Şekil 07**: varlık veri modeli Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))

Devam etmeden önce bir değişiklik yapmanız gerekiyor. Varlık verileri Sihirbazı, filmler veritabanı tablosunu temsil eden *filmler* adlı bir model sınıfı oluşturur. Film sınıfını belirli bir filmi temsil etmek üzere kullanacağımız için, sınıf *adını film yerine* *film* (plural yerine tekil) olarak değiştirmemiz gerekiyor.

Tasarımcı yüzeyinde sınıfın adına çift tıklayın ve filmden film olarak sınıfın adını değiştirin. Bu değişikliği yaptıktan sonra, film sınıfını oluşturmak için **Kaydet** düğmesine (disketin simgesine) tıklayın.

## <a name="creating-the-aspnet-mvc-controller"></a>ASP.NET MVC denetleyicisi oluşturma

Sonraki adım ASP.NET MVC denetleyicisi oluşturmaktır. Bir denetleyici, kullanıcının bir ASP.NET MVC uygulamasıyla nasıl etkileşime gireceğini denetmaktan sorumludur.

Aşağıdaki adımları uygulayın:

1. Çözüm Gezgini penceresinde, denetleyiciler klasörüne sağ tıklayın ve **Ekle, denetleyici**menü seçeneğini belirleyin.
2. Denetleyici Ekle iletişim kutusunda, *HomeController* adını girin ve **Create, Update ve details senaryoları için eylem Ekle yöntemleri** etiketli onay kutusunu Işaretleyin (bkz. Şekil 8).
3. Yeni denetleyiciyi projenize eklemek için **Ekle** düğmesine tıklayın.

Bu adımları tamamladıktan sonra, Listeleme 1 ' deki denetleyici oluşturulur. Dizin, ayrıntılar, oluşturma ve düzenleme adlı yöntemleri içerdiğine dikkat edin. Aşağıdaki bölümlerde, bu yöntemlerin çalışmasını sağlamak için gerekli kodu ekleyeceğiz.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)

**Şekil 08**: yeni BIR ASP.NET MVC denetleyicisi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))

**Listeleme 1 – Controllers\HomeController.cs**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a>Veritabanı kayıtlarını listeleme

Ana denetleyicinin Index () yöntemi, bir ASP.NET MVC uygulaması için varsayılan yöntemdir. Bir ASP.NET MVC uygulaması çalıştırdığınızda, Index () yöntemi çağrılan ilk denetleyici yöntemidir.

, Filmler veritabanı tablosundan kayıt listesini göstermek için Index () yöntemini kullanacağız. Dizin () yöntemiyle film veritabanı kayıtlarını almak için daha önce oluşturduğumuz veritabanı modeli sınıflarından faydalanabilir.

\_DB adlı yeni bir özel alan içermesi için liste 2 ' deki HomeController sınıfını değiştirdim. MoviesDBEntities sınıfı, veritabanı modelimizi temsil eder ve bu sınıfı veritabanımız ile iletişim kurmak için kullanacağız.

Ayrıca, liste 2 ' de dizin () yöntemini de değiştirdim. Index () yöntemi, filmler veritabanı tablosundan tüm film kayıtlarını almak için MoviesDBEntities sınıfını kullanır. *\_DB ifadesi. MovieSet. ToList ()* , filmler veritabanı tablosundan tüm film kayıtlarının bir listesini döndürür.

Film listesi görünüme geçirilir. View () yöntemine geçirilen her şey görünüme görünüm verisi olarak geçirilir.

**Listeleme 2 – denetleyiciler/HomeController. cs (değiştirilen Dizin yöntemi)**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

Index () yöntemi Index adlı bir görünüm döndürür. Film veritabanı kayıtlarının listesini görüntülemek için bu görünümü oluşturuyoruz. Aşağıdaki adımları uygulayın:

**Görünüm Ekle** iletişim kutusunu açmadan önce projenizi oluşturmanız gerekir ( **derleme, derleme çözümünü**seçin) veya **veri sınıfı görüntüle** açılan listesinde hiçbir sınıf görünmeyecek.

1. Kod düzenleyicisinde Index () yöntemine sağ tıklayın ve **Görünüm Ekle** menü seçeneğini belirleyin (bkz. Şekil 9).
2. Görünüm Ekle iletişim kutusunda, **kesin belirlenmiş bir görünüm oluştur** etiketli onay kutusunun işaretli olduğunu doğrulayın.
3. **Içeriği görüntüle** açılan listesinden değer *listesini*seçin.
4. **Veri sınıfı görüntüle** açılan listesinden *Movieapp. modeller. Movie*değerini seçin.
5. Yeni görünümü oluşturmak için Ekle düğmesine tıklayın (bkz. Şekil 10).

Bu adımları tamamladıktan sonra, Views\Home klasörüne Index. aspx adlı yeni bir görünüm eklenir. Dizin görünümünün içeriği, liste 3 ' te bulunur.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)

**Şekil 09**: bir denetleyici eyleminden bir görünüm ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)

**Şekil 10**: Görünüm Ekle iletişim kutusuyla yeni bir görünüm oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))

**Listeleme 3 – Views\home\ındex.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

Dizin görünümü, bir HTML tablosu içindeki filmler veritabanı tablosundan tüm film kayıtlarını görüntüler. Görünüm, ViewData. Model özelliği tarafından temsil edilen her film arasında yinelenen bir foreach döngüsü içerir. F5 tuşuna basarak uygulamanızı çalıştırırsanız, Şekil 11 ' de Web sayfasını görürsünüz.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)

**Şekil 11**: Dizin görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))

## <a name="creating-new-database-records"></a>Yeni veritabanı kayıtları oluşturma

Önceki bölümde oluşturduğumuz dizin görünümü, yeni veritabanı kayıtları oluşturmaya yönelik bir bağlantı içerir. Şimdi, mantığı uygulayıp yeni film veritabanı kayıtları oluşturmak için gereken görünümü oluşturalım.

Ana denetleyici Create () adlı iki yöntem içerir. İlk Create () yönteminde parametre yok. Create () yönteminin bu aşırı yüklemesi, yeni bir film veritabanı kaydı oluşturmak için HTML formunu göstermek üzere kullanılır.

İkinci Create () yönteminde bir FormCollection parametresi vardır. Create () yönteminin bu aşırı yüklemesi sunucuya yeni bir film oluşturmak için HTML formu gönderildiğinde çağrılır. Bu ikinci Create () yönteminin bir HTTP POST işlemi gerçekleştirilmediği takdirde, metodun çağrılmasına engel olan bir AcceptVerbs özniteliği olduğuna dikkat edin.

Bu ikinci Create () yöntemi, liste 4 ' teki güncelleştirilmiş HomeController sınıfında değiştirilmiştir. Create () yönteminin yeni sürümü bir film parametresini kabul eder ve filmler veritabanı tablosuna yeni bir film ekleme mantığını içerir.

> [!NOTE] 
> 
> Bind özniteliğine dikkat edin. Film kimliği özelliğini HTML formdan güncelleştirmek istediğimiz için, bu özelliği açıkça dışlıyoruz.

**Listeleme 4 – Controllers\HomeController.cs (değiştirilen oluşturma yöntemi)**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

Visual Studio, yeni bir film veritabanı kaydı oluşturmaya yönelik formu oluşturmayı kolaylaştırır (bkz. Şekil 12). Aşağıdaki adımları uygulayın:

1. Kod düzenleyicisinde oluştur () yöntemine sağ tıklayın ve **Görünüm Ekle**menü seçeneğini belirleyin.
2. **Kesin belirlenmiş bir görünüm oluştur** etiketli onay kutusunun işaretli olduğunu doğrulayın.
3. **Içeriği görüntüle** açılan listesinden *Oluştur*' u seçin.
4. **Veri sınıfı görüntüle** açılan listesinden *Movieapp. modeller. Movie*değerini seçin.
5. Yeni görünümü oluşturmak için **Ekle** düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)

**Şekil 12**: oluşturma görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))

Visual Studio, görünümü otomatik olarak 5. listede oluşturur. Bu görünüm, film sınıfının özelliklerinin her birine karşılık gelen alanları içeren bir HTML formu içerir.

**Listeleme 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> Görünüm Ekle iletişim kutusu tarafından oluşturulan HTML formu, bir kimlik formu alanı oluşturur. Kimlik sütunu bir kimlik sütunu olduğundan bu form alanına ihtiyacım yoktur ve güvenli bir şekilde kaldırabilirsiniz.

Oluşturma görünümünü ekledikten sonra veritabanına yeni film kayıtları ekleyebilirsiniz. F5 tuşuna basarak uygulamanızı çalıştırın ve şekil 13 ' te formu görmek için yeni oluştur bağlantısına tıklayın. Formu tamamlayıp gönderirseniz yeni bir film veritabanı kaydı oluşturulur.

Form doğrulamasını otomatik olarak almanızı unutmayın. Bir film için bir yayın tarihi girmeyi veya geçersiz bir yayın tarihi girerseniz, form yeniden görüntülenir ve serbest bırakma tarihi alanı vurgulanır.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)

**Şekil 13**: yeni bir film veritabanı kaydı oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))

## <a name="editing-existing-database-records"></a>Mevcut veritabanı kayıtlarını Düzenle

Önceki bölümlerde, yeni veritabanı kayıtlarını nasıl listeleyebilir ve oluşturabileceğiniz açıklanmaktadır. Bu son bölümde, var olan veritabanı kayıtlarını nasıl düzenleyebilirim.

İlk olarak, düzenleme formunu oluşturmamız gerekir. Visual Studio sizin için düzenleme formunu otomatik olarak oluşturduğundan bu adım kolaydır. Visual Studio Code düzenleyicisinde HomeController.cs sınıfını açın ve şu adımları izleyin:

1. Kod düzenleyicisinde Düzenle () yöntemine sağ tıklayın ve **Görünüm Ekle** menü seçeneğini belirleyin (bkz. Şekil 14).
2. **Kesin olarak belirlenmiş bir görünüm oluşturma**etiketli onay kutusunu işaretleyin.
3. **Içeriği görüntüle** açılan listesinden, *Düzenle*değerini seçin.
4. **Veri sınıfı görüntüle** açılan listesinden *Movieapp. modeller. Movie*değerini seçin.
5. Yeni görünümü oluşturmak için **Ekle** düğmesine tıklayın.

Bu adımların tamamlanması, Views\Home klasörüne Edit. aspx adlı yeni bir görünüm ekler. Bu görünüm bir film kaydının düzenlenmesine yönelik bir HTML formu içerir.

[Yeni proje iletişim kutusunu ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)

**Şekil 14**: düzenleme görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))

> [!NOTE] 
> 
> Düzenleme görünümü, film kimliği özelliğine karşılık gelen bir HTML form alanı içerir. İnsanların ID özelliğinin değerini düzenlemesini istemediğiniz için bu form alanını kaldırmalısınız.

Son olarak, bir veritabanı kaydını düzenlemesini desteklemesi için ana denetleyiciyi değiştirmemiz gerekiyor. Güncelleştirilmiş HomeController sınıfı, liste 6 ' da bulunur.

**Listeleme 6 – Controllers\HomeController.cs (düzenleme yöntemleri)**

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

Liste 6 ' da, düzenleme () yönteminin her iki aşırı yüküne ek mantık ekledim. İlk düzenleme () yöntemi, yöntemine geçirilen ID parametresine karşılık gelen film veritabanı kaydını döndürür. İkinci aşırı yükleme, veritabanındaki bir film kaydına yönelik güncelleştirmeleri gerçekleştirir.

Özgün filmi almanız ve ardından, veritabanında var olan filmi güncellemek için ApplyPropertyChanges () çağrısı yapmanız gerektiğini unutmayın.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, ASP.NET MVC uygulaması oluşturma deneyiminden fikir vermektir. ASP.NET MVC web uygulaması oluşturmanın, Active Server sayfaları veya ASP.NET uygulaması oluşturma deneyimine çok benzer olduğunu umuyoruz.

Bu öğreticide, ASP.NET MVC çerçevesinin yalnızca en temel özelliklerini inceledik. Sonraki öğreticilerde, denetleyiciler, denetleyici eylemleri, görünümler, verileri görüntüleme ve HTML Yardımcıları gibi konularda daha ayrıntılı bilgi sunuyoruz.

> [!div class="step-by-step"]
> [Next](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)
