---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: '1\. kısım: Dosya-> Yeni proje | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve dosya/yeni proje içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636131"
---
# <a name="part-1-file--new-project"></a>1\. Bölüm: Dosya -> Yeni Proje

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 1\. bölüm, genel bakış ve dosya/yeni proje içerir.

## <a id="_Toc260221666"></a>Bakýþ

Bu öğretici, ASP.NET WebForms 'e giriş niteliğindedir. Yavaş başlayacağız, bu nedenle başlangıç düzeyi Web geliştirme deneyimi sorunsuz.

Oluşturmakta olduğumuz uygulama basit bir çevrimiçi depodır.

![](tailspin-spyworks-part-1/_static/image1.jpg)

Ziyaretçiler ürüne kategoriye göre gözatabilirler:

![](tailspin-spyworks-part-1/_static/image2.jpg)

Tek bir ürünü görüntüleyebilir ve bu uygulamayı sepetlerinden ekleyebilirler:

![](tailspin-spyworks-part-1/_static/image3.jpg)

Sepetlerinde, artık istedikleri öğeleri kaldırarak kendi sepetini gözden geçirebilir:

![](tailspin-spyworks-part-1/_static/image4.jpg)

Kullanıma almaya devam etmek, bunları şunları isteyecek

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

Sipariş ettikten sonra basit bir onay ekranı görürler:

![](tailspin-spyworks-part-1/_static/image7.jpg)

Visual Studio 2010 ' de yeni bir ASP.NET WebForms projesi oluşturarak başlayacağız ve tamamen çalışan bir uygulama oluşturmak için artımlı olarak Özellikler ekleyeceğiz. Bu şekilde, veritabanı erişimi, liste ve kılavuz görünümlerini, veri güncelleştirme sayfalarını, veri doğrulamayı, tutarlı sayfa düzeni, AJAX, doğrulama, Kullanıcı üyeliği ve daha fazlasını kapsayan ana sayfaları kullanarak ele alacağız.

Adımları adım adım takip edebilir veya tamamlanmış uygulamayı [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/) adresinden indirebilirsiniz

[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)'Den visual Studio 2010 veya ücretsiz Visual Web Developer 2010 ' i kullanabilirsiniz. Uygulamayı derlemek için, veritabanını barındırmak üzere SQL Server veya ücretsiz SQL Server Express kullanabilirsiniz.

## <a id="_Toc260221667"></a>Dosya/yeni proje

Visual Studio 'da Dosya menüsünden yeni projeyi seçerek başlayacağız. Bu, yeni proje iletişim kutusunu getirir.

![](tailspin-spyworks-part-1/_static/image8.jpg)

Sol taraftaki görsel C# /Web şablonları grubunu seçeceğiz ve ardından Orta sütundaki "ASP.NET Web uygulaması" şablonunu seçersiniz. Projenizi TailspinSpyworks olarak adlandırın ve Tamam düğmesine basın.

![](tailspin-spyworks-part-1/_static/image9.jpg)

Bu, projemizi oluşturacaktır. Aşağıda, uygulamamızda bulunan klasörlere sağ taraftaki Çözüm Gezgini göz atalım.

![](tailspin-spyworks-part-1/_static/image10.jpg)

Boş çözüm tamamen boş değildir; temel bir klasör yapısı ekler:

![](tailspin-spyworks-part-1/_static/image1.png)

ASP.NET 4 varsayılan proje şablonu tarafından uygulanan kurallara göz önünde edin.

- "Account" klasörü ASP için temel bir kullanıcı arabirimi uygular. NET 'in üyelik alt sistemi.
- "Betikler" klasörü, istemci tarafı JavaScript dosyaları için depo görevi görür ve çekirdek jQuery. js dosyaları varsayılan olarak kullanılabilir hale getirilir.
- "Stiller" klasörü, Web sitesi görsellerimizi (CSS stil sayfaları) düzenlemek için kullanılır

Uygulamamızı çalıştırmak ve default. aspx sayfasını işlemek için F5 'e bastığımda, aşağıdakileri görtik.

![](tailspin-spyworks-part-1/_static/image11.jpg)

İlk uygulama geliştirmemiz, default WebForms şablonundaki Style. css dosyasını, Tailspin Spyworks uygulamamız için istediğimiz görsel güvenlerle birlikte işleyecek olan CSS sınıflarıyla ve ilişkili resim dosyalarıyla değiştirecek.

Bunu yaptıktan sonra default. aspx sayfamız bu şekilde işlenir.

![](tailspin-spyworks-part-1/_static/image12.jpg)

Sayfanın sağ üst kısmındaki görüntü bağlantılarına ve ana sayfaya eklenen menü öğelerine dikkat edin. Yalnızca "oturum aç" ve "hesap" bağlantıları, var olan sayfalara (varsayılan şablon tarafından oluşturulan) ve uygulamamız oluşturduğumuzdan uyguladığımız sayfaların geri kalanına işaret eder.

Ana sayfayı stiller dizinine de konumlandırıyoruz. Bu yalnızca bir tercih olsa da, uygulamamızı gelecekte "Skinable" olarak yapmaya karar verirse, bu işlemleri biraz daha kolay hale getirir.

Bunu yaptıktan sonra, varsayılan ASP.NET WebForms sayfaları tarafından oluşturulan tüm. aspx dosyalarındaki ana sayfa başvurularını değiştirmemiz gerekir.

> [!div class="step-by-step"]
> [Next](tailspin-spyworks-part-2.md)
