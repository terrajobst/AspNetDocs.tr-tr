---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: Veri erişim katmanını oluşturma | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575744"
---
# <a name="create-the-data-access-layer"></a>Veri Erişim Katmanını Oluşturma

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, ASP.NET Web Forms ve Code First Entity Framework kullanarak bir veritabanında veri oluşturma, erişme ve gözden geçirme açıklanmaktadır. Bu öğretici, önceki öğreticide "Projeyi oluşturma" ve Wingtip oyuncak mağaza öğreticisi serisinin bir parçası olarak oluşturulur. Bu öğreticiyi tamamladığınızda, projenin *modeller* klasöründe olan bir veri erişim sınıfları grubu oluşturacaksınız.

## <a name="what-youll-learn"></a>Şunları öğreneceksiniz:

- Veri modellerini oluşturma.
- Veritabanını başlatma ve çekirdek oluşturma.
- Veritabanını desteklemek için uygulamayı güncelleştirme ve yapılandırma.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>Öğreticide sunulan özellikler şunlardır:

- Entity Framework Code First
- Yerel Veritabanı
- Veri Açıklamaları

## <a name="creating-the-data-models"></a>Veri modellerini oluşturma

[Entity Framework](https://msdn.microsoft.com/data/aa937723) , nesne ilişkisel eşleme (ORM) çerçevesidir. Genellikle yazmanız gereken veri erişimi kodunun çoğunu ortadan kaldırarak, ilişkisel verilerle nesne olarak çalışmanıza olanak sağlar. Entity Framework kullanarak, [LINQ](https://msdn.microsoft.com/library/bb397926.aspx)kullanarak sorgular verebilir, ardından verileri kesin olarak belirlenmiş nesneler olarak alabilir ve işleyebilirsiniz. LINQ, verileri sorgulamak ve güncelleştirmek için desenler sağlar. Entity Framework kullanmak, veri erişim temelleri üzerine odaklanmak yerine uygulamanızın geri kalanını oluşturmaya odaklanabilmenizi sağlar. Bu öğretici serisinde daha sonra, verileri nasıl kullanacağınızı, gezinti ve ürün sorgularını doldurmak için göstereceğiz.

Entity Framework, *Code First*adlı bir geliştirme paradigmasını destekler. Code First, sınıfları kullanarak veri modellerinizi tanımlamanıza olanak sağlar. Sınıf, diğer türlerin, yöntemlerin ve olayların değişkenlerini birlikte gruplandırarak kendi özel türlerinizi oluşturmanızı sağlayan bir yapıdır. Sınıfları varolan bir veritabanıyla eşleyebilir veya bir veritabanı oluşturmak için kullanabilirsiniz. Bu öğreticide, veri modeli sınıfları yazarak veri modellerini oluşturacaksınız. Daha sonra, bu yeni sınıflardan anında veritabanını Entity Framework oluşturmaya izin vereceksiniz.

Web Forms uygulaması için veri modellerini tanımlayan varlık sınıfları oluşturarak başlarsınız. Daha sonra varlık sınıflarını yöneten ve veritabanına veri erişimi sağlayan bir bağlam sınıfı oluşturacaksınız. Ayrıca, veritabanını doldurmak için kullanacağınız bir başlatıcı sınıfı oluşturacaksınız.

### <a name="entity-framework-and-references"></a>Entity Framework ve başvurular

Varsayılan olarak, **Web Forms** şablonunu kullanarak yeni bir **ASP.NET Web uygulaması** oluşturduğunuzda Entity Framework dahil edilir. Entity Framework, bir NuGet paketi olarak yüklenebilir, kaldırılabilir ve güncelleştirilebilen olabilir.

Bu NuGet paketi, projenizde aşağıdaki **çalışma zamanı** derlemelerini içerir:

- EntityFramework. dll – Entity Framework tarafından kullanılan tüm ortak çalışma zamanı kodları
- EntityFramework. SqlServer. dll – Entity Framework için Microsoft SQL Server sağlayıcısı

### <a name="entity-classes"></a>Varlık sınıfları

Verilerin şemasını tanımlamak için oluşturduğunuz sınıflar varlık sınıfları olarak adlandırılır. Veritabanı tasarımına yeni başladıysanız varlık sınıflarını bir veritabanının tablo tanımları olarak düşünün. Sınıftaki her bir özellik, veritabanının tablosundaki bir sütunu belirtir. Bu sınıflar, nesne odaklı kod ve veritabanının ilişkisel tablo yapısı arasında basit, nesne ilişkisel bir arabirim sağlar.

Bu öğreticide, ürünler ve kategoriler için şemaları temsil eden basit varlık sınıfları ekleyerek başlayacaksınız. Products sınıfı her ürün için tanımlar içerir. Ürün sınıfının her üyesinin adı `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`ve `Category`olacaktır. Kategori sınıfı, bir ürünün ait olduğu her bir kategorinin, otomobil, bot veya düzlem gibi tanımlar içerir. Kategori sınıfının her üyesinin adı `CategoryID`, `CategoryName`, `Description`ve `Products`olacaktır. Her ürün kategorilerden birine ait olacaktır. Bu varlık sınıfları projenin mevcut *modeller* klasörüne eklenecektir.

1. **Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın ve ardından **Yeni öğe**&gt; -**Ekle** ' yi seçin. 

    ![Veri erişim katmanını oluşturma-yeni öğe menüsü](create_the_data_access_layer/_static/image1.png)

   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Soldaki **yüklü** bölmeden **görsel C#**  ' ün altında **kod**' u seçin. 

    ![Veri erişim katmanını oluşturma-yeni öğe menüsü](create_the_data_access_layer/_static/image2.png)
3. Orta bölmeden **sınıf** ' ı seçin ve bu yeni sınıfı *Product.cs*olarak adlandırın.
4. **Ekle**'yi tıklatın.  
   Yeni sınıf dosyası düzenleyicide görüntülenir.
5. Varsayılan kodu şu kodla değiştirin:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 1 ile 4 arasındaki adımları tekrarlayarak başka bir sınıf oluşturun, yeni sınıfı *category.cs* olarak adlandırın ve varsayılan kodu şu kodla değiştirin:  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

Daha önce belirtildiği gibi, `Category` sınıfı uygulamanın satış için tasarlandığı ürün türünü temsil eder ( <a id="a"></a>&quot;otomobiller&quot;, &quot;Boats&quot;, &quot;Rockets&quot;vb.) ve `Product` sınıfı veritabanındaki bireysel ürünleri (Toys) temsil eder. Bir `Product` nesnesinin her örneği, ilişkisel veritabanı tablosundaki bir satıra karşılık gelir ve ürün sınıfının her özelliği ilişkisel veritabanı tablosundaki bir sütunla eşlenir. Bu öğreticide daha sonra veritabanında bulunan ürün verilerini gözden geçireceğiz.

### <a name="data-annotations"></a>Veri Açıklamaları

Sınıfların belirli üyelerinin, `[ScaffoldColumn(false)]`gibi, üyeyle ilgili ayrıntıları belirten özniteliklere sahip olduğunu fark etmiş olabilirsiniz. Bunlar *veri ek açıklamalardır*. Veri ek açıklaması öznitelikleri, bu üye için Kullanıcı girişinin nasıl doğrulandığını tanımlayabilir, bu üyeye yönelik biçimlendirmeyi belirtebilir ve veritabanı oluşturulduğunda nasıl modellendirildiğini belirtebilir.

### <a name="context-class"></a>Bağlam Sınıfı

Veri erişimi için sınıfları kullanmaya başlamak için bir bağlam sınıfı tanımlamanız gerekir. Daha önce belirtildiği gibi, bağlam sınıfı varlık sınıflarını (`Product` sınıfı ve `Category` sınıfı) yönetir ve veritabanına veri erişimi sağlar.

Bu yordam modeller klasörüne yeni C# bir bağlam sınıfı ekler .

1. *Modeller* klasörüne sağ tıklayın ve ardından **yeni öğe**&gt; -**Ekle** ' yi seçin.   
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Orta bölmeden **sınıf** ' ı seçin, *ProductContext.cs* olarak adlandırın ve **Ekle**' ye tıklayın.
3. Sınıfında bulunan varsayılan kodu aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

Bu kod, kesin olarak belirlenmiş nesnelerle çalışarak verileri sorgulama, ekleme, güncelleştirme ve silme özelliğini içeren Entity Framework tüm çekirdek işlevlerine erişebilmeniz için `System.Data.Entity` ad alanını ekler.

`ProductContext` sınıfı, veritabanında `Product` sınıf örneklerinin getirmeyi, depolanmasını ve güncelleştirilmesini işleyen Entity Framework ürün veritabanı bağlamını temsil eder. `ProductContext` sınıfı Entity Framework tarafından sunulan `DbContext` taban sınıftan türetilir.

### <a name="initializer-class"></a>Başlatıcı sınıfı

Bağlam ilk kez kullanıldığında veritabanını başlatmak için bazı özel mantık çalıştırmanız gerekir. Bu, ürünleri ve kategorileri hemen görüntüleyebilmeniz için çekirdek verilerin veritabanına eklenmesine izin verir.

Bu yordam modeller klasörüne yeni C# bir başlatıcı sınıfı ekler .

1. *Modeller* klasöründe başka bir `Class` oluşturun ve *ProductDatabaseInitializer.cs*olarak adlandırın.
2. Sınıfında bulunan varsayılan kodu aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

Yukarıdaki koddan görebileceğiniz gibi, veritabanı oluşturulup başlatıldığında `Seed` özelliği geçersiz kılınır ve ayarlanır. `Seed` özelliği ayarlandığında, Kategoriler ve ürünlerdeki değerler veritabanını doldurmak için kullanılır. Veritabanı oluşturulduktan sonra yukarıdaki kodu değiştirerek çekirdek verileri güncelleştirmeye çalışırsanız, Web uygulamasını çalıştırdığınızda hiçbir güncelleştirme görmezsiniz. Bu nedenle, yukarıdaki kod, çekirdek verileri sıfırlamadan önce modelin (şema) değişip değişmediğini tanımak için `DropCreateDatabaseIfModelChanges` sınıfının bir uygulamasını kullanır. `Category` ve `Product` varlık sınıflarında hiçbir değişiklik yapılmadığından, veritabanı çekirdek verilerle yeniden başlatılır.

> [!NOTE] 
> 
> Uygulamayı her çalıştırışınızda veritabanının yeniden oluşturulmasını istediyseniz, `DropCreateDatabaseIfModelChanges` sınıfı yerine `DropCreateDatabaseAlways` sınıfını kullanabilirsiniz. Bununla birlikte, bu öğretici serisi için `DropCreateDatabaseIfModelChanges` sınıfını kullanın.

Bu öğreticide, dört yeni sınıfa ve bir varsayılan sınıfa sahip bir *modeller* klasörünüze sahip olursunuz:

![Veri erişim katmanı-modeller klasörünü oluşturma](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>Uygulamayı veri modelini kullanacak şekilde yapılandırma

Artık verileri temsil eden sınıfları oluşturduğunuza göre, uygulamayı sınıfları kullanacak şekilde yapılandırmanız gerekir. *Global. asax* dosyasında, modeli başlatan kodu eklersiniz. *Web. config* dosyasında, uygulamanın yeni veri sınıfları tarafından temsil edilen verileri depolamak için hangi veritabanına kullanacağınızı belirten bilgileri eklersiniz. *Global. asax* dosyası, uygulama olaylarını veya yöntemlerini işlemek için kullanılabilir. *Web. config* dosyası, ASP.NET Web uygulamanızın yapılandırmasını denetlemenize olanak tanır.

#### <a name="updating-the-globalasax-file"></a>Global. asax dosyası güncelleştiriliyor

Uygulama başlatıldığında veri modellerini başlatmak için, *Global.asax.cs* dosyasında `Application_Start` işleyicisini güncelleşolursunuz.

> [!NOTE] 
> 
> Çözüm Gezgini, *Global.asax.cs* dosyasını düzenlemek için *Global. asax* dosyasını veya *Global.asax.cs* dosyasını seçebilirsiniz.

1. *Global.asax.cs* dosyasındaki `Application_Start` yöntemine sarıya vurgulanan aşağıdaki kodu ekleyin.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> Tarayıcınız, bu öğretici serisini bir tarayıcıda görüntülerken sarı renkle vurgulanmış kodu görüntülemek için HTML5 'yi desteklemelidir.

Yukarıdaki kodda gösterildiği gibi, uygulama başladığında, uygulama ilk kez veriye erişildiğinde çalıştırılacak başlatıcıyı belirtir. `Database` nesnesine ve `ProductDatabaseInitializer` nesnesine erişmek için iki ek ad alanı gerekir.

 Web. config dosyasını değiştirme 

Entity Framework Code First veritabanı çekirdek verilerle doldurulduğu zaman varsayılan bir konumda sizin için bir veritabanı oluşturacak olsa da, uygulamanıza kendi bağlantı bilgilerinizi eklemek, veritabanı konumunu denetlemenizi sağlar. Bu veritabanı bağlantısını, projenin kökündeki uygulamanın *Web. config* dosyasında bir bağlantı dizesi kullanarak belirtirsiniz. Yeni bir bağlantı dizesi ekleyerek veritabanının konumunu (*wingtiptoys. mdf*) varsayılan konumu yerine uygulamanın veri dizininde (*App\_verileri*) oluşturulacak şekilde yönlendirebilirsiniz. Bu değişikliğin yapılması, bu öğreticide daha sonra veritabanı dosyasını bulmanıza ve incelemenize olanak sağlayacak.

1. **Çözüm Gezgini**, *Web. config* dosyasını bulun ve açın.
2. Sarı olarak vurgulanan bağlantı dizesini *Web. config* dosyasının `<connectionStrings>` bölümüne aşağıdaki gibi ekleyin:  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

Uygulama ilk kez çalıştırıldığında, veritabanı bağlantı dizesi tarafından belirtilen konumda oluşturulur. Ancak uygulamayı çalıştırmadan önce, önce oluşturalım.

## <a name="building-the-application"></a>Uygulama Oluşturma

Web uygulamanızdaki tüm sınıfların ve değişikliklerin çalıştığından emin olmak için uygulamayı derlemeniz gerekir.

1. **Hata Ayıkla** menüsünde, **Build wingtiptoys**' u seçin.  
 **Çıkış** penceresi görüntülenir ve hepsi de varsa, *başarılı* bir ileti görürsünüz.  

    ![Veri erişim katmanı çıkış pencerelerini oluşturma](create_the_data_access_layer/_static/image4.png)

Bir hata halinde çalıştırırsanız yukarıdaki adımları yeniden denetleyin. **Çıkış** penceresindeki bilgiler, hangi dosyanın bir sorun olduğunu ve dosyada bir değişikliğin gerekli olduğunu gösterir. Bu bilgiler, yukarıdaki adımların projenizde neleri gözden geçirilmesi ve düzeltilmesi gerektiğini belirlemenizi sağlar.

## <a name="summary"></a>Özet

Serinin Bu öğreticide, veri modeli oluşturdunuz ve ayrıca veritabanını başlatmak ve temel almak için kullanılacak kodu eklediniz. Uygulamayı, uygulama çalıştırıldığında veri modellerini kullanmak için de yapılandırdınız.

Sonraki öğreticide, Kullanıcı arabirimini güncelleştireceğiz, gezinti ekleyecek ve veritabanından veri alacaksınız. Bu, veritabanının bu öğreticide oluşturduğunuz varlık sınıflarına göre otomatik olarak oluşturulmasını sağlayacaktır.

## <a name="additional-resources"></a>Ek Kaynaklar

[Entity Framework genel bakış](https://msdn.microsoft.com/library/bb399567.aspx)   
[Başlangıç Kılavuzu, ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907)   
[Entity Framework Ile geliştirme Code First](http://www.msteched.com/2010/Europe/DEV212) (video)   
[Code First Ilişkiler AKıCı apı](https://msdn.microsoft.com/data/hh134698)   
[Code First veri açıklamaları](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework için üretkenlik Iyileştirmeleri](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [Önceki](create-the-project.md)
> [İleri](ui_and_navigation.md)
