---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 8 ' i kullanmaya başlama Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585913"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 8 ' i kullanmaya başlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>Verileri biçimlendirmek ve doğrulamak için dinamik veri Işlevselliğini kullanma

Önceki öğreticide saklı yordamları uyguladık. Bu öğreticide, dinamik veri işlevlerinin aşağıdaki avantajları nasıl sağlayabilmesinin nasıl yapılacağı gösterilmektedir:

- Alanlar, veri türlerine göre görüntülenmek üzere otomatik olarak biçimlendirilir.
- Alanlar, veri türlerine göre otomatik olarak onaylanır.
- Biçimlendirme ve doğrulama davranışını özelleştirmek için veri modeline meta veri ekleyebilirsiniz. Bunu yaptığınızda, biçimlendirme ve doğrulama kurallarını tek bir yerde ekleyebilirsiniz ve dinamik veri denetimleri kullanarak alanlara her yerden eriştiğinizde otomatik olarak uygulanır.

Bunun nasıl çalıştığını görmek için, var olan *öğrenciler. aspx* sayfasındaki alanları görüntülemek ve düzenlemek için kullandığınız denetimleri değiştireceksiniz ve `Student` varlık türünün ad ve Tarih alanlarına biçimlendirme ve doğrulama meta verileri ekleyeceksiniz.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>DynamicField ve DynamicControl denetimleri kullanma

*Öğrenciler. aspx* sayfasını açın ve `StudentsGridView` denetiminde **ad** ve **kayıt tarihi** `TemplateField` öğelerini aşağıdaki biçimlendirme ile değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

Bu biçimlendirme, öğrenci adı şablonu alanında `TextBox` ve `Label` denetimlerinin yerine `DynamicControl` denetimleri kullanır ve kayıt tarihi için bir `DynamicField` denetimi kullanır. Biçim dizesi belirtilmedi.

`StudentsGridView` denetiminden sonra `ValidationSummary` denetimi ekleyin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

`SearchGridView` denetiminde, **ad** ve **kayıt tarihi** sütunlarının işaretlemesini, `StudentsGridView` denetiminde yaptığınız gibi değiştirin, ancak `EditItemTemplate` öğesini atlayın. `SearchGridView` denetiminin `Columns` öğesi artık aşağıdaki biçimlendirmeyi içerir:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

*Students.aspx.cs* açın ve aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

Sayfanın `Init` olayı için bir işleyici ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

Bu kod, dinamik verilerin, `Student` varlığının alanları için bu veri bağlantılı denetimlerde biçimlendirme ve doğrulama sağlayacağı belirtir. Sayfayı çalıştırdığınızda aşağıdaki örnekte olduğu gibi bir hata iletisi alırsanız, genellikle `Page_Init``EnableDynamicData` yöntemi çağırmayı unutmuş demektir:

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

Sayfayı çalıştırın.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

**Kayıt tarihi** sütununda, zaman tarih ile birlikte görüntülenir, çünkü özellik türü `DateTime`. Daha sonra bunu düzeltireceksiniz.

Şimdilik, dinamik verilerin otomatik olarak temel veri doğrulaması sağladığını fark edersiniz. Örneğin, **Düzenle**' ye tıklayın, tarih alanını temizleyin, **Güncelleştir**' e tıklayın ve değer veri modelinde null atanabilir olmadığından dinamik verilerin bu gerekli alanı otomatik olarak yaptığından emin olmalısınız. Sayfada, `ValidationSummary` denetimindeki bir alan ve hata iletisinden sonra bir yıldız görüntülenir:

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

Hata iletisini görmek için fare işaretçisini yıldız işareti üzerinde tutabilmeniz için `ValidationSummary` denetimini atlayabilirsiniz.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

Dinamik veriler de **kayıt tarihi** alanına girilen verilerin geçerli bir tarih olduğunu doğrular:

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

Gördüğünüz gibi, bu genel bir hata iletisidir. Sonraki bölümde, iletileri özelleştirmeyi ve doğrulama ve biçimlendirme kurallarını nasıl özelleştireceğinizi göreceksiniz.

## <a name="adding-metadata-to-the-data-model"></a>Veri modeline meta veriler ekleme

Genellikle, dinamik veriler tarafından sunulan işlevselliği özelleştirmek istersiniz. Örneğin, verilerin görüntülendiğini ve hata iletilerinin içeriğini değiştirebilirsiniz. Ayrıca, veri türlerine bağlı olarak dinamik verilerin otomatik olarak sağladığı daha fazla işlevsellik sağlamak için veri doğrulama kurallarını da özelleştirebilirsiniz. Bunu yapmak için varlık türlerine karşılık gelen kısmi sınıflar oluşturursunuz.

**Çözüm Gezgini**, **contosouniversity** projesine sağ tıklayın, **başvuru ekle**' yi seçin ve `System.ComponentModel.DataAnnotations`bir başvuru ekleyin.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

*Dal* klasöründe, yeni bir sınıf dosyası oluşturun, *Student.cs*olarak adlandırın ve içindeki şablon kodunu aşağıdaki kodla değiştirin.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

Bu kod `Student` varlığı için kısmi bir sınıf oluşturur. Bu parçalı sınıfa uygulanan `MetadataType` özniteliği, meta verileri belirtmek için kullandığınız sınıfı tanımlar. Meta veri sınıfı herhangi bir ada sahip olabilir, ancak varlık adı artı "metadata" kullanılması yaygın bir uygulamadır.

Meta veri sınıfındaki özelliklere uygulanan öznitelikler biçimlendirme, doğrulama, kurallar ve hata iletileri belirler. Burada gösterilen öznitelikler aşağıdaki sonuçlara sahip olacaktır:

- `EnrollmentDate` bir tarih (bir süre olmadan) olarak gösterilir.
- Her iki ad alanı da 25 karakter uzunluğunda veya daha az olmalı ve özel bir hata iletisi sağlanmalıdır.
- Her iki ad alanı da gereklidir ve özel bir hata iletisi sağlanır.

*Öğrenciler. aspx* sayfasını yeniden çalıştırın ve tarihlerin şu zamanlarda görüntülendiğini görürsünüz:

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

Bir satırı düzenleyin ve ad alanlarındaki değerleri temizlemeye çalışın. Alan hatalarını gösteren yıldız işaretleri, bir alanı bıraktığınızda, **Güncelleştir**' e tıklamadan önce görüntülenir. **Güncelleştir**' e tıkladığınızda, sayfada belirttiğiniz hata iletisi metni görüntülenir.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

25 karakterden daha uzun adlar girmeyi deneyin, **Güncelleştir**' e tıklayın ve belirttiğiniz hata iletisi metnini görüntüler.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

Veri modeli meta verilerinde bu biçimlendirme ve doğrulama kurallarını ayarladığınıza göre, kurallar, `DynamicControl` veya `DynamicField` denetimleri kullandığınız sürece bu alanlarda değişiklik gösteren veya bu alanlarda değişiklik sağlayan her sayfada otomatik olarak uygulanır. Bu, programlama ve sınamayı daha kolay hale getiren ve veri biçimlendirme ve doğrulamanın bir uygulama genelinde tutarlı olmasını sağlayan, yazmanız gereken gereksiz kod miktarını azaltır.

## <a name="more-information"></a>Daha Fazla Bilgi

Bu, Entity Framework ile çalışmaya başlama konusunda bu öğreticiyle sonuçlanır. Entity Framework nasıl kullanacağınızı öğrenmenize yardımcı olacak daha fazla kaynak için, [sonraki Entity Framework öğretici serisinde ilk öğreticiye](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) devam edin veya aşağıdaki siteleri ziyaret edin:

- [Entity Framework SSS](http://www.ef-faq.org/introduction.html)
- [Entity Framework ekip blogu](https://blogs.msdn.com/b/adonet/)
- [MSDN Kitaplığı 'nda Entity Framework](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN veri Geliştirici Merkezi 'nde Entity Framework](https://msdn.microsoft.com/data/ef.aspx)
- [EntityDataSource Web sunucusu denetimine genel bakış MSDN Kitaplığı](https://msdn.microsoft.com/library/cc488502.aspx)
- [MSDN Kitaplığı 'nda EntityDataSource Denetim API başvurusu](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN 'de Entity Framework forumları](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman 'ın blogu](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [Öncekini](the-entity-framework-and-aspnet-getting-started-part-7.md)
