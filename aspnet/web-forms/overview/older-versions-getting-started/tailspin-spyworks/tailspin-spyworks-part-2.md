---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '2\. Bölüm: veri erişim katmanı | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. bölüm, veri erişim katmanını eklemeyi içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573250"
---
# <a name="part-2-data-access-layer"></a>2\. Bölüm: Veri Erişim Katmanı

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. bölüm, veri erişim katmanını eklemeyi içerir.

## <a id="_Toc260221668"></a>Veri erişim katmanını ekleme

Eticaret uygulamamız iki veritabanına bağlı olacaktır.

Müşteri bilgileri için standart ASP.NET üyelik veritabanını kullanacağız. Alışveriş sepetimiz ve Ürün kataloğumuz için aşağıdaki şekilde bir SQL Express veritabanı uygulayacağız.

![](tailspin-spyworks-part-2/_static/image1.jpg)

Uygulamanın uygulama\_veri klasöründe veritabanını (Commerce. mdf) oluşturdunuz, .NET Entity Framework kullanarak veri erişim katmanımızı oluşturmaya devam edebiliriz.

"Data\_Access" adlı bir klasör oluşturacağız ve bu klasöre sağ tıklayıp "yeni öğe Ekle" seçeneğini belirleyin.

"Yüklü şablonlar" öğesinde "ADO.NET Varlık Veri Modeli" öğesini seçin ve ad olarak EDM\_Commerce. edmx girin ve "Ekle" düğmesine tıklayın.

![](tailspin-spyworks-part-2/_static/image2.jpg)

"Veritabanından üret" seçeneğini belirleyin.

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

Kaydet ve oluştur.

Şimdi birinci özelliğimizi eklemeye hazırız: bir ürün kategorisi menüsü.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-1.md)
> [İleri](tailspin-spyworks-part-3.md)
