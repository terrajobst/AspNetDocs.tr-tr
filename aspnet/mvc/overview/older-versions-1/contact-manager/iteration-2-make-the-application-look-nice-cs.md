---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: 'Yineleme #2 – uygulamanın güzel görünmesini sağlama (C#) | Microsoft Docs'
author: microsoft
description: Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 246cb4b4668339cc4b7e4e03ea005102c6a2a5c3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602020"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>Yineleme #2: uygulamanın iyi görünmesini sağlama (C#)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Kişi yönetimi ASP.NET MVC uygulaması (C#) oluşturma

Bu öğretici dizisinde, başlangıçtan sonuna kadar bir Iletişim yönetimi uygulaması oluşturacaksınız. Ilgili kişi Yöneticisi uygulaması, kişi listesi için kişi bilgilerini, telefon numaralarını ve e-posta adreslerini depolamanıza olanak sağlar.

Uygulamayı birden çok yineleme üzerinde oluşturacağız. Her yinelemede, uygulamayı kademeli olarak geliştirdik. Bu birden çok yineleme yaklaşımının hedefi, her bir değişikliğin nedenini anlamanıza olanak sağlamaktır.

- Yineleme #1-uygulamayı oluşturun. İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

- Yineleme #2-uygulamanın iyi görünmesini sağlayın. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

- Yineleme #3-form doğrulaması ekleme. Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

- Yineleme #4-uygulamayı gevşek olarak bağlanmış hale getirin. Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

- Yineleme #5-birim testleri oluşturun. Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

- Yineleme #6-test odaklı geliştirme kullanın. Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

- Yineleme #7-Ajax işlevselliği ekleme. Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="this-iteration"></a>Bu yineleme

Bu yinelemenin hedefi, Contact Manager uygulamasının görünüşünü geliştirmektir. Şu anda, kişi Yöneticisi varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını kullanır (bkz. Şekil 1). Bu, hatalı görünmeme, ancak Contact Manager 'ın diğer tüm ASP.NET MVC web sitesi gibi görünmesini istemiyorum. Bu dosyaları özel dosyalarla değiştirmek istiyorum.

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**Şekil 01**: BIR ASP.NET MVC uygulamasının varsayılan görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image2.png))

Bu yinelemede, uygulamamızın görsel tasarımını iyileştirmek için iki yaklaşım anladım. İlk olarak, ücretsiz bir ASP.NET MVC tasarım şablonunu indirmek için ASP.NET MVC tasarım galerisinden nasıl yararlanabilirim? ASP.NET MVC Tasarım Galerisi, herhangi bir iş yapmadan profesyonel bir Web uygulaması oluşturmanıza olanak sağlar.

Contact Manager uygulaması için ASP.NET MVC tasarım galerisinden bir şablon kullanmamaya karar verdim. Bunun yerine, profesyonel tasarım firması tarafından oluşturulan özel bir tasarımım vardı. Bu öğreticinin ikinci bölümünde, son ASP.NET MVC tasarımını oluşturmak için profesyonel bir tasarım şirketiyle nasıl çalıştık açıkladım.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC Tasarım Galerisi

ASP.NET MVC Tasarım Galerisi, Microsoft tarafından sunulan ücretsiz bir kaynaktır. ASP.NET MVC Galerisi şu adreste bulunur:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC Tasarım Galerisi, bir ASP.NET MVC projesinde kullanımı için özel olarak oluşturulan ücretsiz web sitesi tasarımlarının bir koleksiyonunu barındırır. Tasarımlar, topluluk üyeleri tarafından karşıya yüklenir. Galerinin ziyaretçileri, en sevdiğiniz tasarımlar için oy verebilir (bkz. Şekil 2).

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**Şekil 02**: ASP.NET MVC Tasarım Galerisi ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image4.png))

Bu öğreticiyi yazdığımda, galerideki en popüler tasarım Ekim, David Hauser adlı bir tasarımdır. Aşağıdaki adımları tamamlayarak, bu tasarımı bir ASP.NET MVC projesi için kullanabilirsiniz:

1. Ekim. zip dosyasını bilgisayarınıza indirmek için **İndir** düğmesine tıklayın.
2. İndirilen Ekim. zip dosyasına sağ tıklayın ve **Engellemeyi kaldır** düğmesine tıklayın (bkz. Şekil 3).
3. Dosyayı Ekim adlı bir klasöre ayıklayın.
4. Ekim klasöründe bulunan DesignTemplate klasöründen tüm dosyaları seçin, dosyalara sağ tıklayın ve sonra **Kopyala**' yı seçin.
5. Visual Studio Çözüm Gezgini penceresinde ContactManager proje düğümüne sağ tıklayın ve menü seçeneğini **Yapıştır** ' ı seçin (bkz. Şekil 4).
6. Visual Studio menü seçeneğini belirleyin **, bulun ve değiştirin, Hızlı Değiştir** ve < *MyProjectName]* öğesini *ContactManager* ile değiştirin (bkz. Şekil 5).

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**Şekil 03**: Web 'den indirilen bir dosyanın engellemesini kaldırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image6.png))

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**Şekil 04**: Çözüm Gezgini dosyaların üzerine yazma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image8.png))

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**Şekil 05**: [ProjectName] öğesini ContactManager ile değiştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image10.png))

Bu adımları tamamladıktan sonra, Web uygulamanız yeni tasarımı kullanacaktır. Şekil 6 ' daki sayfa, Ekim tasarımıyla birlikte Contact Manager uygulamasının görünümünü gösterir.

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**Şekil 06**: Ekim şablonuna sahip ContactManager ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>Özel bir ASP.NET MVC tasarımı oluşturma

ASP.NET MVC Tasarım Galerisi, farklı tasarım stilleri için iyi bir seçimdir. Galeri, ASP.NET MVC uygulamalarınızın görünümünü özelleştirmek için biraz daha az bir yol sağlar. Tabii ki, Galeri büyük ölçüde tamamen ücretsiz olarak avantajlıdır.

Ancak, Web siteniz için tamamen benzersiz bir tasarım oluşturmanız gerekebilir. Bu durumda, bir Web sitesi tasarımı şirketiyle çalışmak mantıklı olur. Bu yaklaşımı, Contact Manager uygulamasının tasarımı için yapmaya karar verdim.

Contact Manager 'ı yineleme #1 sıkıştırdım ve projeyi tasarım şirketine gönderdiniz. Bunlar Visual Studio 'Yu (bunlar üzerinde biçimlendirdim!) değil, bir sorun sunmadı. Microsoft Visual Web Developer 'ı [https://www.asp.net](https://www.asp.net) Web sitesinden ücretsiz olarak indirebildikleri ve Visual Web Developer 'Da Contact Manager uygulamasını açamıyor. Birkaç gün içinde, Şekil 7 ' de tasarımı üretti.

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**Şekil 07**: ASP.NET MVC Contact Manager tasarımı ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image14.png))

Yeni tasarım iki ana dosyadan oluşur: yeni bir geçişli stil sayfası dosyası ve yeni bir görünüm ana sayfa dosyası. Bir görünüm ana sayfası, bir ASP.NET MVC uygulamasındaki görünümlere yönelik düzen ve paylaşılan içeriği içerir. Örneğin, görünüm ana sayfası, Şekil 7 ' de görünen üstbilgiyi, gezinti sekmelerini ve altbilgiyi içerir. Tasarım şirketindeki yeni site. master dosyası ile Views\Shared klasöründe var olan site. Master görünüm ana sayfasını aşırı yazdım,

Tasarım şirketi yeni bir geçişli stil sayfası ve görüntü kümesi de oluşturmuştur. Bu yeni dosyaları Içerik klasörüne yerleştirdim ve var olan site. css dosyasının üzerine yazdı. Tüm statik içeriği Içerik klasörüne yerleştirmeniz gerekir.

Kişi Yöneticisi için yeni tasarımın, kişileri düzenlemenin ve silmenin görüntülerini içerdiğine dikkat edin. HTML kişileri tablosundaki her kişinin yanında bulunan bir düzenleme ve silme resmi görüntülenir.

Başlangıçta, bu bağlantılar HTML ile işlenir. Aşağıdaki gibi ActionLink () Yardımcısı:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

HTML. ActionLink () yöntemi görüntüleri desteklemez (HTML yöntemi, bağlantı metnini güvenlik nedenleriyle kodluyor). Bu nedenle, HTML. ActionLink () çağrılarını URL. Action () çağrılarına şunun gibi değiştirdim:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

HTML. ActionLink () yöntemi bir HTML köprünün tamamını işler. Diğer taraftan, URL. Action () yöntemi, &lt;bir&gt; etiketi olmadan yalnızca URL 'YI oluşturur.

Ayrıca, yeni tasarımın hem seçili hem de seçilmemiş sekmeleri içerdiğine dikkat edin. Örneğin, Şekil 8 ' de **Yeni kişi oluştur** sekmesi seçilidir ve **Kişilerim** sekmesi seçili değildir.

[Yeni proje iletişim kutusunu ![](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**Şekil 08**: seçili ve seçilmemiş sekmeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-2-make-the-application-look-nice-cs/_static/image16.png))

Hem seçili hem de seçili olmayan sekmelerin işlenmesini desteklemek için Menuıtemhelper adlı özel bir HTML Yardımcısı oluşturdum. Bu yardımcı yöntem, geçerli denetleyicinin ve eylemin, yardım 'a geçirilen denetleyiciye ve eylem adına karşılık gelen &lt;li&gt; etiketi veya &lt;li Class = "Selected"&gt; etiketini işler. Menuıtemhelper kodu, liste 1 ' de bulunur.

**Listeleme 1-Helpers\menuıtemhelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

Menuıtemhelper, &lt;li&gt; HTML etiketi oluşturmak için dahili olarak TagBuilder sınıfını kullanır. TagBuilder sınıfı, yeni bir HTML etiketi oluşturmanız gerektiğinde kullanabileceğiniz çok faydalı bir yardımcı sınıftır. Öznitelik ekleme, CSS sınıfları ekleme, kimlik oluşturma ve iç HTML etiketlerini değiştirme yöntemlerini içerir.

## <a name="summary"></a>Özet

Bu yinelemede, ASP.NET MVC uygulamamız görsel tasarımını geliştirdik. İlk olarak, ASP.NET MVC tasarım galerisine sunulmuştur. ASP.NET MVC uygulamalarınızda kullanabileceğiniz ASP.NET MVC tasarım galerisinden ücretsiz tasarım şablonlarının nasıl indirileceğini öğrendiniz.

Daha sonra, varsayılan geçişli stil sayfası dosyası ve ana görünüm sayfası dosyasını değiştirerek nasıl özel bir tasarım oluşturabileceğiniz ele alınmıştır. Yeni tasarımı desteklemek için, Contact Manager uygulamamız üzerinde bazı küçük değişiklikler yapmak zorunda kaldık. Örneğin, seçili ve seçilmemiş sekmeleri görüntüleyen Menuıtemhelper adlı yeni bir HTML Yardımcısı ekledik.

Bir sonraki yinelemede, doğrulamanın çok önemli konusunu geliştirdik. Bir kullanıcının, bir kişi adı ve soyadı gibi gerekli değerleri sağlamadan yeni bir kişi oluşturabilmesi için, uygulamamıza doğrulama kodu ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](iteration-1-create-the-application-cs.md)
> [İleri](iteration-3-add-form-validation-cs.md)
