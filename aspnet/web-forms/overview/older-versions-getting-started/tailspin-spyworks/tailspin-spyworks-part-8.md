---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8\. kısım: son sayfalar, özel durum Işleme ve sonuç | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, sayfa ve özel durum hakkında bir kişi sayfası ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586886"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>8\. Bölüm: Son Sayfalar, Özel Durum İşleme ve Sonuç

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, sayfa ve özel durum işleme hakkında bir kişi sayfası ekler. Bu, serinin bir sonucu olur.

## <a id="_Toc260221680"></a>İletişim sayfası (ASP.NET 'den e-posta gönderme)

Yeni bir sayfa oluşturun.

Tasarımcıyı kullanarak, ToolkitScriptManager ve düzenleyici denetimini AjaxControlToolkit öğesinden dahil etmek için aşağıdaki formu oluşturun. arasında yetersiz alanla karşılaştı.

![](tailspin-spyworks-part-8/_static/image1.jpg)

"Gönder" düğmesine çift tıklayarak, arka plan kodu dosyasında bir tıklama olayı işleyicisi oluşturun ve iletişim bilgilerini bir e-posta olarak göndermek için bir yöntem uygulayın.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

Bu kod, Web. config dosyanızın, posta göndermek için kullanılacak SMTP sunucusunu belirten yapılandırma bölümünde bir giriş içermesini gerektirir.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>Sayfa hakkında

AboutUs. aspx adlı bir sayfa oluşturun ve dilediğiniz içeriği ekleyin.

## <a id="_Toc260221682"></a>Genel özel durum Işleyicisi

Son olarak, uygulama genelinde özel durumlar oluşturduğumuzdan, ayrıca web uygulamamız içinde işlenmemiş özel durumlara neden olan öngörülemeyen durumlar vardır.

İşlenmeyen bir özel durumun bir Web sitesi ziyaretçisine görüntülenmesini hiç istemedik.

![](tailspin-spyworks-part-8/_static/image2.jpg)

Farklı bir kullanıcı deneyimi dışında, işlenmemiş özel durumlar da güvenlik sorunu oluşturabilir.

Bu sorunu çözmek için genel bir özel durum işleyicisi uygulayacağız.

Bunu yapmak için Global. asax dosyasını açın ve aşağıdaki önceden oluşturulmuş olay işleyicisine göz önünde edin.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

Uygulama\_hata işleyicisini aşağıdaki şekilde uygulamak için kod ekleyin.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

Sonra çözüme Error. aspx adlı bir sayfa ekleyin ve bu biçimlendirme kod parçacığını ekleyin.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

Şimdi sayfada olay işleyicisini yükle\_, Istek nesnesinden hata iletilerini ayıklayın.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>İşleminin

ASP.NET WebForms 'in veritabanı erişimi, üyeliği, AJAX vb. ile gelişmiş bir Web sitesi oluşturmayı daha kolay bir şekilde gördük. oldukça hızlı.

Bu öğreticide, kendi ASP.NET WebForms uygulamalarınızı oluşturmaya başlamak için ihtiyacınız olan araçları vermiş olursunuz!

> [!div class="step-by-step"]
> [Öncekini](tailspin-spyworks-part-7.md)
