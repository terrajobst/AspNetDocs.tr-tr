---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: '10. kısım: gezinti ve site tasarımına yönelik son güncelleştirmeler, sonuç | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 10, gezinti ve S için son güncelleştirmeleri içerir...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539370"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>10. Bölüm: Gezinti ve Site Tasarımına Yönelik Son Güncelleştirmeler, Sonuç

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 10 ' da gezinti ve site tasarımı için son güncelleştirmeler ve sonuç olarak yer alır.

Sitemizin tüm önemli işlevlerini tamamladık, ancak hala site gezintisine, giriş sayfasına ve mağaza tarama sayfasına eklemek için bazı özellikler sunuyoruz.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>Alışveriş sepeti Özeti kısmi görünümü oluşturuluyor

Kullanıcının alışveriş sepetindeki öğe sayısını tüm site genelinde göstermek istiyoruz.

![](mvc-music-store-part-10/_static/image1.png)

Bunu, sitemiz. Master ' a eklenen kısmi bir görünüm oluşturarak kolayca uygulayabiliriz.

Daha önce gösterildiği gibi, ShoppingCart denetleyicisi kısmi bir görünüm döndüren bir CartSummary eylem yöntemi içerir:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

CartSummary kısmi görünümü oluşturmak için, görünümler/ShoppingCart klasörüne sağ tıklayın ve Görünüm Ekle ' yi seçin. Görünümü CartSummary olarak adlandırın ve aşağıda gösterildiği gibi "kısmi görünüm oluştur" onay kutusunu işaretleyin.

![](mvc-music-store-part-10/_static/image2.png)

CartSummary kısmi görünümü gerçekten basittir. Bu yalnızca, sepetteki öğelerin sayısını gösteren ShoppingCart dizin görünümüne yönelik bir bağlantıdır. CartSummary. cshtml için kodun tamamı aşağıdaki gibidir:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

Site Yöneticisi de dahil olmak üzere sitedeki herhangi bir sayfaya, HTML. RenderAction yöntemini kullanarak kısmi bir görünüm dahil edebilirsiniz. RenderAction, aşağıdaki gibi eylem adını ("CartSummary") ve denetleyici adını ("ShoppingCart") belirtmemizi gerektirir.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

Bunu site düzenine eklemeden önce, tüm site. Master güncelleştirmelerini tek seferde yapabilmemiz için de tarz menüsünü oluşturacağız.

## <a name="creating-the-genre-menu-partial-view"></a>Tarzı menü kısmi görünümü oluşturma

Mağazalarımızda bulunan tüm tarzları listeleyen bir tarz menü ekleyerek kullanıcılarımızın mağazada gezinilmesi çok daha kolay olabilir.

![](mvc-music-store-part-10/_static/image3.png)

Aynı adımları izleyerek bir GenreMenu kısmi görünümü oluşturur ve bunları hem site yöneticisine ekleyebiliriz. Önce, StoreController öğesine aşağıdaki GenreMenu denetleyici eylemini ekleyin:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

Bu eylem, daha sonra oluşturduğumuz kısmi görünüm tarafından görüntülenecek olan tarzın bir listesini döndürür.

*Note: Bu denetleyiciye yalnızca bu eylemin yalnızca bir kısmi görünümden kullanılmasını istediğinizi belirten bu denetleyici eylemine [Childadctiononly] özniteliğini ekledik. Bu öznitelik,/Store/genremenu'e göz atarak denetleyici eyleminin yürütülmesini engeller. Bu, kısmi görünümler için gerekli değildir, ancak denetleyici eylemlerimizin amaçladığınız şekilde kullanıldığından emin olmak istediğimiz için iyi bir uygulamadır. Ayrıca, görüntüleme altyapısının diğer görünümlere eklendiğinden Bu görünüm için Düzen kullanması gerektiğini bilmesini sağlayan, görüntüleme yerine PartialView döndürüyoruz.*

GenreMenu denetleyicisi eylemine sağ tıklayın ve aşağıda gösterildiği gibi tarzı görünüm verisi sınıfı kullanılarak kesin bir şekilde belirlenmiş olan GenreMenu adlı kısmi bir görünüm oluşturun.

![](mvc-music-store-part-10/_static/image4.png)

Aşağıdaki gibi sıralanmamış bir liste kullanarak öğeleri görüntülemek için GenreMenu kısmi görünümünün görünüm kodunu güncelleştirin.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>Kısmi Görünümlerimizi göstermek için site düzeni güncelleştiriliyor

HTML. RenderAction () yöntemini çağırarak kısmi Görünümlerimizi site düzenine (/Views/Shared/\_Layout. cshtml) ekleyebiliriz. Bunları, aşağıda gösterildiği gibi, bunlara ek olarak bunları göstermek için de ekleyeceğiz:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

Artık uygulamayı çalıştırdığımızda, sol gezinti alanında tarzı ve en üstteki sepet özetini görüyoruz.

## <a name="update-to-the-store-browse-page"></a>Mağaza tarayıcı sayfasına Güncelleştir

Mağaza göz at sayfası işlevseldir, ancak çok iyi görünmüyor. Görünüm kodunu güncelleştirerek (/Views/Store/Browse.cshtml içinde bulunur), daha iyi bir düzende Albümler göstermek için sayfayı güncelleştirebiliriz:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

Burada, albüm resmini eklemek için bağlantıya özel biçimlendirme uygulayabilmemiz için HTML. ActionLink yerine URL. Action ' i kullanırız.

*Note: Bu Albümler için genel bir albüm kapağı görüntüliyoruz. Bu bilgiler veritabanında depolanır ve mağaza Yöneticisi aracılığıyla düzenlenebilir. Kendi resminizi eklemek için hoş geldiniz.*

Şimdi bir Tarzya gözatarken, albüm resmindeki bir kılavuzda gösterilen albümleri görüyoruz.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>Ana sayfayı, En Iyi satış albümlerini gösterecek şekilde güncelleştirme

Satışları artırmak için ana sayfada en iyi satış albümlerimizi kullanmak istiyoruz. Bu bilgileri işlemek için HomeController 'da bazı güncelleştirmeler oluşturacağız ve bazı ek grafikler de ekleyeceğiz.

İlk olarak, EntityFramework 'ün ilişkilendirildikleri bilmesini sağlamak için, albüm sınıfmıza bir gezinti özelliği ekleyeceğiz. **Albüm** sınıfınızın son birkaç satırı şu şekilde görünmelidir:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*Note: Bu, System. Collections. Generic ad alanını getirmek için using ifadesinin eklenmesini gerektirir.*

İlk olarak, diğer denetleyicilerimizde olduğu gibi deyimlerini kullanarak bir storeDB alanı ve MvcMusicStore. modeller ekleyeceğiz. Daha sonra, OrderDetails 'e göre en popüler satış albümleri bulmak için veritabanımızı sorgulayan HomeController öğesine aşağıdaki yöntemi ekleyeceğiz.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

Bu, bir denetleyici eylemi olarak kullanılabilir hale getirmek istemediğimiz için özel bir yöntemdir. Bunu basitlik için HomeController içine dahil ediyoruz, ancak iş mantığınızı uygun şekilde ayrı hizmet sınıflarına taşımanız önerilir.

Bu şekilde, Dizin denetleyicisi eylemini en iyi 5 satış albümlerini sorgulamak ve görünüme döndürmek için güncelleştirebiliriz.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

Güncelleştirilmiş HomeController için kodun tamamı aşağıda gösterildiği gibidir.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

Son olarak, model türünü güncelleştirerek ve albüm listesini Alta ekleyerek bir albüm listesi görüntülemesi için giriş dizini görünümümüzü güncelleştirmemiz gerekir. Ayrıca, sayfaya bir başlık ve promosyon bölümü de eklemek için bu fırsatı ele alınacaktır.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

Artık uygulamayı çalıştırdığımızda, en çok satılan albümler ve tanıtım mesajımız ile güncelleştirilmiş giriş sayfamızı görüyoruz.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>Sonuç

ASP.NET MVC 'nin veritabanı erişimi, üyeliği, AJAX vb. ile gelişmiş bir Web sitesi oluşturmayı kolaylaştırdığını gördük. oldukça hızlı. Bu öğreticide, kendi ASP.NET MVC uygulamalarınızı oluşturmaya başlamak için ihtiyacınız olan araçları vermiş olursunuz!

> [!div class="step-by-step"]
> [Öncekini](mvc-music-store-part-9.md)
