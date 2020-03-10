---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: UI ve gezinti | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: ac1dcaf1ba911fdcaeb3845c6836ec771733d93e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643558"
---
# <a name="ui-and-navigation"></a>Kullanıcı Arabirimi ve Gezinti

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, varsayılan Web uygulamasının Kullanıcı arabirimini Wingtip Toys Store ön uygulamasının özelliklerini destekleyecek şekilde değiştirirsiniz. Ayrıca, basit ve veri bağlantılı gezinme ekleyeceksiniz. Bu öğretici, önceki öğreticide "veri erişim katmanını oluşturma" ve Wingtip Toys öğretici serisinin bir parçası olarak oluşturulur.

## <a name="what-youll-learn"></a>Öğrenecekleriniz:

- Kullanıcı arabirimini, Wingtip Toys mağaza ön uygulamasının özelliklerini destekleyecek şekilde değiştirme.
- Sayfa gezintisi eklemek için HTML5 öğesi yapılandırma.
- Belirli ürün verilerine gitmek için veri odaklı denetim oluşturma.
- Entity Framework Code First kullanılarak oluşturulan bir veritabanındaki verileri görüntüleme.

ASP.NET Web Forms, Web uygulamanız için dinamik içerik oluşturmanıza izin verir. Her bir ASP.NET Web sayfası, statik HTML Web sayfasına (sunucu tabanlı işleme dahil olmayan bir sayfa) benzer şekilde oluşturulur, ancak ASP.NET Web sayfası, bir sayfa çalıştırıldığında, ASP.NET tarafından tanıdığı ve işlenen ek öğeleri içerir.

Statik HTML sayfası ( *. htm* veya *. html* dosyası) ile sunucu, dosyayı okuyup tarayıcıya olduğu gibi göndererek bir `Web` isteği yerine getirir. Buna karşılık, birisi bir ASP.NET Web sayfası ( *. aspx* dosyası) istediğinde, sayfa Web sunucusunda bir program olarak çalışır. Sayfa çalışırken, Web sitenizin gerektirdiği, değerleri hesaplama, veritabanı bilgilerini okuma veya yazma ya da diğer programları çağırma gibi her türlü görevi gerçekleştirebilir. Çıktısı olarak, sayfa dinamik olarak biçimlendirme (HTML içindeki öğeler gibi) oluşturur ve bu dinamik çıktıyı tarayıcıya gönderir.

## <a name="modifying-the-ui"></a>Kullanıcı arabirimini değiştirme

*Varsayılan. aspx* sayfasını değiştirerek bu öğretici serisine devam edersiniz. Uygulamayı oluşturmak için kullanılan varsayılan şablon tarafından zaten belirlenen kullanıcı arabirimini değiştirirsiniz. Yaptığınız değişikliklerin türü, herhangi bir Web Forms uygulaması oluştururken tipik bir uygulamadır. Bu, başlığı değiştirerek, bazı içerikleri değiştirerek ve gereksiz varsayılan içeriği kaldırarak bunu yapacaksınız.

1. *Default. aspx* sayfasını açın veya değiştirin.
2. Sayfa **Tasarım** görünümünde görünürse, **kaynak** görünümüne geçin.
3. `@Page` yönergesinin sayfanın üst kısmında, aşağıda sarı renkle gösterildiği gibi `Title` özniteliğini "hoş geldiniz" olarak değiştirin. 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. Ayrıca *default. aspx* sayfasında, biçimlendirmenin aşağıdaki gibi görünmesi için `<asp:Content>` etiketinde bulunan tüm varsayılan içeriği değiştirin. 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. *Varsayılan. aspx* sayfasını **Dosya** menüsünden **default. aspx** ' i seçerek kaydedin.

   Elde edilen *default. aspx* sayfası şu şekilde görünür: 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

Örnekte, `@Page` yönergesinin `Title` özniteliğini ayarlamış olursunuz. HTML bir tarayıcıda görüntülendiğinde, sunucu kodu `<%: Page.Title %>` `Title` özniteliğinde yer alan içeriğe çözümlenir.

Örnek sayfa, bir ASP.NET Web sayfası oluşturan temel öğeleri içerir. Bu sayfa, bir HTML sayfasında sahip olabileceğiniz gibi, ASP.NET 'e özgü öğelerle birlikte statik metin içerir. *Default. aspx* sayfasında bulunan içerik, Bu öğreticinin ilerleyen kısımlarında açıklanacak olan ana sayfa içeriğiyle tümleştirilir.

### <a name="page-directive"></a>@Page yönergesi

ASP.NET Web Forms, genellikle sayfa özelliklerini ve sayfa için yapılandırma bilgilerini belirtmenize imkan tanıyan yönergeleri içerir. Yönergeler, ASP.NET tarafından, sayfanın nasıl işlenediğine ilişkin yönergeler olarak kullanılır, ancak tarayıcıya gönderilen biçimlendirmenin bir parçası olarak işlenmez.

En yaygın olarak kullanılan yönerge, aşağıdaki gibi, sayfa için birçok yapılandırma seçeneği belirtmenize olanak sağlayan `@Page` yönergedir:

1. Sayfadaki kod için sunucu programlama dili gibi C#.
2. Sayfada, tek dosya sayfası olarak adlandırılan veya ayrı bir sınıf dosyasında kod içeren bir sayfa olup olmadığı, bu sayfanın arka plan kod sayfası olarak adlandırılan bir sayfa olup olmadığı.
3. Sayfanın ilişkili ana sayfası olup olmadığı ve bu nedenle bir içerik sayfası olarak değerlendirilme.
4. Hata ayıklama ve izleme seçenekleri.

Sayfada bir `@Page` yönergesi eklemezseniz veya yönerge belirli bir ayarı içermiyorsa, *Web. config* yapılandırma dosyasından veya *Machine. config* yapılandırma dosyasından bir ayar devralınır. *Machine. config* dosyası, bir makinede çalışan tüm uygulamalara ek yapılandırma ayarları sağlar.

> [!NOTE] 
> 
> *Machine. config* Ayrıca tüm olası yapılandırma ayarları hakkında ayrıntılar sağlar.

### <a name="web-server-controls"></a>Web sunucusu denetimleri

Çoğu ASP.NET Web Forms uygulamada, kullanıcının sayfayla etkileşime geçmesini sağlayan denetimler, metin kutuları, listeler ve benzeri denetimler eklersiniz. Bu Web sunucusu denetimleri, HTML düğmelerine ve giriş öğelerine benzer. Ancak, sunucu üzerinde işlenir ve bu, özelliklerini ayarlamak için sunucu kodunu kullanmanıza olanak sağlar. Bu denetimler Ayrıca sunucu kodunda işleyebilmeniz gereken olayları da yükseltir.

Sunucu denetimleri, ASP.NET tarafından sayfa çalışırken tanıdığı özel bir sözdizimi kullanır. ASP.NET Server denetimleri için etiket adı bir `asp:` önekiyle başlar. Bu, ASP.NET 'in bu sunucu denetimlerini tanımasını ve işlemesini sağlar. Denetim .NET Framework bir parçası değilse önek farklı olabilir. ASP.NET Server denetimleri, `asp:` ön ekine ek olarak `runat="server"` özniteliğini ve sunucu kodundaki denetime başvurmak için kullanabileceğiniz bir `ID` da içerir.

Sayfa çalıştığında, ASP.NET sunucu denetimlerini tanımlar ve bu denetimlerle ilişkili kodu çalıştırır. Birçok denetim, bir tarayıcıda görüntülenirken sayfada bazı HTML veya diğer biçimlendirmeleri işler.

### <a name="server-code"></a>Sunucu kodu

Çoğu ASP.NET Web Forms uygulama, sayfa işlendiğinde sunucuda çalışan kodu içerir. Yukarıda belirtildiği gibi, sunucu kodu bir ListView denetimine veri ekleme gibi çeşitli şeyler yapmak için kullanılabilir. ASP.NET, Visual Basic, J# ve diğerleri dahil C#olmak üzere sunucuda çalıştırılacak birçok dili destekler.

ASP.NET, bir Web sayfası için sunucu kodu yazmak üzere iki modeli destekler. Tek dosya modelinde, sayfanın kodu, açılış etiketinin `runat="server"` özniteliğini içerdiği bir betik öğesidir. Alternatif olarak, sayfa için kodu arka plan kod modeli olarak adlandırılan ayrı bir sınıf dosyasında oluşturabilirsiniz. Bu durumda, ASP.NET Web Forms sayfası genellikle sunucu kodu içermez. Bunun yerine, `@Page` yönergesi *. aspx* sayfasını ilişkili arka plan kod dosyası ile bağlayan bilgiler içerir.

`@Page` yönergesinde bulunan `CodeBehind` özniteliği ayrı sınıf dosyasının adını belirtir ve `Inherits` özniteliği, sayfaya karşılık gelen arka plan kod dosyası içindeki sınıfın adını belirtir.

### <a name="updating-the-master-page"></a>Ana sayfa güncelleştiriliyor

ASP.NET Web Forms 'de, ana sayfalar uygulamanızdaki sayfalar için tutarlı bir düzen oluşturmanızı sağlar. Tek bir ana sayfa, uygulamanızdaki tüm sayfalar (veya bir sayfa grubu) için istediğiniz görünüm ve standart davranışı tanımlar. Daha sonra, yukarıda açıklandığı şekilde, göstermek istediğiniz içeriği içeren bireysel içerik sayfaları oluşturabilirsiniz. Kullanıcılar içerik sayfalarını istediğinde, ASP.NET, ana sayfanın yerleşimini içerik sayfasındaki içerikle birleştiren çıktıyı oluşturmak için ana sayfayla birleştirir.

Yeni sitenin her sayfada görüntülemesi için tek bir logo olması gerekir. Bu logoyu eklemek için ana sayfada HTML 'yi değiştirebilirsiniz.

1. **Çözüm Gezgini**, **site. Master** sayfasını bulup açın.
2. Sayfa **Tasarım** görünümsayfaiçeriyorsa **kaynak** görünümüne geçin.
3. Sarı renkle vurgulanmış biçimlendirmeyi **değiştirerek veya ekleyerek** ana sayfayı güncelleştirin: 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

Bu HTML, daha sonra ekleyeceğiniz Web uygulamasının *Images* klasöründen *logo. jpg* adlı görüntüyü görüntüler. Ana sayfayı kullanan bir sayfa bir tarayıcıda görüntülenirken, logo görüntülenir. Kullanıcı logoya tıklarsa, Kullanıcı *default. aspx* sayfasına geri gidecektir. `<a>` HTML tutturucu etiketi, görüntü sunucusu denetimini sarmalanmış ve görüntünün bağlantının bir parçası olarak dahil edilmesini sağlar. Tutturucu etiketinin `href` özniteliği, Web sitesinin "`~/`" kökünü bağlantı konumu olarak belirtir. Varsayılan olarak, Kullanıcı Web sitesinin köküne gittiğinde *varsayılan. aspx* sayfası görüntülenir. **Image** `<asp:Image>` Server Control, bir TARAYıCıDA görüntülenirken HTML olarak işlenen `BorderStyle`gibi ekleme özelliklerini içerir.

### <a name="master-pages"></a>Ana Sayfalar

Ana sayfa,. Master uzantısına sahip bir ASP.NET dosyasıdır (örneğin, *site. Master*) statik metın, HTML öğeleri ve sunucu denetimleri içerebilen önceden tanımlanmış bir düzen ile. Ana sayfa, sıradan *. aspx* sayfaları için kullanılan `@Page` yönergesinin yerini alan özel bir `@Master` yönergesi tarafından tanımlanır.

`@Master` yönergesine ek olarak ana sayfa, bir sayfa için `html`, `head`ve `form`gibi en üst düzey HTML öğelerini de içerir. Örneğin, yukarıda eklediğiniz ana sayfada düzen için bir HTML `table`, şirket logosu için bir `img` öğesi, statik metin ve sunucu denetimleri sitenizin ortak üyeliğini işleyecek şekilde kullanılır. Ana sayfanızın bir parçası olarak herhangi bir HTML ve ASP.NET öğesini kullanabilirsiniz.

Tüm sayfalarda görünecek statik metin ve denetimlerin yanı sıra, ana sayfa bir veya daha fazla **ContentPlaceHolder** denetimi de içerir. Bu yer tutucu denetimleri, değiştirilebilen içeriğin görüneceği bölgeleri tanımlar. Sırasıyla, **içerik sunucu denetimini** kullanarak *varsayılan. aspx*gibi içerik sayfalarında değiştirilebilir içerik tanımlanmıştır.

#### <a name="adding-image-files"></a>Görüntü dosyaları ekleme

Yukarıda başvurulan logo resminin, tüm ürün görüntüleriyle birlikte Web uygulamasına eklenmesi gerekir, böylece proje bir tarayıcıda görüntülenirken görünebilirler.

#### <a name="download-from-msdn-samples-site"></a>MSDN örnekleri sitesinden indir:

[ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) ile çalışmaya başlama

İndirme, örnek uygulamayı oluşturmak için kullanılan *wingtiptoys-varlıklar* klasöründeki kaynakları içerir.

1. Daha önce yapmadıysanız, MSDN örnekleri sitesindeki yukarıdaki bağlantıyı kullanarak sıkıştırılmış örnek dosyaları indirin.
2. İndirildikten sonra,. zip dosyasını açın ve içeriği makinenizde yerel bir klasöre kopyalayın.
3. *Wingtiptoys-varlıklar* klasörünü bulun ve açın.
4. Sürükleyip bırakarak, *Katalog* klasörünü yerel klasörünüzden, Visual Studio 'Nun **Çözüm Gezgini** Web uygulaması projesinin köküne kopyalayın. 

    ![UI ve gezinti-dosyaları Kopyala](ui_and_navigation/_static/image1.png)
5. Sonra, **Çözüm Gezgini** ' de **wingtiptoys** projesine sağ tıklayıp, **Yeni klasör**&gt; **Ekle** -' yi seçerek *resimler* adlı yeni bir klasör oluşturun.
6. *Logo. jpg* dosyasını **Dosya Gezgini** 'ndeki *wingtiptoys-varlıklar* klasöründen, Visual Studio 'nun **Çözüm Gezgini** Web uygulaması projesinin *görüntüler* klasörüne kopyalayın.
7. Yeni dosyaları görmüyorsanız dosya listesini güncelleştirmek için **Çözüm Gezgini** en üstündeki **tüm dosyaları göster** seçeneğine tıklayın.  
  
    **Çözüm Gezgini** artık güncelleştirilmiş proje dosyalarını gösterir. 

    ![UI ve gezinti-Çözüm Gezgini](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>Sayfa ekleme

Web uygulamasına gezinti eklemeden önce, önce gidilecek iki yeni sayfa ekleyeceksiniz. Bu öğretici serisinde daha sonra, bu yeni sayfalarda ürünler ve ürün ayrıntıları görüntülenir.

1. **Çözüm Gezgini**' de **wingtiptoys**' a sağ tıklayın, **Ekle**' ye tıklayın ve ardından **Yeni öğe**' ye tıklayın.   
 **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **Visual C#**  -&gt; **Web** şablonları grubunu seçin. Ardından, orta listeden **Ana sayfa Ile Web formu** ' nu seçin ve *ProductList. aspx*olarak adlandırın. 

    ![UI ve gezinti-yeni öğe Ekle Iletişim kutusu](ui_and_navigation/_static/image3.png)
3. Ana sayfayı yeni oluşturulan *. aspx* sayfasına eklemek için **site. Master** ' u seçin. 

    ![UI ve gezinti-ana sayfa seç](ui_and_navigation/_static/image4.png)
4. Aynı adımları izleyerek *ProductDetails. aspx* adlı ek bir sayfa ekleyin.

### <a name="updating-bootstrap"></a>Önyükleme güncelleştiriliyor

Visual Studio 2013 proje şablonları, Twitter tarafından oluşturulan bir düzen ve tema çerçevesi olan [önyükleme](http://getbootstrap.com/)'yi kullanır. Bootstrap, yanıt veren tasarım sağlamak için CSS3 kullanır, bu da mizanpajlar farklı tarayıcı pencere boyutlarına dinamik olarak uyum sağlayabilir. Uygulamanın görünüm veya hisde bir değişikliği kolay bir şekilde uygulamak için önyükleme 'nin Tema özelliğini de kullanabilirsiniz. Varsayılan olarak, Visual Studio 2013 ASP.NET Web uygulaması şablonu, bir NuGet paketi olarak önyükleme içerir.

Bu öğreticide, önyükleme CSS dosyalarını değiştirerek Wingtip Toys uygulamasının görünümünü değiştireceksiniz.

1. **Çözüm Gezgini**, *içerik* klasörünü açın.
2. *Bootstrap. css* dosyasına sağ tıklayın ve *bootstrap-Original. css*olarak yeniden adlandırın.
3. *Bootstrap. min. css* öğesini *bootstrap-Original. min. css*olarak yeniden adlandırın.
4. **Çözüm Gezgini**, *içerik* klasörüne sağ tıklayıp **klasörü dosya Gezgini 'nde aç**' ı seçin.  
   Dosya Gezgini görüntülenir. İndirilen önyükleme CSS dosyalarını bu konuma kaydetmelisiniz.
5. Tarayıcınızda [https://bootswatch.com/3/](https://bootswatch.com/3/)' a gidin.
6. Tarayıcı penceresini, Ceruyalın temayı görene kadar kaydırın. 

    ![UI ve gezinti-Ceruyalın teması](ui_and_navigation/_static/image5.png)
7. Hem *Bootstrap. css* dosyasını hem de *Bootstrap. min. css* dosyasını *içerik* klasörüne indirin. Daha önce açtığınız **Dosya Gezgini** penceresinde görüntülenen içerik klasörünün yolunu kullanın.
8. **Çözüm Gezgini**en üstünde bulunan **Visual Studio** 'da, içerik klasöründeki yeni dosyaları görüntülemek için **tüm dosyaları göster** seçeneğini belirleyin. 

    ![UI ve gezinti-Çözüm Gezgini](ui_and_navigation/_static/image6.png)

   **İçerik** klasöründe ıkı yeni CSS dosyası görürsünüz, ancak her dosya adının yanında bulunan simgenin gri olduğunu fark edeceksiniz. Bu, dosyanın henüz projeye eklenmemiş olduğu anlamına gelir.
9. *Bootstrap. css* ve *Bootstrap. min. css* dosyalarını sağ tıklatın ve **projeye dahil et**' i seçin.   
   Bu öğreticide daha sonra Wingtip Toys uygulamasını çalıştırdığınızda yeni kullanıcı arabirimi görüntülenir.

> [!NOTE] 
> 
> ASP.NET Web uygulaması şablonu, önyükleme CSS dosyalarının yolunu depolamak için projenin kökündeki *paket. config* dosyasını kullanır.

### <a name="modifying-the-default-navigation"></a>Varsayılan gezintiyi değiştirme

Uygulamadaki her sayfa için varsayılan gezinti, *site. Master* sayfasında yer alan sırasız gezinti listesi öğesi değiştirilerek değiştirilebilir.

1. **Çözüm Gezgini**, *site. Master* sayfasını bulun ve açın.
2. Sarı renkle vurgulanmış ek gezinti bağlantısını aşağıda gösterilen sırasız listeye ekleyin:   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

Yukarıdaki HTML 'de görebileceğiniz gibi, bir bağlantı `href` özniteliğiyle bir tutturucu `<a>` etiketi içeren `<li>` her satır öğesini değiştirdiniz. Her `href` Web uygulamasındaki bir sayfaya işaret eder. Tarayıcıda, bir Kullanıcı bu bağlantılardan birine tıkladığında ( **Ürünler**gibi), `href` bulunan sayfaya ( **ProductList. aspx**gibi) gider. Bu öğreticinin sonunda uygulamayı çalıştıracaksınız.

> [!NOTE] 
> 
> Tilde (`~`) karakteri, `href` yolunun projenin kökünde başlayacağını belirtmek için kullanılır.

### <a name="adding-a-data-control-to-display-navigation-data"></a>Gezinti verilerini göstermek için veri denetimi ekleme

Bundan sonra, veritabanındaki tüm kategorileri görüntüleyecek bir denetim ekleyeceksiniz. Her kategori, *ProductList. aspx* sayfasına bir bağlantı görevi görür. Kullanıcı tarayıcıda bir kategori bağlantısına tıkladığında, Ürünler sayfasına gidebilir ve yalnızca seçili kategori ile ilişkili ürünleri görürler.

Veritabanında bulunan tüm kategorileri göstermek için bir **ListView** denetimi kullanacaksınız. Ana sayfaya bir **ListView** denetimi eklemek için:

1. *Site. Master* sayfasında, daha önce eklediğiniz `id="TitleContent"` içeren `<div>` öğeden **sonra** aşağıdaki vurgulanmış `<div>` öğesini ekleyin:  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

Bu kod, veritabanındaki tüm kategorileri görüntüler. **ListView** denetimi her kategori adını bağlantı metni olarak görüntüler ve kategorinin `ID` içeren bir Query-String değeri olan *ProductList. aspx* sayfasına bir bağlantı içerir. **ListView** denetimindeki `ItemType` özelliğini ayarlayarak, veri bağlama ifadesi `Item` `ItemTemplate` düğümünde kullanılabilir ve denetim kesin bir şekilde türdedir. `Item` nesnenin ayrıntılarını IntelliSense kullanarak `CategoryName`belirtme gibi seçebilirsiniz. Bu kod, bir veri bağlama ifadesini işaretleyen `<%#: %>` kapsayıcı içinde yer alır. Ekleyerek (:) `<%#` önekinin sonuna kadar, veri bağlama ifadesinin sonucu HTML kodlu olur. Sonuç HTML kodlandığında, uygulamanız siteler arası betik ekleme (XSS) ve HTML ekleme saldırılarına karşı daha iyi korunur.

> [!NOTE] 
> 
> **İpucu**
> 
> Geliştirme sırasında yazarak kod eklediğinizde, kesin belirlenmiş veri denetimleri IntelliSense 'e göre kullanılabilir üyeleri gösterebileceğinden nesnenin geçerli bir üyesinin bulunduğundan emin olabilirsiniz. IntelliSense, özellikler, Yöntemler ve nesneler gibi kod yazarken, içeriğe uygun kod seçenekleri sunar.

Sonraki adımda, verileri almak için `GetCategories` yöntemini uygulayacaksınız.

### <a name="linking-the-data-control-to-the-database"></a>Veri denetimini veritabanına bağlama

Veri denetimindeki verileri görüntülemeden önce veri denetimini veritabanına bağlamanız gerekir. Bağlantıyı yapmak için, *site.Master.cs* dosyasının arkasındaki kodu değiştirebilirsiniz.

1. **Çözüm Gezgini**, *site. Master* sayfasına sağ tıklayın ve sonra **kodu görüntüle**' ye tıklayın. *Site.Master.cs* dosyası düzenleyicide açılır.
2. *Site.Master.cs* dosyasının başlangıcına yakın bir şekilde, eklenen tüm ad alanlarının aşağıdaki gibi görünmesi için iki ek ad alanı ekleyin:  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. `Page_Load` olay işleyicisinden sonra vurgulanan `GetCategories` yöntemini aşağıdaki şekilde ekleyin:  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

Yukarıdaki kod, ana sayfayı kullanan herhangi bir sayfa tarayıcıya yüklendiğinde yürütülür. Bu öğreticide daha önce eklediğiniz `ListView` denetimi ("categoryList" adlı), verileri seçmek için model bağlamayı kullanır. `ListView` denetimin biçimlendirmesinde, denetimin `SelectMethod` özelliğini yukarıda gösterilen `GetCategories` yöntemine ayarlarsınız. `ListView` denetimi, `GetCategories` yöntemini sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. Sonraki öğreticide verileri bağlama hakkında daha fazla bilgi edineceksiniz.

### <a name="running-the-application-and-creating-the-database"></a>Uygulamayı çalıştırma ve veritabanı oluşturma

Bu öğretici serisinin başlarında, bir başlatıcı sınıfı oluşturdunuz ("Productdatabaseınitializer" adlı) ve bu sınıfı *Global.asax.cs* dosyasında belirttiniz. Entity Framework, *Global.asax.cs* dosyasında bulunan `Application_Start` yöntemi Başlatıcı sınıfını çağıracağından, uygulama ilk kez çalıştırıldığında veritabanını oluşturacaktır. Başlatıcı sınıfı, veritabanını oluşturmak için bu öğretici serisinde daha önce eklediğiniz model sınıflarını (`Category` ve `Product`) kullanır.

1. **Çözüm Gezgini**, *default. aspx* sayfasına sağ tıklayıp **Başlangıç sayfası olarak ayarla**' yı seçin.
2. Visual Studio 'da **F5**tuşuna basın.   
 Bu ilk çalıştırma sırasında her şeyi ayarlamak biraz zaman alabilir.   
    ![UI ve gezinti tarayıcısı Windows](ui_and_navigation/_static/image7.png)  
 Uygulamayı çalıştırdığınızda uygulama derlenir ve *wingtiptoys. mdf* adlı veritabanı *App\_Data* klasöründe oluşturulur. Tarayıcıda bir kategori gezinti menüsü görürsünüz. Bu menü, veritabanından kategorileri alarak oluşturulmuştur. Sonraki öğreticide, gezintiyi uygulayacaksınız.
3. Çalışan uygulamayı durdurmak için tarayıcıyı kapatın.

### <a name="reviewing-the-database"></a>Veritabanını gözden geçirme

*Web. config* dosyasını açın ve bağlantı dizesi bölümüne bakın. Bağlantı dizesindeki `AttachDbFilename` değerinin, Web uygulaması projesi için `DataDirectory` işaret ettiğini görebilirsiniz. `|DataDirectory|` değeri, projedeki *App\_Data* klasörünü temsil eden ayrılmış bir değerdir. Bu klasör, varlık sınıflarınızda oluşturulmuş olan veritabanının bulunduğu yerdir.

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> *Uygulama\_veri* klasörü görünür değilse veya klasör boşsa, **Yenile** simgesini ve ardından **Çözüm Gezgini** penceresinin en üstündeki **tüm dosyaları göster** simgesini seçin. **Çözüm Gezgini** pencerelerin genişliğini genişletmek, kullanılabilir tüm simgeleri göstermek için gerekli olabilir.

Artık, **Sunucu Gezgini** penceresini kullanarak *wingtiptoys. mdf* veritabanı dosyasında bulunan verileri inceleyebilirsiniz.

1. *Uygulama\_veri* klasörünü genişletin. *Uygulama\_veri* klasörü görünür değilse yukarıdaki nota bakın.
2. *Wingtiptoys. mdf* veritabanı dosyası görünür değilse, **Yenile** simgesini ve ardından **Çözüm Gezgini** penceresinin en üstündeki **tüm dosyaları göster** simgesini seçin.
3. *Wingtiptoys. mdf* veritabanı dosyasına sağ tıklayın ve **Aç**' ı seçin.  
    **Sunucu Gezgini** görüntülenir. 

    ![UI ve gezinti-Sunucu Gezgini](ui_and_navigation/_static/image8.png)
4. *Tablolar* klasörünü genişletin.
5. **Ürünler**tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.  
 **Products** tablosu görüntülenir. 

    ![UI ve gezinti-ürünler tablosu](ui_and_navigation/_static/image9.png)
6. Bu görünüm, **Products** tablosundaki verileri el ile görmenizi ve değiştirmenizi sağlar.
7. **Ürünler** Tablosu penceresini kapatın.
8. **Sunucu Gezgini**, **Ürünler** tablosuna tekrar sağ tıklayın ve **tablo tanımını aç**' ı seçin.  
 **Products** tablosu için veri tasarımı görüntülenir. 

    ![UI ve gezinti-ürün tasarımı](ui_and_navigation/_static/image10.png)
9. **T-SQL** sekmesinde, tabloyu oluşturmak IÇIN kullanılan SQL DDL ifadesini görürsünüz. Şemayı değiştirmek için **Tasarım** sekmesindeki Kullanıcı arabirimini de kullanabilirsiniz.
10. **Sunucu Gezgini** **wingtiptoys** veritabanı ' na sağ tıklayın ve **Bağlantıyı kapat**' ı seçin.   
 Veritabanını Visual Studio 'dan ayırarak, veritabanı şeması bu öğretici serisinde daha sonra değiştirilebilir.
11. **Sunucu Gezgini** penceresinin altındaki **Çözüm Gezgini** sekmesini seçerek **Çözüm Gezgini**döndürün.

## <a name="summary"></a>Özet

Serinin bu öğreticisinde bazı temel kullanıcı arabirimi, grafikler, sayfalar ve gezinti eklediniz. Ayrıca, önceki öğreticide eklediğiniz veri sınıflarından veritabanını oluşturan Web uygulamasını çalıştırdınız. Ayrıca veritabanını doğrudan görüntüleyerek veritabanının *Ürünler* tablosunun içeriğini de görüntüleyebilirsiniz. Sonraki öğreticide, veritabanından veri öğeleri ve Ayrıntılar görüntülenecektir.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web sayfalarına programlama  giriş](https://msdn.microsoft.com/library/ms178125.aspx)  
[ASP.NET Web sunucusu denetimlerine genel bakış](https://msdn.microsoft.com/library/zsyt68f1.aspx)   
[CSS öğreticisi](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [Önceki](create_the_data_access_layer.md)
> [İleri](display_data_items_and_details.md)
