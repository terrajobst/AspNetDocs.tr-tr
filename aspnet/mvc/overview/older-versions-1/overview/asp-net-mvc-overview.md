---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC genel bakış | Microsoft Docs
author: microsoft
description: ASP.NET MVC uygulaması ve ASP.NET Web Forms uygulamaları arasındaki farklılıklar hakkında bilgi edinin. ASP.NET MVC uygulaması oluşturmaya ne zaman karar vereceğiniz hakkında bilgi edinin.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 73965c71f37de13e3813df089a253fde528ea7ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541561"
---
# <a name="aspnet-mvc-overview"></a>ASP.NET MVC’ye Genel Bakış

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET MVC uygulaması ve ASP.NET Web Forms uygulamaları arasındaki farklılıklar hakkında bilgi edinin. ASP.NET MVC uygulaması oluşturmaya ne zaman karar vereceğiniz hakkında bilgi edinin.

Model-View-Controller (MVC) mimari modeli, bir uygulamayı üç ana bileşene ayırır: model, görünüm ve denetleyici. ASP.NET MVC Framework, MVC tabanlı Web uygulamaları oluşturmak için ASP.NET Web Forms düzenine bir alternatif sağlar. ASP.NET MVC çerçevesi; ana sayfalar ve üyelik tabanlı kimlik doğrulaması gibi mevcut ASP.NET özellikleriyle (Web Forms tabanlı uygulamalarda olduğu gibi) birleştirilebilen basit, yüksek düzeyde sınanabilir bir sunu çerçevesidir. MVC çerçevesi, **System. Web. Mvc** ad alanında tanımlanmıştır ve **System. Web** ad alanının temel ve desteklenen bir parçasıdır.   
  
MVC, çoğu geliştiricinin tanıdığı standart bir tasarım örüntüsüdür. Web uygulamalarının bazı türleri MVC çerçevesinden faydalanır. Diğer türler, Web Forms ve geri göndermelere dayanan geleneksel ASP.NET uygulama örüntüsünü kullanmaya devam eder. Web uygulamalarının diğer türleri iki yaklaşımı birleştirir; her iki yaklaşım da diğerini dışlamaz.   
  
MVC çerçevesinde aşağıdaki iki bileşen yer almaktadır:

[bir parametre değeri bekleyen bir denetleyici eylemini çağırma ![](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Şekil 01**: parametre değeri bekleyen bir denetleyici eylemi çağırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](asp-net-mvc-overview/_static/image2.png))

- **Modeller**. Model nesneleri uygulamanın, uygulama verileri etki alanı için mantığı uygulayan parçalarından oluşur. Model nesneleri sıklıkla model durumunu bir veritabanına alır ve burada depolar. Örneğin, bir ürün nesnesi bir veritabanından bilgi alabilir, üzerinde işlem yapar ve ardından SQL Server bir Ürünler tablosuna güncelleştirilmiş bilgileri geri yazabilir.

Küçük uygulamalarda, model, genellikle fiziksel ayrım yerine kavramsal bir ayrımdır. Örneğin, uygulama yalnızca bir veri kümesini okur ve görünüme gönderirse, uygulamanın bir fiziksel model katmanı ve ilişkili sınıfları yoktur. Bu durumda, veri kümesi bir model nesnesinin rolünü alır.

- **Görünümler**. Görünümler, uygulama kullanıcı arabirimini (UI) görüntüleyen bileşenlerdir. Bu UI, genellikle model verilerinden oluşturulur. Bir ürün tablosunun, bir ürünler nesnesinin geçerli durumuna bağlı olarak metin kutularını, açılan listeleri ve onay kutularını gösteren bir düzenleme görünümü bir örnektir.

- **Denetleyici**. Denetleyiciler; kullanıcı etkileşimini işleyen, modelle çalışan ve son olarak UI'ı görüntüleyecek görünümü seçerek işleyen bileşenlerdir. Bir MVC uygulamasında, görünüm yalnızca bilgileri görüntüler; denetleyici ise kullanıcı girişini ve etkileşimini işler ve bunlara yanıt verir. Örneğin, Denetleyici sorgu dize değerlerini işler ve bu değerleri modele geçirir, bu da değerleri kullanarak veritabanını sorgular.

MVC örüntüsü, öğeler arasında (giriş mantığı, iş mantığı ve UI mantığı) sıkı bir ilişki sağlarken, uygulamanın bu farklı yönlerini birbirlerinden ayıran uygulamalar oluşturmanıza yardımcı olur. Örüntü, her bir mantık türünün uygulamanın hangi konumunda yer alması gerektiğini belirtir. UI mantığı görünümde yer alır. Giriş mantığı denetleyicide yer alır. İş mantığı modelde yer alır. Bu ayrım, bir uygulama oluşturduğunuzda bir seferde uygulamanın tek bir yönüne odaklanmanızı sağladığı için karışıklığı yönetmenize yardımcı olur. Örneğin, iş mantığına bağlı kalmaksızın görünüme odaklanabilirsiniz.   
  
Karışıklığın yönetilmesine ek olarak, MVC örüntüsü, MVC kullanılarak geliştirilen uygulamaların sınanmasını, Web Form tabanlı ASP.NET Web uygulamalarının sınanmasından daha kolay bir hale getirmektedir. Örneğin, Web Forms tabanlı ASP.NET Web uygulamasında, hem çıkışı görüntülemek hem de kullanıcı girişine yanıt vermek için tek bir sınıf kullanılır. Web Forms tabanlı ASP.NET uygulamaları için otomatikleştirilmiş test yazılması, belirli bir sayfayı test etmek üzere sayfa sınıfı, sayfanın tüm alt denetimleri ve uygulamadaki ek bağımlı sınıfları başlatmanız gerektiği için karmaşık olabilir. Sayfayı çalıştırmak için çok sayıda sınıf çalıştırıldığı için uygulamanın belirli parçalarına özel olarak odaklanan testleri yazmak zor olabilir. Bu yüzden, Web Forms tabanlı ASP.NET uygulamalarına yönelik testlerinin uygulanması MVC uygulamasındaki testlere göre daha zor olabilir. Üstelik, Web Forms tabanlı ASP.NET uygulamasındaki testler için bir Web sunucusu gerekir. MVC çerçevesi bileşenleri ayrıştırır ve belirli bileşenlerin çerçevenin geri kalanındaki yalıtılmış bir şekilde test edilmelerini kolaylaştıracak şekilde, arabirimlerin kullanımına ağırlık verir.   
  
MVC uygulamasının ilgili üç ana bileşeni arasındaki bu sıkı bağ aynı zamanda paralel gelişimi de kolaylaştırır. Örneğin, bir geliştirici görünümde çalışırken, ikinci bir geliştirici denetleyici mantığı üzerinde çalışabilir ve üçüncü bir geliştirici modeldeki iş mantığına odaklanabilir.

## <a name="deciding-when-to-create-an-mvc-application"></a>MVC uygulaması oluşturma ne zaman karar verme

Bir Web uygulamasını uygulamak için ASP.NET MVC çerçevesinin mi, yoksa ASP.NET Web Forms modelinin mi kullanılacağını dikkatli şekilde ele almanız gerekmektedir. MVC çerçevesi, Web Forms modelini değiştirmez; Web uygulamaları için ikisinden birini kullanabilirsiniz. (Mevcut Web Forms tabanlı uygulamalarınız varsa, bu uygulamalar her zamanki gibi düzgün şekilde çalışmaya devam eder.)   
  
Belirli bir Web sitesi için MVC çerçevesi veya Web Forms modeli kullanmaya karar vermeden önce, her iki yaklaşımın avantajlarını masaya yatırın.

### <a name="advantages-of-an-mvc-based-web-application"></a>MVC Tabanlı Web Uygulamasının Avantajları

ASP.NET MVC çerçevesi aşağıdaki avantajları sağlamaktadır:

- Uygulamayı modele, görünüme ve denetleyiciye bölerek karışıklığın yönetilmesini kolaylaştırır.
- Görünüm durumu veya sunucu tabanlı formlar kullanmaz. Bu, uygulamanın davranışı üzerinde tam denetim sağlamak isteyen geliştiriciler için MVC çerçevesini ideal kılar.
- Tek bir denetleyici üzerinden Web uygulama isteklerini işleyen bir Front Controller örüntüsü kullanır. Zengin yönlendirme altyapısını destekleyen bir uygulama tasarlamanızı sağlar. Daha fazla bilgi için bkz. MSDN Web sitesindeki [ön denetleyici](https://go.microsoft.com/fwlink/?LinkId=106357 "Ön denetleyici") .
- Teste dayalı geliştirme (TDD) için daha iyi destek sunar.
- Büyük geliştiriciler ve uygulama davranışı üzerinde yüksek düzeyde denetim gerektiren web tasarımcıları tarafından desteklenen Web uygulamaları için iyi sonuç verir.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web Forms Tabanlı Web Uygulamasının Avantajları

Web Forms tabanlı çerçeve aşağıdaki avantajları sağlamaktadır:

- İş dalına özel Web uygulaması geliştirmeleri için faydalı olan, HTTP üzerindeki durumu koruyan olay modelini destekler. Web Forms tabanlı uygulama, yüzlerce sunucu denetiminde desteklenen düzinelerce olayı sağlar.
- Belirli sayfalara işlevsellik ekleyen Page Controller örüntüsünü kullanır. Daha fazla bilgi için MSDN Web sitesindeki [sayfa denetleyicisi](https://go.microsoft.com/fwlink/?LinkId=106359 "Sayfa denetleyicisi") ' ne bakın.
- Durum bilgilerini yönetmeyi kolaylaştırmak için görünüm durumunu veya sunucu tabanlı formları kullanır.
- Hızlı uygulama geliştirme için çok sayıdaki mevcut bileşenden faydalanmak isteyen küçük Web geliştiricileri ve tasarımcıları ekipleri için uygundur.
- Genel olarak, uygulama geliştirme için daha az karmaşıktır çünkü bileşenler ( **sayfa** sınıfı, denetimler, vb.) sıkı bir şekilde tümleşiktir ve genellikle MVC modelinden daha az kod gerektirir.

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC Çerçevesinin Özellikleri

ASP.NET MVC çerçevesi aşağıdaki özellikleri sunmaktadır:

- Varsayılan olarak uygulama görevlerinin (Giriş mantığı, iş mantığı ve UI mantığı), yük kararlılığı ve test odaklı geliştirme (TDD) ayrımı. MVC çerçevesindeki tüm esas sözleşmeler arabirim tabanlı olup, uygulamadaki asıl nesnelerin davranışını taklit eden benzetimli nesneler olan sahte nesneler kullanılarak test edilebilir. ASP.NET işlemindeki denetleyicileri çalıştırmaksızın, hızlı ve esnek bir şekilde uygulamada birim testi gerçekleştirebilirsiniz. .NET Framework ile uyumlu olan her türlü birim testi çerçevesini kullanabilirsiniz.
- Genişletilebilir ve eklenebilir bir çerçeve. ASP.NET MVC çerçevesinin bileşenleri kolay şekilde değiştirilebilmesi veya özelleştirilebilmesi için tasarlanır. Kendi görünüm altyapınızı, URL yönlendirme ilkenizi, eylem yöntemi parametrenizin serileştirilmesini ve diğer bileşenleri ekleyebilirsiniz. ASP.NET MVC çerçevesi aynı zamanda Bağımlılık Ekleme (DI) ve Denetimi Tersine Çevirme (IOC) kapsayıcı modellerinin kullanımını da destekler. Dı, nesne kendisini oluşturmak için sınıfa güvenmek yerine bir sınıfa nesneleri eklemenizi sağlar. IOC, bir nesne başka bir nesneyi gerektirirse, birinci nesnenin ikinci nesneyi yapılandırma dosyası gibi bir dış kaynaktan alınması gerektiğini belirtir. Bu işlem, testi kolaylaştırır.
- Mantıklı ve aranabilir URL 'Ler içeren uygulamalar oluşturmanıza olanak tanıyan güçlü bir URL eşleme bileşeni. URL'lere dosya adı uzantıları dahil değildir ve URL'ler arama motoru iyileştirmesi (SEO) ve temsili durum aktarımı (REST) adreslemesiyle düzgün şeklide çalışan URL adlandırma modelleri için tasarlanır.
- Görünüm şablonları olarak mevcut ASP.NET sayfası (.aspx dosyaları), kullanıcı denetimi (.ascx dosyaları) ve ana sayfa (.master dosyaları) biçimlendirme dosyalarında biçimlendirmeyi kullanma desteği. Mevcut ASP.NET özelliklerini, iç içe geçmiş ana sayfalar, satır içi ifadeler (&lt;% =%&gt;), bildirime dayalı sunucu denetimleri, şablonlar, veri bağlama, yerelleştirme vb. gibi ASP.NET MVC çerçevesiyle birlikte kullanabilirsiniz.
- Mevcut ASP.NET özellikleri için destek. ASP.NET MVC; formların kimlik doğrulaması, Windows kimlik doğrulaması, URL yetkilendirmesi, üyelik ve roller, çıkış ve veri arabelleğe alma, oturum ve profil durumu yönetimi, sistem durumu izleme, yapılandırma sistemi ve sağlayıcı mimarisi gibi özellikleri kullanmanızı sağlar.
