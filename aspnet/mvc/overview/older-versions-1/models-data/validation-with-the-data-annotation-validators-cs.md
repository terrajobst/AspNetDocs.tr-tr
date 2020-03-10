---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: Veri ek açıklama Doğrulayıcıları ile doğrulamaC#() | Microsoft Docs
author: microsoft
description: Bir ASP.NET MVC uygulaması içinde doğrulama gerçekleştirmek için veri ek açıklaması modeli ciltlerinden yararlanın. Farklı Doğrulayıcı türlerini nasıl kullanacağınızı öğrenin...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: e154384c08adf0c14920afff85e983a67b41707c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542135"
---
# <a name="validation-with-the-data-annotation-validators-c"></a>Veri Ek Açıklama Doğrulayıcıları ile Doğrulama (C#)

[Microsoft](https://github.com/microsoft) tarafından

> Bir ASP.NET MVC uygulaması içinde doğrulama gerçekleştirmek için veri ek açıklaması modeli ciltlerinden yararlanın. Farklı türde Doğrulayıcı özniteliklerini kullanmayı ve bunlarla Microsoft Entity Framework nasıl çalışacağınızı öğrenin.

Bu öğreticide, ASP.NET MVC uygulamasında doğrulama gerçekleştirmek için veri ek açıklaması doğrulayıcılarının nasıl kullanılacağını öğrenirsiniz. Veri ek açıklama Doğrulayıcıları kullanmanın avantajı, bir sınıf özelliğine gerekli veya StringLength özniteliği gibi bir veya daha fazla öznitelik ekleyerek yalnızca doğrulama gerçekleştirmenize olanak sağlamaktır.

Veri ek açıklama Doğrulayıcıları kullanabilmeniz için, veri ek açıklaması modeli cildi indirmeniz gerekir. Veri ek açıklama modeli Ciltçi örneğini [buraya](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)tıklayarak CodePlex Web sitesinden indirebilirsiniz.

Veri ek açıklama modeli bağlayıcısının Microsoft ASP.NET MVC çerçevesinin resmi bir parçası olmadığı anlaşılması önemlidir. Veri ek açıklamaları model Bağlayıcısı Microsoft ASP.NET MVC ekibi tarafından oluşturulmuş olsa da, Microsoft bu öğreticide açıklanan ve kullanılan veri ek açıklaması modeli Bağlayıcısı için resmi ürün desteği sunmaz.

## <a name="using-the-data-annotation-model-binder"></a>Veri ek açıklama modeli cildi kullanma

Veri ek açıklama modelini bir ASP.NET MVC uygulamasında kullanmak için, önce Microsoft. Web. Mvc. Dataaçıklamalarda. dll derlemesine ve System. ComponentModel. Dataaçıklamalarda. dll derlemesine bir başvuru eklemeniz gerekir. Menü seçeneği **projesi, başvuru Ekle ' yi**seçin. Ardından, **Gözden** geçirme sekmesine tıklayın ve veri ek açıklaması modeli Ciltçi örneğini indirdiğiniz (ve sıkıştırmışın) konumuna gidin (bkz. **Şekil 1**).

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**Şekil 1**: veri ek açıklama modeli cilde başvuru ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](validation-with-the-data-annotation-validators-cs/_static/image3.png))

Hem Microsoft. Web. Mvc. Dataek açıklama. dll derlemesini hem de System. ComponentModel. Dataaçıklamalarda. dll derlemesini seçin ve **Tamam** düğmesine tıklayın.

.NET Framework Service Pack 1 ' de bulunan System. ComponentModel. Dataaçıklamalarda. dll derlemesini, veri ek açıklama modeli Bağlayıcısı ile kullanamazsınız. Veri ek açıklaması modeli Ciltçi örnek indirmesi ile birlikte bulunan System. ComponentModel. Dataaçıklamalarda. dll derlemesinin sürümünü kullanmanız gerekir.

Son olarak, Dataek açıklama modeli cildi Global. asax dosyasına kaydetmeniz gerekir. Uygulama\_Start () yönteminin şöyle görünmesi için, uygulama\_Start () olay işleyicisine aşağıdaki kod satırını ekleyin:

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

Bu kod satırı, Ataannotationsmodelciltçi 'yi tüm ASP.NET MVC uygulaması için varsayılan model Ciltçi olarak kaydeder.

## <a name="using-the-data-annotation-validator-attributes"></a>Veri ek açıklaması Doğrulayıcı özniteliklerini kullanma

Veri ek açıklama modeli cildi kullandığınızda doğrulama gerçekleştirmek için doğrulayıcı özniteliklerini kullanırsınız. System. ComponentModel. Dataaçıklamalarda ad alanı aşağıdaki Doğrulayıcı özniteliklerini içerir:

- Aralık: bir özelliğin değerinin belirtilen bir değer aralığı arasında olup olmadığını doğrulamanızı sağlar.
- Cevap içerisinde RegularExpression – bir özelliğin değerinin belirtilen bir normal ifade düzeniyle eşleşip eşleşmediğini doğrulamanızı sağlar.
- Gerekli – bir özelliği gereken şekilde işaretlemenizi sağlar.
- StringLength: dize özelliği için uzunluk üst sınırı belirtmenize olanak sağlar.
- Doğrulama: tüm Doğrulayıcı öznitelikleri için temel sınıf.

> [!NOTE] 
> 
> Doğrulama gereksinimleriniz standart doğrulayıcılar tarafından karşılanmıyorsa, her zaman temel doğrulama özniteliğinden yeni bir doğrulayıcı özniteliği devralarak özel bir doğrulayıcı özniteliği oluşturma seçeneğiniz vardır.

**Liste 1** ' deki ürün sınıfı, Bu Doğrulayıcı özniteliklerinin nasıl kullanılacağını gösterir. Ad, açıklama ve BirimFiyat özellikleri gerekli olarak işaretlenir. Name özelliği 10 karakterden daha az bir dize uzunluğuna sahip olmalıdır. Son olarak, BirimFiyat özelliği bir para birimi miktarını temsil eden bir normal ifade düzeniyle eşleşmelidir.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**Listeleme 1**: Models\product.cs

Ürün sınıfı, bir ek özniteliğin nasıl kullanılacağını gösterir: DisplayName özniteliği. DisplayName özniteliği, özellik bir hata iletisinde görüntülenirken özelliğin adını değiştirmenize olanak sağlar. "BirimFiyat alanı gereklidir" hata iletisini görüntülemek yerine "fiyat alanı gereklidir" hata iletisini görüntüleyebilirsiniz.

> [!NOTE] 
> 
> Doğrulayıcı tarafından görünen hata mesajını tamamen özelleştirmek istiyorsanız, doğrulayıcının ErrorMessage özelliğine şu şekilde özel bir hata iletisi atayabilirsiniz: `<Required(ErrorMessage:="This field needs a value!")>`

Liste **2**' deki oluştur () denetleyici eylemi Ile, **liste 1** ' de ürün sınıfını kullanabilirsiniz. Bu denetleyici eylemi, model durumu herhangi bir hata içerdiğinde oluştur görünümünü yeniden görüntüler.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**Listeleme 2**: Controllers\productcontroller.exe

Son olarak, Create () eylemine sağ tıklayıp **Görünüm Ekle**menü seçeneğini belirleyerek **liste 3** ' te görünümü oluşturabilirsiniz. Model sınıfı olarak ürün sınıfıyla kesin türü belirtilmiş bir görünüm oluşturun. İçeriği görüntüle açılan listesinden **Oluştur** ' u seçin (bkz. **Şekil 2**).

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**Şekil 2**: oluşturma görünümü ekleme

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**Listeleme 3**: Views\product\create.aspx

> [!NOTE] 
> 
> **Görünüm Ekle** menü seçeneği tarafından oluşturulan oluştur formundaki ID alanını kaldırın. Kimlik alanı bir kimlik sütununa karşılık geldiğinden, kullanıcıların bu alan için bir değer girmelerini sağlamak istemezsiniz.

Bir ürün oluşturmak için formu gönderirseniz ve gerekli alanlar için değer girmezseniz, **Şekil 3** ' teki doğrulama hatası iletileri görüntülenir.

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**Şekil 3**: gerekli alanlar eksik

Geçersiz bir para birimi miktarı girerseniz, **Şekil 4** ' te hata iletisi görüntülenir.

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**Şekil 4**: geçersiz para birimi tutarı

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Entity Framework veri ek açıklama Doğrulayıcıları kullanma

Veri modeli sınıflarınızı oluşturmak için Microsoft Entity Framework kullanıyorsanız, bu durumda Doğrulayıcı özniteliklerini doğrudan sınıflarınıza uygulayamazsınız. Entity Framework Designer model sınıfları oluşturduğundan, Tasarımcıda herhangi bir değişiklik yaptığınız sırada model sınıflarında yaptığınız tüm değişiklikler üzerine yazılır.

Doğrulayıcıları Entity Framework tarafından oluşturulan sınıflarla kullanmak istiyorsanız, meta veri sınıfları oluşturmanız gerekir. Doğrulayıcıları, gerçek sınıfa Doğrulayıcıları uygulamak yerine meta veri sınıfına uygularsınız.

Örneğin, Entity Framework kullanarak bir film sınıfı oluşturduğunuzu düşünün (bkz. **Şekil 5**). Ayrıca, film başlığı ve yönetmen özelliklerinin gerekli özellikleri olmasını istediğinizi düşünün. Bu durumda, **Listeleme 4**' te kısmi sınıf ve meta veri sınıfını oluşturabilirsiniz.

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**Şekil 5**: Entity Framework tarafından üretilen film sınıfı

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**Listeleme 4**: Models\movie.cs

**Listeleme 4** ' teki dosya, film ve MovieMetaData adlı iki sınıf içerir. Film sınıfı, kısmi bir sınıftır. DataModel. Designer. vb dosyasında bulunan Entity Framework tarafından oluşturulan kısmi sınıfa karşılık gelir.

Şu anda, .NET Framework kısmi özellikleri desteklemiyor. Bu nedenle, doğrulama özniteliklerini, **Liste 4**' teki dosyada tanımlanan film sınıfının özelliklerine uygulayarak, doğrulama özniteliklerini DataModel. Designer. vb dosyasında tanımlanan film sınıfının özelliklerine uygulamanın bir yolu yoktur.

Film kısmi sınıfının MovieMetaData sınıfına işaret eden bir MetadataType özniteliğiyle donatılmış olduğuna dikkat edin. MovieMetaData sınıfı, film sınıfının özellikleri için proxy özellikleri içerir.

Doğrulayıcı öznitelikleri, MovieMetaData sınıfının özelliklerine uygulanır. Başlık, yönetmen ve dadlı özellikler gerekli özellikler olarak işaretlenir. Director özelliğine 5 ' ten az karakter içeren bir dize atanmalıdır. Son olarak, DisplayName özniteliği, "Yayımlanma tarihi alanı gereklidir" gibi bir hata mesajı göstermek için, Dadterekiralık özelliğine uygulanır. "Dadterekiralık alanı gereklidir" hatası yerine

> [!NOTE] 
> 
> MovieMetaData sınıfındaki proxy özelliklerinin, film sınıfında karşılık gelen özelliklerle aynı türleri temsil etmesi gerekmediğini unutmayın. Örneğin, Director özelliği, film sınıfındaki bir String özelliğidir ve MovieMetaData sınıfında bir nesne özelliğidir.

**Şekil 6** ' daki sayfa, film özellikleri için geçersiz değerler girdiğinizde döndürülen hata iletilerini gösterir.

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**Şekil 6**: Entity Framework ile Doğrulayıcıları kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](validation-with-the-data-annotation-validators-cs/_static/image14.png))

## <a name="summary"></a>Özet

Bu öğreticide, bir ASP.NET MVC uygulaması içinde doğrulama gerçekleştirmek için veri ek açıklaması modeli ciltinin avantajlarından nasıl yararlanabilmeniz öğrendiniz. Gerekli ve StringLength öznitelikleri gibi farklı türde Doğrulayıcı özniteliklerinin nasıl kullanılacağını öğrendiniz. Ayrıca, Microsoft Entity Framework çalışırken bu özniteliklerin nasıl kullanılacağını öğrenirsiniz.

> [!div class="step-by-step"]
> [Önceki](validating-with-a-service-layer-cs.md)
> [İleri](creating-model-classes-with-the-entity-framework-vb.md)
