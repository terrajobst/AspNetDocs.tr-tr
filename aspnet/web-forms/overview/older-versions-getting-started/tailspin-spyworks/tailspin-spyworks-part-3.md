---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: '3\. kısım: düzen ve kategori menüsü | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 3\. bölüm, düzen ve kategori menüsü eklemeyi içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639120"
---
# <a name="part-3-layout-and-category-menu"></a>3\. Bölüm: Düzen ve Kategori Menüsü

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 3\. bölüm, düzen ve kategori menüsü eklemeyi içerir.

## <a id="_Toc260221669"></a>Bazı düzen ve kategori menüsü ekleme

Site ana sayfamızda, sol taraftaki sütun için, ürün kategorisi menüsünü içerecek bir div ekleyeceğiz.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

İstenen hizalama ve diğer biçimlendirmeler Style. css dosyanıza eklediğimiz CSS sınıfı tarafından sağlanacaktır.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

Ürün kategorisi menüsü, mevcut ürün kategorileri için ticaret veritabanını sorgulayarak ve menü öğeleri ve karşılık gelen bağlantılar oluşturarak çalışma zamanında dinamik olarak oluşturulur.

Bunu gerçekleştirmek için, iki ASP. NET ' in güçlü veri denetimleri. "Varlık veri kaynağı" denetimi ve "ListView" denetimi.

![](tailspin-spyworks-part-3/_static/image1.jpg)

"Tasarım görünümüne" geçelim ve denetimlerinizi yapılandırmak için yardımcıları kullanabilirsiniz.

![](tailspin-spyworks-part-3/_static/image2.jpg)

EntityDataSource ID özelliğini EDS\_category\_Menu olarak ayarlayalim ve "veri kaynağını Yapılandır" seçeneğine tıklaalım.

![](tailspin-spyworks-part-3/_static/image3.jpg)

Ticaret veritabanımız için varlık veri kaynağı modelini oluşturduğumuzda ve "Ileri" ye tıkladığımızda bizim için oluşturulan CommerceEntities bağlantısını seçin.

![](tailspin-spyworks-part-3/_static/image4.jpg)

"Kategoriler" varlık kümesi adını seçin ve diğer seçenekleri varsayılan olarak bırakın. "Son" düğmesine tıklayın.

Şimdi sayfamıza yerleştirdiğimiz ListView denetim örneğinin ID özelliğini bir ListView\_ProductsMenu olarak ayarlayalım ve yardımcı ' i etkinleştirmektir.

![](tailspin-spyworks-part-3/_static/image5.jpg)

Veri öğesi görüntüleme ve biçimlendirmesini biçimlendirmek için denetim seçeneklerini kullanabiliriz; ancak, bu kodu kaynak görünümüne girebilmemiz için menü oluşturma yalnızca basit biçimlendirme gerektireceğiz.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

Lütfen "eval" ekstresini unutmayın: &lt;% # eval ("CategoryName")%&gt;

ASP.NET sözdizimi &lt;% #%&gt;, çalışma zamanının içinde yer aldığı her şeyi yürütmesini ve sonuçları "satır" olarak çıktısını veren bir toplu kuraldır.

İfade eval ("CategoryName"), veri öğelerinin bağlantılı koleksiyonundaki geçerli giriş için "CategoryName" varlık modeli öğe adlarının değerini getiren bildirir. Bu, çok güçlü bir özellik için kısa bir sözdizimidir.

Uygulamayı şimdi çalıştırmaya izin verir.

![](tailspin-spyworks-part-3/_static/image6.jpg)

Ürün kategorisi menümüzün görüntülendiğini ve kategori menü öğelerinden birinin üzerine geldiğinizde, menü öğesi bağlantı noktalarını yalnızca adlandırılmış ProductsList. aspx ' i uygulamamız ve bir dinamik sorgu dizesi bağımsız değişkeni (  kategori kimliği.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-2.md)
> [İleri](tailspin-spyworks-part-4.md)
