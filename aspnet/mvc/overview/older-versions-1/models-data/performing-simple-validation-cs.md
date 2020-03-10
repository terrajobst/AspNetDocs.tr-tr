---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: Basit doğrulama (C#) gerçekleştiriliyor | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC uygulamasında doğrulama gerçekleştirmeyi öğrenin. Bu öğreticide, Stephen Walther size durumu ve doğrulama HTML Yardımcısı 'nı modelleyebilir...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: e33f522af74efe97b5a245e956bc0b918ea769af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542996"
---
# <a name="performing-simple-validation-c"></a>Basit Doğrulama Gerçekleştirme (C#)

ile [Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC uygulamasında doğrulama gerçekleştirmeyi öğrenin. Bu öğreticide, Stephen Walther, size durumu ve doğrulama HTML yardımcılarını modelleyebilir.

Bu öğreticinin amacı, bir ASP.NET MVC uygulaması içinde nasıl doğrulama gerçekleştirebileceğini açıklamaktır. Örneğin, bir kullanıcının gerekli bir alan için değer içermeyen bir form göndermesini nasıl önleyeceğinizi öğrenirsiniz. Model durumunun ve doğrulama HTML yardımcılarını nasıl kullanacağınızı öğrenirsiniz.

## <a name="understanding-model-state"></a>Model durumunu anlama

Doğrulama hatalarını göstermek için model durumunu veya daha doğru bir şekilde model durumu sözlüğünü kullanırsınız. Örneğin, liste 1 ' deki oluştur () eylemi, ürün sınıfını bir veritabanına eklemeden önce ürün sınıfının özelliklerini doğrular.

Doğrulama veya veritabanı mantığınızı bir denetleyiciye eklemenizi önermiyor. Denetleyicinin yalnızca uygulama akış denetimiyle ilgili mantığı içermesi gerekir. Şeyleri basit tutmaya yönelik bir kısayol sunuyoruz.

**Listeleme 1-Controllers\ProductController.cs**

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

Liste 1 ' de, ürün sınıfının ad, açıklama ve UnitsInStock özellikleri onaylanır. Bu özelliklerden herhangi biri doğrulama testinde başarısız olursa, model durumu sözlüğüne bir hata eklenir (Controller sınıfının ModelState özelliği tarafından temsil edilir).

Model durumunda herhangi bir hata varsa ModelState. IsValid özelliği false değerini döndürür. Bu durumda, yeni ürün oluşturmaya yönelik HTML formu yeniden görüntülenir. Aksi takdirde, doğrulama hatası yoksa, yeni ürün veritabanına eklenir.

## <a name="using-the-validation-helpers"></a>Doğrulama yardımcıları kullanma

ASP.NET MVC Framework iki doğrulama yardımcıları içerir: HTML. ValidationMessage () Yardımcısı ve HTML. ValidationSummary () Yardımcısı. Doğrulama hata iletilerini görüntülemek için bu iki yardımcıları bir görünümde kullanırsınız.

HTML. ValidationMessage () ve HTML. ValidationSummary () yardımcıları, ASP.NET MVC scafkatlaması tarafından otomatik olarak oluşturulan oluşturma ve düzenleme görünümlerinde kullanılır. Oluşturma görünümü oluşturmak için aşağıdaki adımları izleyin:

1. Ürün denetleyicisindeki oluştur () eylemine sağ tıklayın ve **Görünüm Ekle** menü seçeneğini belirleyin (bkz. Şekil 1).
2. **Görünüm Ekle** iletişim kutusunda, **türü kesin belirlenmiş görünüm oluştur** onay kutusunu Işaretleyin (bkz. Şekil 2).
3. **Veri sınıfı görüntüle** açılan listesinden ürün sınıfını seçin.
4. **Içeriği görüntüle** açılan listesinden oluştur ' u seçin.
5. **Ekle** düğmesine tıklayın.

Bir görünüm eklemeden önce uygulamanızı derlediğinizden emin olun. Aksi takdirde, sınıf listesi **veri sınıfı görüntüle** açılan listesinde görünmez.

[Yeni proje iletişim kutusunu ![](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)

**Şekil 01**: Görünüm ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-simple-validation-cs/_static/image2.png))

[Yeni proje iletişim kutusunu ![](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)

**Şekil 02**: türü kesin belirlenmiş bir görünüm oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-simple-validation-cs/_static/image4.png))

Bu adımları tamamladıktan sonra, liste 2 ' de oluştur görünümü alırsınız.

**Listeleme 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

Liste 2 ' de HTML. ValidationSummary () Yardımcısı HTML formunun hemen üzerinde çağrılır. Bu yardımcı, doğrulama hata iletilerinin listesini göstermek için kullanılır. HTML. ValidationSummary () Yardımcısı, hataları madde işaretli bir listede işler.

HTML. ValidationMessage () Yardımcısı HTML form alanlarının her birinin yanında çağırılır. Bu yardımcı, bir form alanının hemen yanında bir hata mesajı göstermek için kullanılır. Liste 2 olduğunda, HTML. ValidationMessage () Yardımcısı bir hata olduğunda bir yıldız işareti görüntüler.

Şekil 3 ' teki sayfa, form eksik alanlarla gönderildiğinde ve geçersiz değerlerle doğrulama yardımcıları tarafından işlenen hata iletilerini gösterir.

[Yeni proje iletişim kutusunu ![](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)

**Şekil 03**: sorun Ile gönderilen oluşturma görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-simple-validation-cs/_static/image6.png))

Bir doğrulama hatası olduğunda HTML giriş alanlarının görünümünün de değiştirildiğine dikkat edin. HTML. TextBox () Yardımcısı tarafından işlenen özellik ile ilişkili bir doğrulama hatası olduğunda HTML. TextBox () Yardımcısı bir *class = "Input-Validation-Error"* özniteliği işler.

Doğrulama hatalarının görünüşünü denetlemek için kullanılan üç geçişli stil sayfası sınıfı vardır:

- giriş-doğrulama-hata-HTML. TextBox () Yardımcısı tarafından oluşturulan &lt;Input&gt; etiketine uygulandı.
- alan-doğrulama-hata-HTML. ValidationMessage () Yardımcısı tarafından oluşturulan &lt;span&gt; etiketine uygulandı.
- Doğrulama-Özet-hatalar-HTML. ValidationSummary () Yardımcısı tarafından oluşturulan &lt;ul&gt; etiketine uygulandı.

Bu geçişli stil sayfası sınıflarını değiştirebilir ve bu nedenle Içerik klasöründe bulunan site. css dosyasını değiştirerek doğrulama hatalarının görünümünü değiştirebilirsiniz.

> [!NOTE] 
> 
> HtmlHelper sınıfı, doğrulamayla ilgili CSS sınıflarının adlarını almak için salt okunurdur statik özellikler içerir. Bu statik özellikler Validationınputcssclassname, ValidationFieldCssClassName ve ValidationSummaryCssClassName olarak adlandırılır.

## <a name="prebinding-validation-and-postbinding-validation"></a>Ön bağlama doğrulama ve Postbinding doğrulaması

Bir ürün oluşturmak için HTML formunu gönderirseniz ve Price alanı için geçersiz bir değer girip UnitsInStock alanı için değer yoksa, Şekil 4 ' te, doğrulama iletilerini alırsınız. Bu doğrulama hata iletileri nereden geliyor?

[Yeni proje iletişim kutusunu ![](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)

**Şekil 04**: doğrulama hatalarını önceden bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-simple-validation-cs/_static/image8.png))

Aslında iki tür doğrulama hatası iletisi vardır. HTML form alanları bir sınıfa bağlanmadan önce oluşturulan ve form alanları sınıfa bağlandıktan sonra oluşturulan bunlar. Diğer bir deyişle, önceden bağlama doğrulama hataları ve geri bağlama doğrulama hataları vardır.

Liste 1 ' de ürün denetleyicisi tarafından kullanıma sunulan Create () eylemi, ürün sınıfının bir örneğini kabul eder. Create yönteminin imzası şöyle görünür:

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

Oluştur formundaki HTML form alanlarının değerleri, model Ciltçi adlı bir şey ile productToCreate sınıfına bağlanır. Varsayılan model Ciltçi, form özelliğine form alanı bağladığı zaman otomatik olarak model durumuna bir hata iletisi ekler.

Varsayılan model Ciltçi, "Apple" dizesini ürün sınıfının Price özelliğine bağlayamıyor. Bir Decimal özelliğine dize atayamazsınız. Bu nedenle, model Ciltçi model durumuna bir hata ekler.

Varsayılan model Bağlayıcısı aynı zamanda null değeri boş değer kabul etmayan bir özelliğe atayamaz. Özellikle model Ciltçi, UnitsInStock özelliğine null değer atayamayabilir. Model cildi bir kez daha ve model durumuna bir hata iletisi ekler.

Bu önceden bağlama hata iletilerinin görünümünü özelleştirmek istiyorsanız, bu iletiler için kaynak dizeleri oluşturmanız gerekir.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, ASP.NET MVC çerçevesinde doğrulamanın temel iskeikleri tanımlamakta. Model durumunun ve doğrulama HTML yardımcılarını nasıl kullanacağınızı öğrendiniz. Ayrıca, ön bağlama ve postbinding doğrulaması arasındaki ayrımı ele alınmaktadır. Diğer öğreticilerde, doğrulama kodunuzu Denetleyicilerinizden ve model sınıflarınıza taşımaya yönelik çeşitli stratejileri tartışacağız.

> [!div class="step-by-step"]
> [Önceki](displaying-a-table-of-database-data-cs.md)
> [İleri](validating-with-the-idataerrorinfo-interface-cs.md)
