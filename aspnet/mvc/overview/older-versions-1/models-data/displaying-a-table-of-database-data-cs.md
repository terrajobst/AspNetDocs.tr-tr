---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: Veritabanı verilerinin tablosunu görüntüleme (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticide, bir veritabanı kayıtları kümesini görüntülemenin iki yöntemini gösterdim. Bir HTML ta veritabanı kaydı kümesini biçimlendirmek için iki yöntem göster...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c908d030076fc8400190ef3cf1672632ac1ed6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543143"
---
# <a name="displaying-a-table-of-database-data-c"></a>Veritabanı Verilerinin Tablosunu Görüntüleme (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> Bu öğreticide, bir veritabanı kayıtları kümesini görüntülemenin iki yöntemini gösterdim. Bir HTML tablosunda veritabanı kayıtlarının bir kümesini biçimlendirmek için iki yöntem gösteriyorum. İlk olarak, veritabanı kayıtlarını doğrudan bir görünüm içinde nasıl biçimlendirmek istediğinizi göstereceğiz. Daha sonra, veritabanı kayıtlarını biçimlendirirken partiden nasıl yararlanabildiğini gösteririm.

Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında bir HTML tablosu veritabanı verilerinin nasıl görüntüleneceğini açıklamaktır. İlk olarak, bir kayıt kümesini otomatik olarak görüntüleyen bir görünüm oluşturmak için Visual Studio 'ya dahil olan yapı iskelesi araçlarını nasıl kullanacağınızı öğreneceksiniz. Daha sonra, veritabanı kayıtlarını biçimlendirirken kısmen şablon olarak nasıl kullanacağınızı öğrenirsiniz.

## <a name="create-the-model-classes"></a>Model sınıfları oluşturma

Film veritabanı tablosundan kayıt kümesini görüntüleyeceğiz. Filmler veritabanı tablosu şu sütunları içerir:

<a id="0.3_table01"></a>

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar (200) | False |
| Direktörü | NVarchar (50) | False |
| Davterekiralık | DateTime | False |

ASP.NET MVC uygulamamızda film tablosunu göstermek için bir model sınıfı oluşturmanız gerekir. Bu öğreticide, model Sınıflarımızı oluşturmak için Microsoft Entity Framework kullanırız.

> [!NOTE] 
> 
> Bu öğreticide, Microsoft Entity Framework kullanırız. Ancak, LINQ to SQL, Nhazırda Beklet veya ADO.NET gibi bir ASP.NET MVC uygulamasından veritabanıyla etkileşim kurmak için çeşitli farklı teknolojiler kullanacağınızı anlamak önemlidir.

Varlık Veri Modeli sihirbazını başlatmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresinde modeller klasörüne sağ tıklayın ve menü seçeneğini belirleyin **, yeni öğe**' yi seçin.
2. **Veri** kategorisini seçin ve **ADO.net varlık veri modeli** şablonunu seçin.
3. Veri modelinize *MoviesDBModel. edmx* adını verin ve **Ekle** düğmesine tıklayın.

Ekle düğmesine tıkladıktan sonra Varlık Veri Modeli Sihirbazı görüntülenir (bkz. Şekil 1). Sihirbazı tamamladıktan sonra aşağıdaki adımları izleyin:

1. **Model Içeriğini seçin** adımında, **veritabanından oluştur** seçeneğini belirleyin.
2. **Veri bağlantınızı seçin** adımında, bağlantı ayarları için *MoviesDB. mdf* veri bağlantısını ve *MoviesDBEntities* adını kullanın. **İleri** düğmesine tıklayın.
3. **Veritabanı nesnelerinizi seçin** adımında, tablolar düğümünü genişletin, filmler tablosunu seçin. Ad alanı *modellerini* girin ve **son** düğmesine tıklayın.

[LINQ to SQL sınıfları oluşturma ![](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**Şekil 01**: LINQ to SQL sınıfları oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image2.png))

Varlık Veri Modeli Sihirbazı 'nı tamamladıktan sonra, Varlık Veri Modeli Tasarımcısı açılır. Tasarımcı, filmler varlığını görüntülemelidir (bkz. Şekil 2).

[Varlık Veri Modeli tasarımcısını ![](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**Şekil 02**: varlık veri modeli Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image4.png))

Devam etmeden önce bir değişiklik yapmanız gerekiyor. Varlık verileri Sihirbazı, filmler veritabanı tablosunu temsil eden *filmler* adlı bir model sınıfı oluşturur. Film sınıfını belirli bir filmi temsil etmek üzere kullanacağımız için, sınıf *adını film yerine* *film* (plural yerine tekil) olarak değiştirmemiz gerekiyor.

Tasarımcı yüzeyinde sınıfın adına çift tıklayın ve filmden film olarak sınıfın adını değiştirin. Bu değişikliği yaptıktan sonra, film sınıfını oluşturmak için **Kaydet** düğmesine (disketin simgesine) tıklayın.

## <a name="create-the-movies-controller"></a>Filmler denetleyicisini oluşturma

Veritabanı kayıtlarınızı göstermek için bir yol olduğuna göre, film koleksiyonunu döndüren bir denetleyici oluşturuyoruz. Visual Studio Çözüm Gezgini penceresinde, denetleyiciler klasörüne sağ tıklayın ve **Ekle, denetleyici** (bkz. Şekil 3) menü seçeneğini belirleyin.

[Denetleyici Ekle menüsünü ![](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**Şekil 03**: denetleyici Ekle menüsü ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image6.png))

**Denetleyici Ekle** iletişim kutusu göründüğünde, denetleyici adı moviecontroller (bkz. Şekil 4) girin. Yeni denetleyiciyi eklemek için **Ekle** düğmesine tıklayın.

[Denetleyici Ekle iletişim kutusunu ![](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**Şekil 04**: denetleyici Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image8.png))

Veritabanı kayıtlarının kümesini döndürmesi için film denetleyicisi tarafından kullanıma sunulan dizin () eylemini değiştirmemiz gerekiyor. Denetleyiciyi, liste 1 ' deki denetleyiciye benzemek üzere değiştirin.

**Listeleme 1 – Controllers\MovieController.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

Liste 1 ' de, MoviesDBEntities sınıfı MoviesDB veritabanını temsil etmek için kullanılır. Bu sınıfı kullanmak için, MvcApplication1. modeller ad alanını şöyle içeri aktarmanız gerekir:

MvcApplication1. modellerini kullanma;

İfade *varlıkları. MovieSet. ToList ()* , filmler veritabanı tablosundan tüm filmler kümesini döndürür.

## <a name="create-the-view"></a>Görünümü oluşturun

Bir HTML tablosunda veritabanı kayıtlarının bir kümesini görüntülemenin en kolay yolu, Visual Studio tarafından sunulan yapı iskelesi avantajlarından faydalanır.

**Oluşturma, çözüm oluşturma**menü seçeneğini belirleyerek uygulamanızı oluşturun. **Görünümü Ekle** iletişim kutusunu açmadan önce uygulamanızı oluşturmanız gerekir, aksi durumda veri sınıflarınız iletişim kutusunda görünmez.

Dizin () eylemine sağ tıklayın ve **Görünüm Ekle** menü seçeneğini belirleyin (bkz. Şekil 5).

[![görünüm ekleme](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**Şekil 05**: Görünüm ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image10.png))

**Görünüm Ekle** iletişim kutusunda, **türü kesin belirlenmiş görünüm oluştur**onay kutusunu işaretleyin. **Görünüm Verisi sınıfı**olarak film sınıfını seçin. **İçeriği görüntüle** ' *yi seçin (* bkz. Şekil 6). Bu seçeneklerin belirlenmesi, filmlerin listesini görüntüleyen kesin türü belirtilmiş bir görünüm oluşturur.

[Görünüm Ekle iletişim kutusu ![](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**Şekil 06**: Görünüm Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image12.png))

**Ekle** düğmesine tıkladıktan sonra, liste 2 ' deki görünüm otomatik olarak oluşturulur. Bu görünüm, film koleksiyonu boyunca yinelemek için gereken kodu içerir ve bir filmin her bir özelliğini görüntüler.

**Listeleme 2 – Views\movie\ındex.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

Uygulamayı, **Hata Ayıkla, hata ayıklamayı Başlat** (veya F5 tuşuna basarak) menü seçeneğini belirleyerek çalıştırabilirsiniz. Uygulamanın çalıştırılması Internet Explorer 'ı başlatır. /Movie URL 'sine gittiğinizde, Şekil 7 ' de sayfayı görürsünüz.

[Bir film tablosu ![](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**Şekil 07**: bir film tablosu ([tam boyutlu görüntüyü görüntülemek için tıklayın](displaying-a-table-of-database-data-cs/_static/image14.png))

Şekil 7 ' de veritabanı kayıtlarının kılavuzunun görünümü hakkında herhangi bir şey beğenmezseniz, Dizin görünümünü yalnızca değiştirebilirsiniz. Örneğin, Dizin görünümünü *değiştirerek, izin ver üst bilgisini* *Yayınlanan Tarih* olarak değiştirebilirsiniz.

## <a name="create-a-template-with-a-partial"></a>Kısmi ile şablon oluşturma

Bir görünüm çok karmaşık olduğunda, görünümü parçalara bölmek iyi bir fikirdir. Parals kullanımı, görünümlerinizin anlaşılması ve bakımını kolaylaştırır. Film veritabanı kayıtlarının her birini biçimlendirmek için şablon olarak kullanılabilecek bir kısmi oluşturacağız.

Kısmi oluşturmak için aşağıdaki adımları izleyin:

1. Views\Movie klasörüne sağ tıklayın ve **Görünüm Ekle**menü seçeneğini belirleyin.
2. *Kısmi görünüm oluştur (. ascx)* onay kutusunu işaretleyin.
3. Kısmi *Movietemplate*adını adlandırın.
4. **Kesin olarak belirlenmiş bir görünüm oluşturma**etiketli onay kutusunu işaretleyin.
5. *Görünüm Verisi sınıfı*olarak filmi seçin.
6. *Görünüm içeriği*olarak boş ' ı seçin.
7. Projenize kısmi olarak eklemek için **Ekle** düğmesine tıklayın.

Bu adımları tamamladıktan sonra, MovieTemplate bölümünü, liste 3 gibi görünecek şekilde değiştirin.

**Listeleme 3 – Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

Listeleme 3 ' te kısmi tek bir kayıt satırı için şablon içerir.

Liste 4 ' te değiştirilen dizin görünümü, MovieTemplate kısmi kullanır.

**Listeleme 4 – Views\movie\ındex.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

Liste 4 ' teki görünüm, tüm filmlerde yinelenen bir foreach döngüsü içerir. Her film için, filmi biçimlendirmek için MovieTemplate kısmi kullanılır. MovieTemplate, RenderPartial () yardımcı yöntemi çağırarak işlenir.

Değiştirilen dizin görünümü, veritabanı kayıtlarının çok aynı HTML tablosunu işler. Ancak, görünüm büyük ölçüde basitleştirilmiştir.

RenderPartial () yöntemi bir dize döndürmediğinden diğer yardımcı yöntemlerin çoğundan farklı. Bu nedenle,% HTML. RenderPartial () &lt;kullanarak RenderPartial () yöntemini çağırmanız gerekir. %&gt; yerine &lt;% = HTML. RenderPartial (); %&gt;.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, bir HTML tablosunda bir dizi veritabanı kaydını nasıl kullanabileceğinizi açıklamaktır. İlk olarak, Microsoft Entity Framework avantajlarından yararlanarak bir denetleyici eyleminden bir veritabanı kayıtları kümesini döndürmeyi öğrendiniz. Daha sonra, bir öğe koleksiyonunu otomatik olarak görüntüleyen bir görünüm oluşturmak için Visual Studio scafkatlamayı nasıl kullanacağınızı öğrendiniz. Son olarak, kısmi avantajlarından yararlanarak görünümü nasıl basitleştireceğinizi öğrendiniz. Her bir veritabanı kaydını biçimlendirebilmeniz için kısmen şablon olarak nasıl kullanacağınızı öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](creating-model-classes-with-linq-to-sql-cs.md)
> [İleri](performing-simple-validation-cs.md)
