---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: Projeyi oluştur | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576063"
---
# <a name="create-the-project"></a>Projeyi Oluşturma

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, ASP.NET özellikleri hakkında bilgi sahibi olmak için Visual Studio 'da varsayılan projeyi oluşturacak, incelemesinin ve çalıştıracaksınız. Ayrıca, Visual Studio ortamını gözden geçilecektir.

## <a name="what-youll-learn"></a>Şunları öğreneceksiniz:

- Yeni bir Web Forms projesi oluşturma.
- Web Forms projesinin dosya yapısı.
- Visual Studio 'da projeyi çalıştırma.
- Varsayılan Web Forms uygulamasının farklı özellikleri.
- Visual Studio ortamını kullanma hakkında bazı temel bilgiler.

## <a name="creating-the-project"></a>Projeyi Oluşturma

1. Visual Studio'yu açın.
2. Visual Studio 'da **Dosya** menüsünden **Yeni proje** ' yi seçin. 

    ![Projeyi oluştur-Yeni Proje menü öğesi](create-the-project/_static/image1.png)
3. Soldaki -**Şablonlar** &gt; **Visual C#**  -&gt; **Web** şablonları grubunu seçin.
4. Orta sütundaki **ASP.NET Web uygulaması** şablonunu seçin.  
 Bu öğretici serisi, .NET Framework 4.5.2 kullanıyor.
5. Projenizi *wingtiptoys* olarak adlandırın ve **Tamam** düğmesini seçin. 

    ![Projeyi oluşturma-yeni proje Iletişim kutusu](create-the-project/_static/image2.png)

    > [!NOTE]
    > Bu öğretici serisindeki projenin adı **wingtiptoys**' dır. Bu *tam* proje adını, öğretici serisi boyunca sunulan kodun beklenen şekilde işlevlerini sağlamak için kullanmanız önerilir.

6. **Kimlik doğrulamayı Değiştir** düğmesine tıklayın. **Bireysel kullanıcı hesapları** ' nı seçin ve **Tamam** düğmesine tıklayın.

7. **Web Forms** şablonunu seçin ve **Tamam** düğmesine tıklayın.

    ![Projeyi oluşturma-yeni proje şablonu](create-the-project/_static/image3.png)

Projenin oluşturulması biraz zaman alabilir. Hazır olduğunda **default. aspx** sayfasını açın.

![Projeyi oluşturma-yeni proje şablonu](create-the-project/_static/image4.png)

Orta pencerenin alt kısmında bir seçenek belirleyerek **Tasarım** görünümü ve **kaynak** görünümü arasında geçiş yapabilirsiniz. **Tasarım** görünümü, ASP.NET Web sayfaları, ana sayfalar, içerik sayfaları, HTML sayfaları ve Kullanıcı DENETIMLERINI neredeyse WYSIWYG görünümü kullanarak görüntüler. **Kaynak** görünümü, Web SAYFANıZ için HTML işaretlemesini görüntüler ve bunları düzenleyebilirsiniz.

> [!TIP] 
> 
> **ASP.NET çerçevelerini anlama**
> 
> ASP.NET Web Forms, tanıdık bir sürükle ve bırak, olay odaklı model kullanarak dinamik Web siteleri oluşturmanızı sağlar. Tasarım yüzeyi ve yüzlerce denetim ve bileşen, veri erişimi ile hızlı bir şekilde gelişmiş, güçlü Kullanıcı arabirimi odaklı siteleri oluşturmanızı sağlar. Wingtip oyuncak mağazası, ASP.NET Web Forms tabanlıdır, ancak bu öğretici serisinde öğrendiği kavramların birçoğu tüm ASP.NET için geçerlidir.
> 
> ASP.NET dört adet birincil geliştirme çerçevesi sunar:
> 
> - [ASP.NET Web Forms](../../../index.md)  
>  Web Forms Framework, Microsoft Windows Forms (WinForms) ve WPF/XAML/Silverlight gibi bildirime dayalı ve denetim tabanlı programlamayı tercih eden geliştiricilere hedefler. WYSıWYG tasarlayıcı temelli bir geliştirme modeli sunarak web geliştirme için hızlı uygulama geliştirme (RAD) ortamı arayan geliştiricilerle popüler hale gelir. Web programlamasına yeni ve geleneksel Microsoft RAD istemci geliştirme araçları hakkında bilgi sahibiyseniz (örneğin, Visual Basic ve görsel C#için), HTML ve JavaScript 'te deneyim duymadan hızlı bir şekilde Web uygulaması oluşturabilirsiniz.
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC, test odaklı geliştirme, sorunların ayrılması, denetimin Inversion (IoC) ve bağımlılık ekleme (DI) gibi desenler ve ilkeler ile ilgilenen geliştiricileri hedefler. Bu çerçeve, bir Web uygulamasının iş mantığı katmanını sunum katmanından ayırmayı teşvik eder.
> - [ASP.NET Web Sayfaları](../../../../web-pages/index.md)  
>  ASP.NET Web sayfaları, PHP satırları üzerinde basit bir Web geliştirme hikayesi isteyen geliştiricilere hedefler. Web sayfaları modelinde, HTML sayfaları oluşturur ve bu biçimlendirmenin nasıl işleneceğini dinamik olarak denetlemek için sayfaya sunucu tabanlı kod eklersiniz. Web sayfaları, basit bir çerçeve olmak üzere özel olarak tasarlanmıştır ve ASP.NET ' e en kolay giriş noktasıdır. Bu, HTML bilen ancak büyük programlama deneyimlerine sahip olmayan, örneğin öğrenciler veya hobbyists. Ayrıca, PHP veya benzer çerçeveleri bilen web geliştiricileri için ASP.NET kullanmaya başlamak için de iyi bir yoldur.
> - [ASP.NET tek sayfalı uygulama](../../../../single-page-application/index.md)  
>  ASP.NET tek sayfalı uygulama (SPA), HTML 5, CSS 3 ve JavaScript kullanarak önemli istemci tarafı etkileşimleri içeren uygulamalar oluşturmanıza yardımcı olur. ASP.NET and Web Tools 2012,2 güncelleştirmesi, altını gizleme. js ve ASP.NET Web API 'SI kullanarak tek sayfalı uygulamalar oluşturmaya yönelik yeni bir şablon sevk eder. Yeni SPA şablonuna ek olarak, yeni topluluk tarafından oluşturulan SPA şablonları da indirilebilir.
> 
> ASP.NET, dört ana geliştirme çerçevesini de göz önünde bulundurun ve bu öğretici serisinde ele alınmaması gereken ek teknolojiler de sunar:
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -tarayıcılar ve mobil cihazlar dahil olmak üzere çok çeşitli ISTEMCILERE ulaşan http hizmetleri oluşturmaya yönelik bir çerçeve.
> - [ASP.NET SignalR](../../../../signalr/index.md) -gerçek zamanlı Web işlevselliği geliştirmeyi kolaylaştıran bir kitaplık.

### <a name="reviewing-the-project"></a>Projeyi gözden geçirme

Visual Studio 'da **Çözüm Gezgini** penceresi, proje dosyalarını yönetmenizi sağlar. **Çözüm Gezgini**, uygulamanıza eklenen klasörlere göz atalım. Web uygulaması şablonu temel bir klasör yapısı ekler:

![Projeyi oluşturma-Çözüm Gezgini](create-the-project/_static/image5.png)

Visual Studio, projeniz için bazı başlangıç klasörlerini ve dosyalarını oluşturur. Bu öğreticide ilerleyen bölümlerinde birlikte çalışabileceksiniz ilk dosya şunlardır:

| **Dosyasýný** | **Amaç** |
| --- | --- |
| *Default. aspx* | Genellikle uygulama bir tarayıcıda çalıştırıldığında ilk sayfa görüntülenir. |
| *Site. Master* | Uygulamanızda sayfalar için tutarlı bir düzen oluşturmanıza ve standart davranışı kullanmanıza olanak tanıyan bir sayfa. |
| *Global. asax* | ASP.NET veya HTTP modülleri tarafından oluşturulan uygulama düzeyi ve oturum düzeyindeki olaylara yanıt vermek için kod içeren isteğe bağlı bir dosya. |
| *Web. config* | Bir uygulama için yapılandırma verileri. |

### <a name="running-the-default-web-application"></a>Varsayılan Web uygulamasını çalıştırma

Varsayılan Web uygulaması, yerleşik işlevselliği ve desteği temel alan zengin bir deneyim sağlar. Varsayılan Web formları projesinde herhangi bir değişiklik yapılmadan, uygulama yerel Web tarayıcınızda çalıştırılmaya hazır olur.

1. Visual Studio 'da ***F5*** tuşuna basın.   
 Uygulama Web tarayıcınızda oluşturulacak ve görüntülenecek.  

    ![Proje-varsayılan sayfasını oluşturma](create-the-project/_static/image6.png)
2. Çalışan uygulamayı gözden geçirmeyi tamamladıktan sonra tarayıcı penceresini kapatın.

Bu varsayılan Web uygulamasında üç ana sayfa vardır: *default. aspx* (Home), *hakkında. aspx*ve *Contact. aspx*. Bu sayfaların her birine üst gezinti çubuğundan ulaşılabilir. Ayrıca, hesap klasöründe, Register. aspx sayfası ve Login. aspx sayfası dahil olmak üzere iki ek sayfa de vardır. Bu iki sayfa, Kullanıcı kimlik bilgilerini oluşturmak, depolamak ve doğrulamak için ASP.NET üyelik yeteneklerini kullanmanıza olanak sağlar.

## <a name="aspnet-web-forms-background"></a>Arka planı ASP.NET Web Forms

ASP.NET Web Forms, sunucuda çalışan kodun tarayıcıya veya istemci cihaza dinamik olarak Web sayfası çıktısı oluşturduğu Microsoft ASP.NET teknolojisini temel alan sayfalardır. Bir ASP.NET Web Forms sayfası stiller, düzen ve benzeri özellikler için doğru tarayıcıyla uyumlu HTML 'yi otomatik olarak işler. Web Forms, Microsoft Visual Basic ve Microsoft Visual C#gibi .NET ortak dil çalışma zamanı tarafından desteklenen herhangi bir dille uyumludur. Ayrıca, Web Forms, yönetilen ortam, tür güvenliği ve devralma gibi avantajlar sağlayan [Microsoft .NET Framework](https://msdn.microsoft.com/vstudio/aa496123)üzerine kurulmuştur.

Bir ASP.NET Web Forms sayfası çalıştığında, sayfa bir dizi işleme adımı gerçekleştirdiği bir yaşam döngüsü boyunca gider. Bu adımlar başlatma, denetimleri örnekleme, durumu geri yükleme ve sürdürme, olay işleyici kodu çalıştırma ve işlemeyi içerir. ASP.NET Web Forms gücünden daha fazla bilgi sahibi olduğunuzda, planladığınız etkiyle ilgili yaşam döngüsü aşamasında kod yazmak için [ASP.NET sayfası yaşam döngüsünü](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx) anlamanız önemlidir.

Bir Web sunucusu bir sayfa için istek aldığında, sayfayı bulur, işler, tarayıcıya gönderir ve sonra tüm sayfa bilgilerini atar. Kullanıcı aynı sayfayı yeniden isterse, sunucu tüm diziyi yineler, sayfanın sıfırdan yeniden işlenmesini ister. Başka bir yöntem de, bir sunucuda işlenen sayfaların belleği yoktur-sayfalar durum bilgisiz değildir. ASP.NET Page Framework, sayfanızın ve denetimlerin durumunu koruma görevini otomatik olarak işler ve uygulamaya özgü bilgilerin durumunu korumak için size açık yollar sunar.

> [!TIP] 
> 
> **Web Forms uygulama şablonundaki Web uygulaması özellikleri**
> 
> ASP.NET Web Forms uygulama şablonu, zengin bir yerleşik işlevsellik kümesi sağlar. Size yalnızca size bir *Home.* aspx sayfası, bir *About.* aspx sayfası, bir *Contact. aspx* sayfası ve ayrıca kullanıcıları kaydeden ve kimlik bilgilerini kaydederek Web sitenizde oturum açabilmeleri için üyelik işlevleri de içerir. Bu genel bakışta, ASP.NET Web Forms uygulama şablonunda bulunan özelliklerden bazıları ve bunların Wingtip Toys uygulamasında nasıl kullanıldıkları hakkında daha fazla bilgi verilmektedir.
> 
> **Üyelik**
> 
> [ASP.net](https://msdn.microsoft.com/library/yh26yfzy.aspx) Kimlik, kullanıcılarınızın kimlik bilgilerini uygulama tarafından oluşturulan bir veritabanında depolar. Kullanıcılarınız oturum açarken, uygulamayı veritabanını okuyarak kimlik bilgilerini doğrular. Projenizin *Hesap* klasörü, üyelik: kaydolma, oturum açma, parolayı değiştirme ve erişimi yetkilendirme gibi çeşitli bölümleri uygulayan dosyaları içerir. Ayrıca, ASP.NET Web Forms OAuth ve OpenID 'yi destekler. Bu kimlik doğrulama geliştirmeleri, kullanıcıların, Facebook, Twitter, Windows Live ve Google gibi hesapların mevcut kimlik bilgilerini kullanarak sitenizde oturum açmasına olanak tanır.
> 
> ![Projeyi oluşturma-Çözüm Gezgini (ASP.NET Identity)](create-the-project/_static/image7.png)
> 
> Varsayılan olarak, şablon, Web için Visual Studio Express 2013 ile birlikte sunulan geliştirme veritabanı sunucusu olan SQL Server Express LocalDB örneğinde varsayılan veritabanı adı kullanarak bir üyelik veritabanı oluşturur.
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx) , bir SQL Server veritabanının birçok programlama özelliğine sahip SQL Server basit bir sürümüdür. SQL Server Express LocalDB, kullanıcı modunda çalışır ve yükleme önkoşullarını kısa bir listesi olan hızlı, sıfır özellikli bir yüklemeye sahiptir. Microsoft SQL Server, herhangi bir veritabanı veya Transact-SQL kodu SQL Server Express LocalDB 'den SQL Server ve SQL Azure herhangi bir yükseltme adımı olmadan taşınabilir. Bu nedenle, SQL Server Express LocalDB, tüm SQL Server sürümlerini hedefleyen uygulamalar için bir geliştirici ortamı olarak kullanılabilir. SQL Server Express LocalDB, saklı yordamlar, Kullanıcı tanımlı işlevler ve toplamalar, .NET Framework tümleştirme, uzamsal türler ve SQL Server Compact kullanılamayan diğerleri gibi özelliklere izin vermez.
> 
> **Ana Sayfalar**
> 
> Bir [ASP.NET ana sayfası](https://msdn.microsoft.com/library/wtxbf3hh.aspx) , uygulamanızdaki tüm sayfalar için tutarlı bir görünüm ve davranış tanımlar. Ana sayfanın düzeni, kullanıcının gördüğü son sayfayı oluşturmak için, tek bir içerik sayfasından içerik birleştirir. Wingtip Toys uygulamasında, Wingtip Toys Web sitesindeki tüm sayfaların aynı ayırıcı logoyu ve gezinti çubuğunu paylaşmasını sağlamak için *site. Master* ana sayfasını değiştirirsiniz.
> 
> **HTML5**
> 
> ASP.NET Web Forms uygulama şablonu, HTML biçimlendirme dilinin en son sürümü olan [HTML5](http://www.w3schools.com/html/html5_intro.asp)'yi destekler. HTML5, Web siteleri oluşturmayı kolaylaştıran yeni öğeleri ve işlevleri destekler.
> 
> **Modernize**
> 
> HTML5 desteği olmayan tarayıcılarda [Modernizr](http://www.modernizr.com/)' yi kullanabilirsiniz. Modernizr, tarayıcıların HTML5 özelliklerini destekleyip desteklemediğini tespit eden açık kaynaklı bir JavaScript kitaplığıdır ve değilse bunları etkinleştirebilir. ASP.NET Web Forms uygulama şablonunda, Modernizr bir NuGet paketi olarak yüklenir.
> 
> **Yükleyebilirsiniz**
> 
> Visual Studio 2013 proje şablonları, Twitter tarafından oluşturulan bir düzen ve tema çerçevesi olan [önyükleme](http://getbootstrap.com/)'yi kullanır. Bootstrap, yanıt veren tasarım sağlamak için CSS3 kullanır, bu da mizanpajlar farklı tarayıcı pencere boyutlarına dinamik olarak uyum sağlayabilir. Uygulamanın görünüm veya hisde bir değişikliği kolay bir şekilde uygulamak için önyükleme 'nin Tema özelliğini de kullanabilirsiniz. Varsayılan olarak, Visual Studio 2013 ASP.NET Web uygulaması şablonu, bir NuGet paketi olarak önyükleme içerir.
> 
> **NuGet paketleri**
> 
> ASP.NET Web Forms uygulama şablonu bir [NuGet](http://www.nuget.org/) paketleri kümesi içerir. Bu paketler, açık kaynak kitaplıkları ve araçları biçiminde bileşen işlevlerini sağlar. Uygulamalarınızı oluşturmanıza ve test etmenize yardımcı olacak çok çeşitli paketler vardır. Visual Studio, NuGet paketlerini eklemeyi, kaldırmayı ve güncelleştirmeyi kolaylaştırır. Geliştiriciler ayrıca NuGet 'e paket oluşturup ekleyebilir.
> 
> ![Proje-NuGet Iletişim kutusunu oluşturma](create-the-project/_static/image8.png)
> 
> Bir paket yüklediğinizde NuGet dosyaları çözümünüze kopyalar ve başvuruları ekleme ve Web uygulamanızla ilişkili yapılandırmayı değiştirme gibi her türlü değişikliği otomatik olarak yapar. Kitaplığı kaldırmaya karar verirseniz, NuGet dosyaları kaldırır ve ikincil değer kalmayacak şekilde projenizde yaptığınız değişiklikleri ters çevirir. NuGet, Visual Studio 'daki **Araçlar** menüsünden kullanılabilir.
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/) , Hızlı Web GELIŞTIRME için HTML belgesi geçiş, olay işleme, animasyon uygulama ve Ajax etkileşimleri kolaylaştıran hızlı ve kısa bir JavaScript kitaplığıdır. JQuery JavaScript kitaplığı, ASP.NET Web Forms uygulama şablonuna bir NuGet paketi olarak dahildir.
> 
> **Unobtrusive doğrulaması**
> 
> Yerleşik Doğrulayıcı denetimleri, istemci tarafı doğrulama mantığı için unobtrusive JavaScript kullanmak üzere yapılandırılmıştır. Bu, sayfa biçimlendirmesinde satır içi işlenen JavaScript miktarını önemli ölçüde azaltır ve toplam sayfa boyutunu azaltır. Unobtrusive doğrulaması, uygulamanın kökündeki *Web. config* dosyasının &lt;appSettings&gt; öğesindeki ayara bağlı olarak, ASP.NET Web Forms uygulama şablonuna Global olarak eklenir.
> 
> **Entity Framework Code First**
> 
> ASP.NET Web Forms uygulama şablonundaki özelliklerin yanı sıra, Wingtip Toys uygulaması, verilerle çalışırken kod merkezli geliştirmeyi sağlayan bir NuGet kitaplığı olan [Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)kullanır. Basitçe, yazdığınız koda göre sizin için uygulamanızın veritabanı bölümünü oluşturur. Entity Framework kullanarak verileri kesin olarak belirlenmiş nesneler olarak alır ve işlersiniz. Bu, verilere nasıl erişildiğine ilişkin ayrıntılar yerine uygulamanızdaki iş mantığına odaklanmanızı sağlar.
> 
> ASP.NET Web Forms şablonuna dahil edilen yüklü kitaplıklar ve paketler hakkında daha fazla bilgi için, yüklü NuGet paketleri listesine bakın. Bunu yapmak için, Visual Studio 'Da yeni bir Web Forms projesi oluşturun, **araçlar** > **nuget Paket Yöneticisi** > **çözüm için NuGet Paketlerini Yönet**' i seçin ve **NuGet Paketlerini Yönet** iletişim kutusunda **yüklü paketler** ' i seçin.

### <a name="touring-visual-studio"></a>Touring Visual Studio

Visual Studio 'daki birincil pencereler **Çözüm Gezgini**, **Sunucu Gezgini** (Express 'Teki**veritabanı Gezgini** ), **Özellikler penceresini**, araç **kutusunu**, **araç çubuğunu**ve **belge penceresini**içerir.

![Proje-NuGet Iletişim kutusunu oluşturma](create-the-project/_static/image9.png)

Visual Studio hakkında daha fazla bilgi için bkz. Visual [Web Developer Visual Guide](https://msdn.microsoft.com/library/ee410104.aspx).

## <a name="summary"></a>Özet

Bu öğreticide, varsayılan Web Forms uygulamasını oluşturup gözden geçirdikten sonra çalıştırın. Varsayılan Web formları uygulamasının farklı özelliklerini incelendi ve Visual Studio ortamının nasıl kullanılacağına ilişkin bazı temel bilgileri öğrendiniz. Aşağıdaki öğreticilerde veri erişim katmanını oluşturacaksınız.

## <a name="additional-resources"></a>Ek Kaynaklar

[Doğru programlama modelini seçme](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
Web [uygulaması projeleri Web sitesi projelerine karşı](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web Forms sayfalarına genel bakış](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [Önceki](introduction-and-overview.md)
> [İleri](create_the_data_access_layer.md)
