---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: Ana sayfaları görüntülemek için veri geçirme (VB) | Microsoft Docs
author: microsoft
description: Bu öğreticinin amacı, bir denetleyiciden verileri bir görünüm ana sayfasına nasıl geçirebileceğiniz hakkında açıklamaktır. Verileri bir görünüme iletmek için iki strateji inceliyoruz...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593700"
---
# <a name="passing-data-to-view-master-pages-vb"></a>Görünüm Ana sayfalarına Veri Geçirme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> Bu öğreticinin amacı, bir denetleyiciden verileri bir görünüm ana sayfasına nasıl geçirebileceğiniz hakkında açıklamaktır. Bir görünüm ana sayfasına veri geçirmek için iki strateji inceliyoruz. İlk olarak, devam eden bir uygulama ile sonuçlanan kolay bir çözümü tartıştık. Daha sonra, biraz daha fazla ilk iş gerektiren, ancak daha sürdürülebilir bir uygulamayla sonuçlandığımız çok daha iyi bir çözüm inceleyeceğiz.

## <a name="passing-data-to-view-master-pages"></a>Ana sayfaları görüntülemek için veri geçirme

Bu öğreticinin amacı, bir denetleyiciden verileri bir görünüm ana sayfasına nasıl geçirebileceğiniz hakkında açıklamaktır. Bir görünüm ana sayfasına veri geçirmek için iki strateji inceliyoruz. İlk olarak, devam eden bir uygulama ile sonuçlanan kolay bir çözümü tartıştık. Daha sonra, biraz daha fazla ilk iş gerektiren, ancak daha sürdürülebilir bir uygulamayla sonuçlandığımız çok daha iyi bir çözüm inceleyeceğiz.

### <a name="the-problem"></a>Sorun

Bir film veritabanı uygulaması oluşturduğunuzu ve uygulamanızdaki her sayfada film kategorilerinin listesini görüntülemek istediğinizi varsayın (bkz. Şekil 1). Ayrıca, film kategorilerinin listesinin bir veritabanı tablosunda depolandığını düşünün. Bu durumda, Kategoriler veritabanından alınır ve film kategorilerinin listesini bir görünüm ana sayfası içinde işleyebilir.

[bir görünüm ana sayfasında film kategorilerini görüntüleme ![](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**Şekil 01**: bir görünüm ana sayfasında film kategorilerini görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](passing-data-to-view-master-pages-vb/_static/image3.png))

Sorun aşağıda verilmiştir. Ana sayfadaki film kategorilerinin listesini nasıl alabilirsiniz? Doğrudan ana sayfada model sınıflarınızın yöntemlerini çağırmak önemlidir. Diğer bir deyişle, verileri doğrudan ana sayfanızda veritabanından almak için kodu eklemek önemlidir. Ancak, MVC denetleyicilerinizi veritabanına erişmek için atlamak, MVC uygulaması oluşturmanın başlıca avantajlarından biri olan kaygıların temiz ayrılmasını ihlal ediyor.

MVC uygulamasında, MVC görünümleriniz ve MVC modeliniz arasındaki tüm etkileşimlerin MVC denetleyicilerinizi tarafından işlenmesini istiyorsunuz. Bu önemli noktalar, daha sürdürülebilir, uyarlanamayacak ve test edilebilir bir uygulamayla sonuçlanır.

MVC uygulamasında, görünüm ana sayfası dahil olmak üzere bir görünüme geçirilen tüm veriler, bir denetleyici eylemi tarafından bir görünüme geçirilmelidir. Ayrıca, verilerin görünüm verilerinden faydalanması gerekir. Bu öğreticinin geri kalanında, görünüm ana sayfasına veri görüntülemeyi iki yöntemle inceleyeceğiz.

### <a name="the-simple-solution"></a>Basit çözüm

Bir denetleyiciden bir görünüm ana sayfasına veri görüntüleme için en basit çözümle başlayalım. En basit çözüm, ana sayfanın görünüm verilerini her bir denetleyici eyleminde geçirmektir.

Döküm 1 ' de denetleyiciyi göz önünde bulundurun. `Index()` ve `Details()`adlı iki eylemi kullanıma sunar. `Index()` Action yöntemi, filmler veritabanı tablosundaki her filmi döndürür. `Details()` Action yöntemi, belirli bir film kategorisindeki her filmi döndürür.

**Listeleme 1 – `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

Hem `Index()` hem de `Details()` eylemlerinin verileri görüntülemek için iki öğe eklemediğine dikkat edin. `Index()` eylemi iki anahtar ekler: Kategoriler ve filmler. Kategoriler anahtarı, görünüm ana sayfası tarafından gösterilecek film kategorilerinin listesini temsil eder. Filmler anahtarı, dizin görünümü sayfası tarafından görünen filmlerin listesini temsil eder.

`Details()` eylemi Kategoriler ve filmler adlı iki anahtar da ekler. Kategoriler anahtarı, bir kez daha, görünüm ana sayfasında görüntülenecek film kategorilerinin listesini temsil eder. Filmler anahtarı, Ayrıntılar görünümü sayfası tarafından görünen belirli bir kategorideki filmlerin listesini temsil eder (bkz. Şekil 2).

[Ayrıntılar görünümünü ![](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**Şekil 02**: Ayrıntılar görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](passing-data-to-view-master-pages-vb/_static/image6.png))

Dizin görünümü liste 2 ' de yer alır. Bu, verileri görüntüleme içindeki film öğesi tarafından temsil edilen film listesi boyunca yinelenir.

**Listeleme 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

Ana görünüm sayfası, Listeleme 3 ' te bulunur. Görünüm ana sayfası, görünüm verilerinden Kategoriler öğesi tarafından temsil edilen tüm film kategorilerini yineler ve işler.

**Listeleme 3 – `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

Tüm veriler görünüm verileri aracılığıyla görünüme ve ana görünüm sayfasına geçirilir. Bu, verileri ana sayfaya geçirmenin doğru yoludur.

Bu nedenle, bu çözümle ilgili sorun nedir? Sorun, bu çözümün kurutma (Kendini Tekrarlama) ilkesini ihlal ediyor olması. Her bir ve her denetleyici eylemi, verileri görüntülemek için film kategorilerinin çok aynı listesini eklemesi gerekir. Uygulamanızda yinelenen kod bulunması, uygulamanızın bakımını, uyarlanmasını ve değiştirilmesini çok daha zor hale getirir.

### <a name="the-good-solution"></a>Iyi çözüm

Bu bölümde, bir denetleyici eyleminden verileri bir görünüm ana sayfasına geçirmek için alternatif ve daha iyi bir çözüm inceleyeceğiz. Her bir denetleyici eyleminde ana sayfa için film kategorilerini eklemek yerine, film kategorilerini yalnızca bir kez görüntüleme verilerine ekleyeceğiz. Görünüm ana sayfası tarafından kullanılan tüm görünüm verileri bir uygulama denetleyicisine eklenir.

ApplicationController sınıfı, listeleme 4 ' te bulunur.

ApplicationController sınıfı, listeleme 4 ' te bulunur.

**Listeleme 4 – `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

Liste 4 ' te uygulama denetleyicisi hakkında dikkat etmeniz gereken üç şey vardır. İlk olarak, sınıfın temel System. Web. Mvc. Controller sınıfından devraldığından emin olun. Uygulama denetleyicisi bir denetleyici sınıfıdır.

İkincisi, uygulama denetleyicisi sınıfının bir MustInherit sınıfı olduğuna dikkat edin. MustInherit sınıfı, somut bir sınıf tarafından uygulanması gereken bir sınıftır. Uygulama denetleyicisi bir MustInherit sınıfı olduğundan, sınıfta doğrudan tanımlanmış herhangi bir yöntemi çağıramazsınız. Uygulama sınıfını doğrudan çağırmaya çalışırsanız, bir kaynak bulunamıyor hata iletisi alırsınız.

Üçüncü olarak, uygulama denetleyicisinin verileri görüntülemek için film kategorilerinin listesini ekleyen bir Oluşturucu içerdiğine dikkat edin. Uygulama denetleyicisinden devralan her denetleyici sınıfı, uygulama denetleyicisinin oluşturucusunu otomatik olarak çağırır. Uygulama denetleyicisinden devralan herhangi bir denetleyici üzerinde herhangi bir eylem çağırdığınızda, film kategorileri görünüm verilerine otomatik olarak eklenir.

Kod 5 ' teki filmler denetleyicisi uygulama denetleyicisinden devralınır.

**Listeleme 5 – `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

Önceki bölümde ele alınan giriş denetleyicisi gibi film denetleyicisi, `Index()` ve `Details()`adlı iki eylem yöntemini kullanıma sunar. Görünüm ana sayfası tarafından görüntülenen film kategorilerinin listesinin `Index()` veya `Details()` yönteminde verileri görüntülemek için eklenmediğine dikkat edin. Film denetleyicisi uygulama denetleyicisinden devraldığından, film kategorilerinin listesi verileri otomatik olarak görüntülemek için eklenir.

Bir görünüm ana sayfasına yönelik Görünüm verilerini eklemek için bu çözümün kurutma (Kendini Tekrarlama) ilkesini ihlal etmediğine dikkat edin. Verileri görüntülemek için film kategorilerinin listesini ekleme kodu yalnızca bir konuma dahil edilir: uygulama denetleyicisinin Oluşturucusu.

### <a name="summary"></a>Özet

Bu öğreticide, verileri bir denetleyiciden görünüm ana sayfasına geçirmek için iki yaklaşım ele alınmıştır. İlk olarak, basit bir yaklaşım inceliyoruz, ancak yaklaşımdan korursunuz. İlk bölümde, uygulamanızdaki her bir denetleyici eyleminde bir görünüm ana sayfasına yönelik Görünüm verilerini nasıl ekleyebileceğiniz açıklanmıştır. KURUTMA (Kendini Tekrarlama) prensibi ihlal ettiğinden bunun hatalı bir yaklaşım olduğunu sonuçlandırtık.

Daha sonra, verileri görüntülemek için bir görünüm ana sayfasının gerektirdiği verileri eklemek için çok daha iyi bir strateji inceliyoruz. Her bir denetleyici eyleminde Görünüm verilerini eklemek yerine, Görünüm verilerini bir uygulama denetleyicisi içinde yalnızca bir kez ekledik. Bu şekilde, bir ASP.NET MVC uygulamasındaki bir görünüm ana sayfasına veri geçirirken yinelenen koddan kaçınabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](creating-page-layouts-with-view-master-pages-vb.md)
