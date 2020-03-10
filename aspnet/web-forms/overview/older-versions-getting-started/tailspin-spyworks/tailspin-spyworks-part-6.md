---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 'Bölüm 6: ASP.NET üyeliği | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 6, ASP.NET üyeliği ekler.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564185"
---
# <a name="part-6-aspnet-membership"></a>6\. Bölüm: ASP.NET Üyeliği

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 6, ASP.NET üyeliği ekler.

## <a id="_Toc260221672"></a>ASP.NET üyeliğiyle çalışma

![](tailspin-spyworks-part-6/_static/image1.png)

Güvenlik 'e tıklayın

![](tailspin-spyworks-part-6/_static/image1.jpg)

Forms kimlik doğrulaması kullandığınızdan emin olun.

![](tailspin-spyworks-part-6/_static/image2.jpg)

Birkaç kullanıcı oluşturmak için "Kullanıcı Oluştur" bağlantısını kullanın.

![](tailspin-spyworks-part-6/_static/image3.jpg)

İşiniz bittiğinde Çözüm Gezgini penceresine bakın ve görünümü yenileyin.

![](tailspin-spyworks-part-6/_static/image2.png)

ASPNETDB 'nin olduğunu unutmayın. MDF ince oluşturulmuş. Bu dosya, üyelik gibi çekirdek ASP.NET hizmetlerini destekleyecek tabloları içerir.

Artık kullanıma alma işlemini uygulamaya başlayabiliriz.

Bir kullanıma alma. aspx sayfası oluşturarak başlayın.

CheckOut. aspx sayfası yalnızca oturum açmış kullanıcılar tarafından kullanılabilir olmalıdır, bu sayede oturum açan kullanıcılara erişimi kısıtlayacağız ve oturum açan kullanıcıları oturum açma sayfasında yeniden yönlendiririz.

Bunu yapmak için, Web. config dosyasının yapılandırma bölümüne aşağıdakileri ekleyeceğiz.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web Forms uygulamalar şablonu, Web. config dosyasına otomatik olarak bir kimlik doğrulama bölümü ekledi ve varsayılan oturum açma sayfasını kurdu.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

Kullanıcı oturum açtığında anonim bir alışveriş sepetini geçirmek için login. aspx kodu dosyasının arkasında değişiklik yapılmalıdır. Sayfa\_yükleme olayını aşağıda gösterildiği gibi değiştirin.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

Ardından, oturum adını yeni oturum açmış olan kullanıcıya ayarlamak için bu şekilde bir "LoggedIn" olay işleyicisi ekleyin ve MyShoppingCart sınıfımızda MigrateCart yöntemini çağırarak alışveriş sepetindeki geçici oturum kimliğini kullanıcıya değiştirin. (. Cs dosyasında uygulandı)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

Bunun gibi MigrateCart () yöntemini uygulayın.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

Kullanıma alma. aspx ' te, alışveriş sepeti sayfamızda yaptığımız kadar çok sayıda kullanıma alma sayfamızda bir EntityDataSource ve GridView kullanacağız.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

GridView Denetimimizin, MyList\_Rowveriye bağlı bir "onumuza" olay işleyicisini belirttiğinden emin olmak için bu olay işleyicisini bu şekilde uygulayalim.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

Bu yöntem, her satır bağlandığı ve GridView 'un alt satırını güncelleştiren bir alışveriş sepetinin çalışma toplamı tutar.

Bu aşamada, yerleştirilecek siparişin bir "Gözden geçirme" sunumunu uyguladık.

Sayfa\_Load olayına birkaç satır kod ekleyerek boş bir sepet senaryosunu işleyelim:

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

Kullanıcı "Gönder" düğmesine tıkladığında, Gönder düğmesine tıklama olay işleyicisi ' nde aşağıdaki kodu yürütecektir.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

Order gönderim işleminin "et" i MyShoppingCart sınıfımız SubmitOrder () yönteminde uygulanmalıdır.

SubmitOrder:

- Alışveriş sepetindeki tüm satır öğelerini alıp yeni bir sipariş kaydı ve ilişkili OrderDetails kayıtları oluşturmak için bunları kullanın.
- Sevkiyat tarihini hesaplayın.
- Alışveriş sepetini temizleyin.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

Bu örnek uygulamanın amaçları doğrultusunda, geçerli tarihe yalnızca iki gün ekleyerek bir sevk tarihi hesaplayacağız.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

Şimdi uygulamayı çalıştırmak, alışveriş sürecini baştan sona test etmemize olanak sağlayacak.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-5.md)
> [İleri](tailspin-spyworks-part-7.md)
